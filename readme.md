# Install ShadowSocksR Plus plugin on GL-iNet GL-SFT1200 router

## Install SSRP plugin based on official firmware version 3.206

## Referenced and extracted from the following websites:
- Official firmware download address：https://dl.gl-inet.cn/?model=sft1200
- If the space is not enough, please refer to OpenWRT expansion overlay [pointing Overlay space to external storage](https://blog.digicat-studio.com/Technology/openwrt_overlay.html)
- [GL-SFT1200 official firmware one-click installation magic Internet access](https://www.126126.xyz/post/031/#%E5%8E%9F%E5%8E%82%E7%B3%BB%E7%BB%9F%E4%B8%80%E9%94%AE%E5%AE%89%E8%A3%85%E9%AD%94%E6%B3%95%E4%B8%8A%E7%BD%91)(PassWall is not very useful in actual testing, so it is not recommended)

## 1. Manual installation method
1.Download the Release compressed package and decompress it using the password: ssrp;

2.Use the winscp tool to upload the plug-in to the /tmp/tmp/ directory of the router;

3.Use "cd /tmp/tmp/" to enter the plugin upload directory;

4.Use the "opkg update && opkg install *.ipk" command to install and wait for the installation to complete;

5.If an error message appears when opening the luci plug-in, continue to use the command "opkg install luci-compat" to install the luci-compat plug-in;

6.Log in to luci again and you will see the plug-in you just installed in the "Service" menu;

## 2. One-click installation method
    wget -qO- https://cdn.jsdelivr.net/gh/ericwang2006/sft1200_buddha/install.sh | sh -s ssr-plus

## 3. Optimization

1.If SSRP cannot be started, please reboot first. If that still does not work, try to modify START=99 in /etc/init.d/shadowsocksr and then reboot.

2.If Taobao is slow to respond, first check the firewall traffic sharing status and execute the following command to disable hardware forwarding acceleration:

    uci show firewall
    .....
    uci set firewall.@defaults[0].flow_offloading='1'
    uci set firewall.@defaults[0].flow_offloading_hw='0'
    uci commit firewall
    service firewall restart

3.Execute the following command to close the real-time speed and traffic statistics program (the close button on the management webpage does not actually close the statistics program) to improve the system load;

    /etc/init.d/gl_tertf stop
    /etc/init.d/gl_tertf disable
    
    如需恢复，执行以下命令：
    /etc/init.d/gl_tertf enable
    /etc/init.d/gl_tertf start
