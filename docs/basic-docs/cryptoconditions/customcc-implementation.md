## Introduction

*THIS SECTION FOR THE NEXT 50 OR SO LINES UNTIL EOF SHOULD GO IN SOME NARRATIVE SECTION*

Think about making your own blockchain rules beyond simple value transactions, Satoshi and gen1 and gen2 blockchains have done this.  Now is the time to include abstract concepts like objects for consensus.

This example custom consensus is just something that requires to send 1 coin.  It only allows you to send exactly 1 coin.

::Given the book ***mastering bitcoin***, any decent senior C/C++ coder will be able to do custom consensus just fine

Understanding the UTXO model and ability to do some coding is the pathway to creating custom consensus for your application's blockchain.  The first consensus took many year to get working stable, e.g. bitcoin protocol.  **Before Komodo's custom consensus and a new consensus was required, it was a big project.**

Komodo allows you to add your creativity into the consensus mechanism itself, without having to rewrite the consensus mechanism from scratch.  Changing consensus rules with CC is a lot easier.  The working customcc.cpp is simple enough that it is possible for a coder to do it in a few hours and adding extra functionality to this new consensus can be done within a week for more complex things.

**Instead of taking years, it is reduced to weeks or days**.

What differentiates a smart contract from a custom consensus?  A smart contract is an interpreted set of commands.  A custom consensus is a network wide agreement on the fundamentals of programming logic.  The subtle difference is that smart contracts deal with approximations.  The native code is the real thing instaed of a simulation of something that must be interpreted.

The number of blockchain consensus rules created in the first 10 years including bitcoin and ethereum, can be created by a dedicated team within a month.  There is a 100x consensus productivity upgrade by being able to create custom consensus modules.

## Workflow of updating the rules to a game
You don't want to have to run a centralized database, because then it would put the responsibility over consensus and fairplay on your shoulders.  Instead put it on your players. This saves you loads of hassle. Everyone can verify the blockchain, and therefore everyone can be assured that the gameplay and the blockchain are in harmony.

Once you start adding a gameplay rule to a normal blockchain, you're basically dealing with a whole new consensus mechanism. It took years to make the Bitcoin consensus mechanism stable.

CC allows you to add in your creativity, without having to start over.  All custom consensus is derived from the underlying UTXO model, and this UTXO model is re-used at the custom layer with a new UTXO type - the custom gameplay rules.  Gameplay rules are part of the consensus without having to start in the testing phase of basic UTXO consensus.

## Integrating custom consensus with others
Imagine you have a style of making a game better.  This is your expertise.  It might be hard to apply this element that you bring, and you're good at it. You can basically plug that into a small module, and test it out without having to re-code the whole blockchain from scratch.

**EOF**

## Consensus needs validation

All you need to do is transaction level validation, all the block level consensus is automatic.  The transaction is still following all the existing consensus rules.

In the header's declaration of functions, custom_validate (MYCCNAME_validate where MYCCNAME=custom) it says "[validation code is the most important](/basic-docs/cryptoconditions/customcc-masterclass.md#declaration-of-functions)

Validation must return true.  Reasons it may not return true are logical:
* The number of vouts/vins does not equal an expected number
* An invalid opreturn, verify there is an opreturn
* The amounts and destination match the expected values and that it is a CC spend

This is the evaluation of EVAL_CUSTOM #evalcade

The sample custom_validate is really simple.   As you **make more CC methods, you need to add the corresponding validation**, otherwise they are not validated.

### Stepping through the validation

```
char expectedaddress[64]; CPubKey pk;
```
`char expectedaddress[64]` and `CPubKey pk` declare a character array of 64 bytes and pubkey.

```
if ( tx.vout.size() != 2 ) // make sure the tx only has 2 outputs
return eval->Invalid("invalid number of vouts");
```
Those two lines make sure the tx has only 2 vouts.

```
else if ( custom_opretdecode(pk,tx.vout[1].scriptPubKey) != '1' ) // verify has opreturn
return eval->Invalid("invalid opreturn");
```
This runs the massively complex custom_opretdecode function to determine if it has a valid opreturn - more information about this function is below in [opretdecode](#)

```
GetCCaddress(cp,expectedaddress,pk);
```
That gets the CC address for the pk (pubkey) and assigns it to `expectedaddress`.  More info about this internal helper function is [below](#)

```
if ( IsCClibvout(cp,tx,0,expectedaddress) == COIN ) // make sure amount and destination matches
return(true);
```
That checks the transaction, vout `0` to make sure it is a CC vout for 1 COIN.  `COIN` is defined in `src/amount.h` as 100000000 (100 million).

More info on the [IsCClibvout](#) is below.  It returns the value, and why we can compare it to 100000000 (100 million) because that is the value we accept for validation in this exercise. *1 COIN*.

Let's summarize this:
* It checks the tx, vout0 to make sure it is a CC vout for 1.00000000 COINS
* So if it got that far, the tx has 2 vouts, second one is a valid opreturn and the first one is for 1 COIN -> return true
* Otherwise `else return eval->Invalid("invalid vout0 amount");` that returns false with an error message "invalid vout0 amount"

## Instructive design flaw
This will be a lesson you won't soon forget.  Despite the simplicity of the validation (and therefore the consensus), it has a design flaw.  You will only notice how useless it is, despite it being a send-one-coin consensus rule when the design flaw is understood.

Can you see it yet?  If not, it doesn't matter - more will be revealed.

To understand why it is useless, it is good to understand the RPC call that creates the transaction that is being validated.

## custom_func0
This function simply responds with a string, and because it is wired together with an RPC call to `custom_func01`, your CLI or RPC wrapper will receive this string response.

## custom_func1



## GetCCaddress internal function
GetCCaddress ([src](https://github.com/jl777/komodo/blob/jl777/src/cc/CCinclude.h#L262)) accepts these arguments:
* `cp` is *this consensus* pointer
* `expectedaddress` is the destination (an array, also passable to (a c++) function that accepts a pointer as a parameter)
* pubkey.

## IsCClibvout internal function
IsCClibvout returns the satoshis of the specified vout.

This is a nice helper function for the custom consensus library you're making.  It simply returns the `tx.vout[0].nValue` because it is passed the transaction vout index of `0`.

Similar functions can be found in other custom consensus source files like [IsRewardsVout](https://github.com/jl777/komodo/blob/jl777/src/cc/rewards.cpp#L144) checks similarly and returns the value.

## opretdecode internal function
This function returns the `funcid` defined in the `RPC_FUNCS` in the `custom.h` file.  The `e` and `f` are the eval code and the funcid.

This function is used in other custom consensus, customized for different modules.  For now whilst learning how to code a custom consensus, stick to index numbers.  The id is a byte, and for more complex custom consensus, maybe it will assist GUI developers if the ids were instead, a character representing a behaviour or property, e.g. 'w'rite or 'r'ead or 'd'double or 's'plit.

 For instance, the funcid for the [Rewards](#) use a `char` to identify what different functions do, and during validation, [only 'U' will unlock funds](https://github.com/jl777/komodo/blob/jl777/src/cc/rewards.cpp#L239).

The same is done in [oracles.cpp](https://github.com/jl777/komodo/blob/jl777/src/cc/oracles.cpp#L651) but simply reading the script[1] byte.


## Other notes
* tx.vout[0].nValue is the amount
* tx.vout[0].scriptPubKey is the spending script (destination)
