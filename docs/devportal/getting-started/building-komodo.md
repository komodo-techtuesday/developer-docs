# Getting Started

## Building Komodo From Source
### Prerequisites
On ubuntu, these packages cover the bare minimum, lowest requirement

### With Additional Utilities
On ubuntu 18.04 these packages provide usefulness

### Compile & Install
        git clone https://github.com/komodoplatform/komodo.git
        cd komodo
        git checkout dev
        ./zcutil/fetch-params.sh
        ./zcutil/build.sh -j$(nproc)
        mkdir ~/.komodo
        touch komodo.conf
        rpcuser=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 24 | head -n 1)
        rpcpassword=$(cat /dev/urandom | tr -dc 'a-zA-Z0-9' | fold -w 24 | head -n 1)
        echo "rpcuser=$rpcuser" > komodo.conf
        echo "rpcpassword=$rpcpassword" >> komodo.conf
        echo "daemon=1" >> komodo.conf
        echo "server=1" >> komodo.conf
        echo "txindex=1" >> komodo.conf
        chmod 0600 komodo.conf
        ln -sf $KMD_SRC/src/komodo-cli /usr/local/bin/komodo-cli
        ln -sf $KMD_SRC/src/komodod /usr/local/bin/komodod


### Commands Quick Reference

* `komodod` - daemon start.
* `komodo-cli getinfo` - get komodo info.
* `komodo-cli getpeerinfo` - get peers.
* `komodo-cli getnewaddress` - generate a new privkey/pubkey combo (address).
* `komodo-cli validateaddress <ADDRESS>` - validate address.
* `komodo-cli sendtoaddress <ADDRESS> <AMOUNT> "note" "memo" true` - send funds to an address.

All the komodo commands work with custom blockchains.  Use the `-ac_name=<NAME>` parameter
* `komodo-cli -ac_name=CUSTOMCHAIN1 getinfo` - get customchain1 info.
* `komodo-cli -ac_name=CUSTOMCHAIN2 getinfo` - get customchain2 info.



## Starting & Syncing

For the komodo mainnet chain, simply start komodo
   
        komodod -daemon

To start an existing custom blockchain, use the custom chain's parameters.

        komodod -ac_name=EXISTINGCHAIN -ac_supply....

To create a custom blockchain:

        komodod -ac_name=CUSTOMCHAIN1 -ac_supply.....

## Data Directory

The default location is .komodo in your home directory.  You can specify a custom location when starting the daemon

        komodod -datadir=/my/custom/location

### Project layout

    .komodo/         # Default data home dir
        db.log
        debug.log
        fee_estimates.dat
        komdoo.conf  # configuration file
        komodo.pid
        komodostate
        komodostate.ind
        lograte-state
        logrotate.conf
        notarisations/
        peers.dat
        realtime
        wallet.dat
        CUSTOMCHAIN1/  # Your custom chain data dir
            CUSTOMCHAIN1.conf
            blocks/
            chainstate/
            database/
            db.log
            debug.log
            fee_estimates.dat
            komodostate
            komodostate.ind
            notarisations/
            peers.dat
            wallet.dat
        CUSTOMCHAIN2/  # Your custom chain data dir
            ...
        CUSTOMCHAIN3/  # Your custom chain data dir
            ...
        CUSTOMCHAIN4/  # Your custom chain data dir
            ...



## Configuration & Logs

Configuration & logging goes to CHAINNAME.conf & debug.log in the data dir.

## Important wallet.dat

Private keys are stored in wallet.dat
Making a backup can be created with

* `komodo-cli backupwallet` - 

## Security Considerations
Having physical access to your server is always ideal for maximum security.  If in a leased or co-location environment, be sure to monitor the server for any intrusion.

### Firewall
Using an intrusion detection system like fail2ban will ....

### SSH
Protecting ssh login with a key reduces risk of brute force.
Changing the port number from default tcp/22 can also be beneficial - be sure to update any maintenance scripts and firewall rules.

### Non-Essential Software
Relying on third party software that is not related to running your blockchain project on the same server adds an unquantifiable added risk.

### 2FA/MFA
When using any service related to your blockchain project, be sure to employ stricter controls on accessing third party services.   Any information can be used against you to gain access to your secure blockchain environment.