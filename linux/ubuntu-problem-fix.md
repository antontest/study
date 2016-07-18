在终端输入 
sudo gedit /etc/ppp/options 
将弹出的文档中的 lcp-echo-failure 4 (这句在232行) 改为 lcp-echo-failure 30 

lcp-echo-failure次数被设为4,而lcp-echo-interval设为30秒。也就是说，如果120秒钟之
内，ADSL服务器没有给回echo-reply信号，Ubuntu便会认为网络已经出了问题，马上中断重
联，所以……
