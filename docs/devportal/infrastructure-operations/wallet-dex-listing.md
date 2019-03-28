***************************************
Add Komodo Assetchains in Agama Desktop
***************************************

The Agama desktop code comprises of two parts. Backend and UI. This assetchain adding guide will cover both. All the files needs changing are linked. If you want to add Bitcoin compatible coins follow :doc:`this guide <add-Bitcoin-Compatible-coin-Agama-Desktop>`.

## Backend

* Add a default asset chain port `KomodoPlatform/Agama:routes/ports.js@dev <https://github.com/KomodoPlatform/Agama/blob/dev/routes/ports.js>`_
* Add an electrum server for your asset (optional) `pbca26/agama-wallet-lib:src/electrum-servers.js@dev#L1 <https://github.com/pbca26/agama-wallet-lib/blob/dev/src/electrum-servers.js#L1>`_
* Add a fixed fee for your asset (required if you submit electrum servers list) `pbca26/agama-wallet-lib:src/fees.js@dev#L1 <https://github.com/pbca26/agama-wallet-lib/blob/dev/src/fees.js#L1>`_
* Add an asset chain to the list of kmd assets `pbca26/agama-wallet-lib:src/coin-helpers.js@dev#L1 <https://github.com/pbca26/agama-wallet-lib/blob/dev/src/coin-helpers.js#L1>`_
*  Add asset chain params to this file `KomodoPlatform/Agama:routes/chainParams.js@dev <https://github.com/KomodoPlatform/Agama/blob/dev/routes/chainParams.js>`_
* Submit a `PR <https://github.com/KomodoPlatform/Agama>`_

## Asset chains with block rewards (optional)

* Add ``genproclimit: true`` property to allow mining with multiple CPU threads. Default value is 0 (e.g. -gen -genproclimit=0) in case genproclimit option is not explicitly specified. `KomodoPlatform/Agama:routes/chainParams.js@dev <https://github.com/KomodoPlatform/Agama/blob/dev/routes/chainParams.js>`_

## UI:

* Drop a 100 x 100 px (better 200 x 200 px) logo into `KomodoPlatform/EasyDEX-GUI:react/src/assets/images/cryptologo@dev <https://github.com/KomodoPlatform/EasyDEX-GUI/tree/dev/react/src/assets/images/cryptologo>`_
* Add an asset chain explorer `pbca26/agama-wallet-lib:src/coin-helpers.js@dev#L51 <https://github.com/pbca26/agama-wallet-lib/blob/dev/src/coin-helpers.js#L51>`_
* Add asset chain name to EN translation file [https://github.com/KomodoPlatform/EasyDEX-GUI/blob/dev/react/src/translate/en.js] (`KomodoPlatform/EasyDEX-GUI:react/src/translate/en.js@dev <https://github.com/KomodoPlatform/EasyDEX-GUI/blob/dev/react/src/translate/en.js>`_), look for ``ASSETCHAINS``. 
* Submit a `PR <https://github.com/KomodoPlatform/Agama>`_ to ``dev`` branch on each repo.

Please make sure an asset chain is working in Agama before making a commit. Pull requests containing partial information or not working assets/servers will remain unmerged until all requirements are fulfilled.

## PR List for enabling BarterDEX trading
In order for the coin to be enabled in BarterDEX trading platform you need to submit a PR to [https://github.com/jl777/coins](https://github.com/jl777/coins) repo. Here is an useful guide for the process [https://docs.komodoplatform.com/barterDEX/add-coin-barterDEX.html](https://docs.komodoplatform.com/barterDEX/add-coin-barterDEX.html).

Requirements:
1. Logo (icon) - [https://github.com/jl777/coins/blob/master/icons/zex.png](https://github.com/jl777/coins/blob/master/icons/zex.png)  
2. Explorer - [https://github.com/jl777/coins/blob/master/explorers/ZEX](https://github.com/jl777/coins/blob/master/explorers/ZEX)  
3. Coin info - [https://github.com/jl777/coins/blob/master/coins#L2789](https://github.com/jl777/coins/blob/master/coins#L2789)  
4. Electrum servers (BEER as example)- [https://github.com/jl777/coins/blob/master/electrums/BEER](https://github.com/jl777/coins/blob/master/electrums/BEER)  

**Note: If you can't do it all by yourself, there are 3rd party services (Chainmakers & Chainzilla) available who can do everything for you. Please reach them out using [Komodo Discord](https://komodoplatform.com/discord) or use the [Komodo Platform Website](http://komodoplatform.com/blockchain-starter-kit/#service-provider).**