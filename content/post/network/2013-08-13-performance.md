
# Network Performance

## ipef
ref. 

* [iperf 2.x](http://sourceforge.net/projects/iperf/)
* [xjperf](http://code.google.com/p/xjperf/)
* [iperf 3](http://code.google.com/p/iperf/)

### Installation for ubuntu

    sudo apt-get install iperf

### Usage
ref.

* [openmaniak iperf tutorial](http://openmaniak.com/iperf.php)
* [Multiple Instances of iperf in Linux](http://sandilands.info/sgordon/multiple-iperf-instances)

* Server Side

        iperf -s -i 1 -B 192.168.1.1 -p 12345

* Client Side

        iperf -c 192.168.1.1 -p 12345 -i 1 -t 10

* Help

        -l length of buffer to read or write (每個封包的大小)
        -u use UDP rather than TCP (使用 UDP 傳輸協定)

## Reference

* [High Performance Browser Networking](http://chimera.labs.oreilly.com/books/1230000000545/index.html)