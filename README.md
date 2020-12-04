# uTip Coin Source Code
uTipcoin is a PoS-based cryptocurrency.



#### Compile uTip Daemon for Raspberry Pi 4 with Ubuntu Server 20.04 (64bit)
**Step 1. Install required dependencies**
```sh
$ sudo apt-get -y install git automake build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev libcrypto++-dev libevent-dev libminiupnpc-dev libgmp-dev devscripts libdb++-dev libsodium-dev libboost-dev libboost-chrono-dev libboost-filesystem-dev libboost-program-options-dev libboost-system-dev libboost-test-dev libboost-thread-dev
```

**Step 2. Download and install Berkley DB**
```sh
$ wget http://download.oracle.com/berkeley-db/db-4.8.30.NC.tar.gz
$ tar xzvf db-4.8.30.NC.tar.gz
$ cd db-4.8.30.NC/build_unix/
$ sudo wget -O ../dist/config.guess 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.guess;hb=HEAD'
$ sudo wget -O ../dist/config.sub 'http://git.savannah.gnu.org/gitweb/?p=config.git;a=blob_plain;f=config.sub;hb=HEAD'
$ ../dist/configure --enable-cxx
$ make && sudo make install
$ export BDB_INCLUDE_PATH="/usr/local/BerkeleyDB.4.8/include"
$ export BDB_LIB_PATH="/usr/local/BerkeleyDB.4.8/lib"
$ export CPATH=”/usr/local/BerkeleyDB.4.8/include”
$ export LIBRARY_PATH=”/usr/local/BerkeleyDB.4.8/lib”
$ sudo ln -s /usr/local/BerkeleyDB.4.8/lib/libdb-4.8.so /usr/lib/libdb-4.8.so
$ sudo ln -s /usr/local/BerkeleyDB.4.8/lib/libdb_cxx-4.8.so /usr/lib/libdb_cxx-4.8.so
$ cd
```

**Step 3. Clone and compile the uTip Source Code**
```sh
$ git clone https://github.com/PorkyForky/uTip.git
$ cd uTip/src/leveldb
$ sudo chmod +x build_detect_platform
$ sudo make libleveldb.a libmemenv.a
$ cd ..
$ make -f makefile.unix USE_UPNP=-
$ strip uTipcoind
```
