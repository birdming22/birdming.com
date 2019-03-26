

# Wireshark

## Note

* wireshark 1.10+ need gtk3

## Get Source

    git clone https://code.wireshark.org/review/wireshark

## Prepare

For Ubuntu

    sudo apt-get install bison flex libgtk2.0-dev libglib2.0-dev libpcap-dev automake autoconf libtool

Wireshark 1.10+

    sudo apt-get install libgtk3-dev

or 

    sudo apt-get install libgtk-3-dev qt-sdk

## Install

    sh autogen.sh
    ./configure
    make
    sudo make install
    sudo ldconfig -v
