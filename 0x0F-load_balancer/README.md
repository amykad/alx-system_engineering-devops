0x0F. Load balancer project solutions

Installing HAProxy and configuring HAProxy

 sudo apt-get install -y haproxy=1.6.\*

$ sudo vi /etc/haproxy/haproxy.cfg
# Add the below code to the file opened using vi editor
frontend sammykingx.tech
        bind 0:80
	mode http
        default_backend web_servers

backend web_servers
        balance roundrobin
        server 64820-web-01 100.26.152.157:80
        server 64820-web-02 52.86.102.6:80
~
~
:wq(to save and exit)
--------------- or ----------------------- 
$ echo '
frontend sammykingx.tech
        bind 0:80
	mode http
        default_backend web_servers

backend web_servers
        balance roundrobin
        server 64820-web-01 100.26.152.157:80
        server 64820-web-02 52.86.102.6:80
' >> /etc/haproxy/haproxy.cfg

$ service haproxy restart

# git clone this repo on your terminal and run the file
# install_haproxy_safely or 1-install_load_balancer to 
# configure yours on a fly.
