



# Kernel Module

## Checksumming
ref.

* [Writing Netﬁlter modules](http://inai.de/documents/Netfilter_Modules.pdf)
* [Cisco與Linux的NAT-Linux實現Cisco風格的NAT](http://blog.csdn.net/dog250/article/details/8936766)

### re-calculate checksum

    #include <net/tcp.h>
    
    struct iphdr *iph;
    struct tcphdr *tcph;

    iph = ip_hdr(skb);
    tcph = (struct tcphdr *)(skb->data + iph->ihl * 4);
    tcplen = (skb->len - (ip_header->ihl << 2));
        
    /* change source ip */
    iph->saddr = newip;

    /* re-calculte tcp checksum */
    tcph->check = 0; 
    tcph->check = tcp_v4_check(tcph, tcplen, 
            iph->saddr, iph->daddr, 
            csum_partial((char *)tcph, tcplen, 0)); 

    /* re-calculte ip checksum */
    ip_send_check(iph);

### update checksum
ps. this code is strange slow at ubuntu 10.04 (kernel 2.6.32)

    struct iphdr *iph;
    struct tcphdr *tcph;

    iph = ip_hdr(skb);
    tcph = (struct tcphdr *)(skb->data + iph->ihl * 4);
        
    oldip = iph->saddr;
        
    /* update ip checksum */
    csum_replace4(&iph->check, iph->saddr, new_addr);
        
    /* update tcp checksum */
    inet_proto_csum_replace4(&tcph->check, skb, oldip, newip, true);

    /* change source ip */
    iph->saddr = newip;

## CONFIG_X86_X32 enabled but no binutils support
ref. [Compiling error while installing Realtek RTL8111E in 64 bit 13.10. CONFIG_X86_X32 enabled but no binutils support](http://askubuntu.com/questions/367838/compiling-error-while-installing-realtek-rtl8111e-in-64-bit-13-10-config-x86-x)

It seems that one shouldn't have spaces in the folder names

## Memory Leak Detection

### KEDR

Download source 0.5 from [offical site](https://github.com/euspectre/kedr)

Install

        tar jxvf kedr-0.5.tar.bz2
        mkdir kedr-build
        cd kedr-build
        cmake ../kedr-0.5
        make
        sudo make install

#### KEDR Usage
Start kedr
    
        sudo kedr start my_module -f leak_check.conf
            
 Load kernel module
    
        sudo insmod my_module.ko
            
  Stop kedr and see result
    
        sudo kedr stop
        dmesg

## Unknown Symbol
Unknown symbol ip_route_output_flow (err 0)

    cat /proc/kallsyms |grep ip_route_output_flow
    0000000000000000 T ip_route_output_flow
    0000000000000000 r __ksymtab_ip_route_output_flow
    0000000000000000 r __kcrctab_ip_route_output_flow
    0000000000000000 r __kstrtab_ip_route_output_flow

add

    MODULE_LICENSE("GPL");

## Reference

## compile kernel
http://www.ubuntu-tw.org/modules/newbb/viewtopic.php?post_id=172030
https://help.ubuntu.com/community/Kernel/Compile
https://wiki.ubuntu.com/KernelTeam/GitKernelBuild
http://www.codewhirl.com/2012/04/how-to-compile-a-single-module-in-ubuntu-linux/
http://mitchtech.net/compile-linux-kernel-on-ubuntu-12-04-lts-detailed/

## build kernel
http://thegeekrising.blogspot.tw/2012/08/module-hack.html

## kernel module
[“Hello World” Loadable Kernel Module](http://blog.markloiseau.com/2012/04/hello-world-loadable-kernel-module-tutorial/)
