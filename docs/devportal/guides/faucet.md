* [linktocode](#)


## Validation
``` cpp

bool FaucetValidate(struct CCcontract_info *cp,Eval* eval,const CTransaction &tx, uint32_t nIn)
{
    int32_t numvins,numvouts,preventCCvins,preventCCvouts,i,numblocks; bool retval; uint256 txid; uint8_t hash[32]; char str[65],destaddr[64];
    std::vector<std::pair<CAddressIndexKey, CAmount> > txids;
    numvins = tx.vin.size();
    numvouts = tx.vout.size();
    preventCCvins = preventCCvouts = -1;
    if ( numvouts < 1 )
        return eval->Invalid("no vouts");
    else
    {
        for (i=0; i<numvins; i++)
        {
            if ( IsCCInput(tx.vin[0].scriptSig) == 0 )
            {
                fprintf(stderr,"faucetget invalid vini\n");
                return eval->Invalid("illegal normal vini");
            }
        }
        //fprintf(stderr,"check amounts\n");
        if ( FaucetExactAmounts(cp,eval,tx,1,10000) == false )
        {
            fprintf(stderr,"faucetget invalid amount\n");
            return false;
        }
        else
        {
            preventCCvouts = 1;
            if ( IsFaucetvout(cp,tx,0) != 0 )
            {
                preventCCvouts++;
                i = 1;
            } else i = 0;
            txid = tx.GetHash();
            memcpy(hash,&txid,sizeof(hash));
            fprintf(stderr,"check faucetget txid %s %02x/%02x\n",uint256_str(str,txid),hash[0],hash[31]);
            if ( tx.vout[i].nValue != FAUCETSIZE )
                return eval->Invalid("invalid faucet output");
            else if ( (hash[0] & 0xff) != 0 || (hash[31] & 0xff) != 0 )
                return eval->Invalid("invalid faucetget txid");
            Getscriptaddress(destaddr,tx.vout[i].scriptPubKey);
            SetCCtxids(txids,destaddr);
            for (std::vector<std::pair<CAddressIndexKey, CAmount> >::const_iterator it=txids.begin(); it!=txids.end(); it++)
            {
                //int height = it->first.blockHeight;
                if ( CCduration(numblocks,it->first.txhash) > 0 && numblocks > 3 )
                {
                    //fprintf(stderr,"would return error %s numblocks.%d ago\n",uint256_str(str,it->first.txhash),numblocks);
                    return eval->Invalid("faucet is only for brand new addresses");
                }
            }
            retval = PreventCC(eval,tx,preventCCvins,numvins,preventCCvouts,numvouts);
            if ( retval != 0 )
                fprintf(stderr,"faucetget validated\n");
            else fprintf(stderr,"faucetget invalid\n");
            return(retval);
        }
    }

```
