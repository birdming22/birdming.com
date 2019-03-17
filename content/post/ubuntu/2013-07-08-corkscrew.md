
# Corkscrew

## Install

    sudo apt-get install -y corkscrew

## config
ref. [How to use SSH Via HTTP Proxy using Corkscrew in Ubuntu](http://www.ubuntugeek.com/how-to-use-ssh-via-http-proxy-using-corkscrew-in-ubuntu.html)

edit ~/.corkscrew-auth

    username:password

edit ~/.ssh/config

    Host *
        ProxyCommand corkscrew proxyhostname proxyport %h %p /home/username/.corkscrew-auth
