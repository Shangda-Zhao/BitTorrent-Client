# Introduction
I built this BitTorrent Client __from scratch__ using __C++__, which is a peer-to-peer protocol for downloading and distributing files across the Internet. The general steps were as follows:

(1) Used C++ Bencoding Library to parse torrent files to get peers who own the data; and then use C++ CPR Library to send an HTTP GET request to Tracker that stores information of downloader (uploader), to know the information of peer.

(2) Used __Socket Programming__ to build a TCP connection with a peer and then send handshake messages to make sure that the peer uses the same BitTorrent protocol and whether it has what our client wants.

(3) Used PieceManager to __manage__ pieces which is part of the __desired document__.

(4) Put all discovered peers into a __thread-safe queue__, and each thread gets the peer from this queue and continues to run until the end of the file download.

I have achieved excellent output: with eight threads, the download speed is __1.14 MB/s__ when the network connection is good.

# How to use
If you want to try this project, follow the following steps:

(1) Clone this repository, and install cmake  

(2) Run the following commands in the terminal:

    $ cd BitTorrentClient 

    $ mkdir build 
       
    $ cd build

    $ cmake .. && make -j

(3) To download the ubuntu iso as an example, enter the following command:

    $ ./BitTorrentClient -t ../res/ubuntu-12.04.5-alternate-amd64.iso.torrent -o ../res/  # logging disabled
    
    $ ./BitTorrentClient -t ../res/ubuntu-12.04.5-alternate-amd64.iso.torrent -o ../res/  -l # logging enabled, log can be found in logs/client.log
___Note:___ the Command Description

    -t: Path to the Torrent file
    
    -o: The output directory where the file will be downloaded
    
    -n: Number of downloading threads to use
    
    -l: Enable logging
    
All files in the ``res`` directory can be used for testing. 
