## PR List for Activating dPoW
In order to activate dPoW you need to submit PR into 2 GitHub repos.
1. Komodo repo (`dev` branch) - [https://github.com/jl777/komodo](https://github.com/jl777/komodo)  
2. SuperNET repo (`dev` branch) - [https://github.com/jl777/SuperNET](https://github.com/jl777/SuperNET)  

## Changes required for Komodo repo
2 new file needs creating and 2 existing files needs updating. These new files are executable scripts named as the coin ticker with small letters. They would go inside `~/komodo/src/ac/` and `~/komodo/src/fiat/` dir and required for quering the chain easily. i.e.: `~/komodo/src/ac/zex getinfo`.

Contents of these 2 new files would be as following:
```shell
#!/bin/bash
./komodo-cli -ac_name=ZEX $1 $2 $3 $4 $5 $6
```
So, you will have [`~/komodo/src/ac/zex`](https://github.com/jl777/komodo/blob/dev/src/ac/zex) and [`~/komodo/src/fiat/zex`](https://github.com/jl777/komodo/blob/dev/src/fiat/zex). **Make sure both of the files has proper execute permission.**

Next, is to add coin parameters at the bottom of [`assetchains.json`](https://github.com/jl777/komodo/blob/dev/src/assetchains.json#L202) and [`assetchains.old`](https://github.com/jl777/komodo/blob/dev/src/assetchains.old#L47) files inside `~/komodo/src/` directory. Please check the links to the files to understand how they were done. The `.json` file is basically converting the ZEX chain start command from shell fromat to JSON format.

Check [this commit](https://github.com/jl777/komodo/commit/7f5ed6ec453b78042bd791062203452a7043aa93) to fully understand what was done to add ZEX in Komodo repo.

### Step 2.2 Changes required for SuperNET repo
For SuperNET repo we need to add 1 new file called [`zex_7776`](https://github.com/jl777/SuperNET/blob/dev/iguana/coins/zex_7776) inside `~/SuperNET/iguana/coins/` (please change zex with your coin ticker). **Make sure this file has executable permission.** This file gets created automatically in the directory where you start the chain from. Generally inside `~/komodo/src/` dir.

And, we need to edit 4 existing files, [`dpowassets`](https://github.com/jl777/SuperNET/blob/dev/iguana/dpowassets#L50), [`iguana_notary.c`](https://github.com/jl777/SuperNET/blob/dev/iguana/iguana_notary.c#L543), [`m_notary_run`](https://github.com/jl777/SuperNET/blob/dev/iguana/m_notary_run#L106) & [`m_splitfund`](https://github.com/jl777/SuperNET/blob/dev/iguana/m_splitfund#L51)) inside `~/SuperNET/iguana/` dir. These links points to the line where you should be checking.

Check [this commit](https://github.com/jl777/SuperNET/commit/c715f0aa4c99d20de6b99b5d173d543d2a94010f) to fully understand what was done to add ZEX in SuperNET repo.

Once you have all the changes done locally, you can submit a PR to Komodo and SuperNET repo `dev` branch. After the PR gets merged by jl777, it will be announced and Komodo Notary Node operators will update their node and start notarizing the coin.