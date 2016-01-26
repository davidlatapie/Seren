


Seren

Copyright (c) 2016 Seren Developers
Copyright (c) 2013-2015 HyperStake Developers -- Press, you already started working on it in 2013? 
Copyright (c) 2013 NovaCoin Developers
Copyright (c) 2011-2012 Bitcoin Developers
Distributed under the MIT/X11 software license, see the accompanying
file license.txt or http://www.opensource.org/licenses/mit-license.php.
This product includes software developed by the OpenSSL Project for use in
the OpenSSL Toolkit (http://www.openssl.org/).  This product includes
cryptographic software written by Eric Young (eay@cryptsoft.com).


Intro
-----
Seren is a free open source project derived from HyperStake, with
the goal of providing a long-term energy-efficient Proof of Stake based crypto-currency.
Built on the foundation of Bitcoin and HyperStake, innovations such as proof-of-stake
help further advance the field of crypto-currency.

About Seren's Fee System
-----
Seren charges a transaction fee based on the amount of coins that is sent to another address. 

* 1% fee for up to 10 coins sent to another address <!-- to be checked: what is the exact fee for exactly 10 coin, because the documentation was blurry before editing (David) -->
* 0.01% fee from the eleventh coin onward sent to another address (first 10 still pay 1%)
* Minimum fee amount of 0.01 coin <!-- this was not included, so must be checked (David) -->
* Maximum fee amount of 1,000 coins

Since typically when sending coins to another address, the sending address does not have exact change, typical crypto-currency implementation will generate a new *change address* which any change is returned to. Since it impossible to determine what is a change address and what is being sent to the receiving party, the fee is calculated on all coins that are sent to an address the address signing the unspent inputs (ie the sending address).

In order to minimize fee's the *sender is encouraged to use the sending address as the change address*. Using QT wallet this is done by selecting the 'return change' button. Using the daemon you can do this by using the return change flag in sendtoaddress. <!-- feature request: have the "return change" option selected by defaut (David) -->

The sending party should beware that *proper handling of the return change code should be taken into an account*, for example an exchange may want to pool all user deposits into an intermediate address in which withdrawals are only sent from that address, and using the return change feature will not accidentally debit any users accounts.

Actual code for this system can be found in GetValueBasedFee() in main.h and GetValueInForValueBasedFee() in main.cpp.


Setup
-----
sudo apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev libdb5.1-dev libdb5.1++-dev libminiupnpc-dev libqrencode-dev automake

 ./autogen.sh

  ./configure --with-incompatible-bdb --with-gui=no

make


to build with QT:

sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools libprotobuf-dev protobuf-compiler

./autogen.sh

./configure --with-incompatible-bdb --with-gui=qt5

make

The software automatically finds other nodes to connect to.  You can
enable Universal Plug and Play (UPnP) with your router/firewall
or forward port 

Upgrade
-------
All you existing coins/transactions should be intact with the upgrade.
To upgrade first backup wallet
serend backupwallet <destination_backup_file>
Then shutdown serend by
serend stop
Start up the new serend.

