https://openwrt.org/toh/xiaomi/nano
Download the Official Developer ROM.
Visit http://192.168.31.1, login and manually upgrade to the Official Developer ROM. Ignore any warning regarding downgrading.
Wait for 5-7 minutes. After the router is back on again, you need to set a root password to be able to log in. Login to the router and copy the “stok” but from the address bar. Open up a shell and,
curl -d "oldPwd=your_admin_pass&newPwd=desired_root_pass" "http://192.168.31.1/cgi-bin/luci/;stok=<stok from browser url>/api/xqsystem/set_name_password"
Now you should get a code 0 response if everything went okay. Let's login.
ssh root@192.168.31.1


启用路由器SSH登录
sed -i ":x;N;s/if \[.*\; then\n.*return 0\n.*fi/#tb/;b x" /etc/init.d/dropbear
/etc/init.d/dropbear start
nvram set ssh_en=1; nvram commit

刷入Breed固件
mtd -r write /tmp/breed.bin Bootloader

进入breed控制台
拔掉路由器电源，使路由关机，用取卡针或者其他尖锐物戳着reset键，然后插上电源，待路由器后方的网络接口灯闪烁时松开reset键即可，然后用一条网线把电脑和路由器的WAN口相连，打开浏览器访问192.168.1.1，即可进入breed控制台。进入后即可开始对路由器进行刷机。


刷入潘多拉固件
推荐使用Padavan固件，固件发布地址：http://opt.cn2qq.com/padavan/（注意：小米路由器青春版请选择MI-NANO专版，目前最新版固件名称如下：MI-NANO_3.4.3.9-099.trx）。

潘多拉网关
192.168.123.1  http://my.router/  admin admin

