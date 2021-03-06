## What is this?

This repo was a **unofficial** MediaTek feeds for [OpenWrt](https://openwrt.org "OpenWrt") or [Lede](https://lede-project.org). This project is experimental, and technical support will be limited.

In OpenWrt/Lede, a [feeds](https://wiki.openwrt.org/doc/devel/feeds "feeds") is collection of software components (applications, libraries, kernel-modules, ...) that you can integrate into your OpenWrt/Lede system.

## How can I use them?

I assume that you already have a working OpenWrt/Lede workspace, then add the following line into "feeds.conf.default" (You will find it under the top dir of your workspace).

    src-git mtk https://github.com/Nossiac/mtk-openwrt-feeds;lede-17.01

then execute:

	scripts/feeds update -f mtk
	scripts/feeds install -a -p mtk

Now you will be able to see extra packages via `make menuconfig`. All packages from this feeds are located under `MTK Properties`.

## What do we have here?

### mt7620/mt7610/mt7612/mt7628/mt7603/mt7615

These are prebuilt WiFi modules for OpenWrt/Lede.

The following drivers are planned :

* mt7620 (done)
* mt7628 (done)
* mt7610 (done)
* mt7612 (todo)
* mt7603 (todo)
* mt7615 (todo)

Currently I only build them with latest stable branch of lede.

### uci2dat

An application that translates "/etc/config/wireless" into MTK's WiFi profiles (e.g. mt7620.dat). You may use it as an adapter to make MTK's WiFi drivers work with standard LuCi's WiFi management.

### mtk-nvram

The term "nvram" in MTK's software means a raw storage scheme on flash chips. It access flash device in raw mode (without filesystem). 

All data stored in nvram partition are "<Key>=[Value]" pairs. It usually resides in mtd partition "config". 

Note： OpenWrt/Lede has replaced nvram scheme with [uci](https://wiki.openwrt.org/doc/uci) long ago. I keep this for back compatibility only. 

### mtk-luci-plugin

This is a plugin for LuCI web interface, which manipulate MTK's proprietary drivers by reading/writing its profile directly. It does not use uci, so "/etc/config/wireless" is left untouched.

To use this, you should install LuCI first:

	scripts/feeds update
	scripts/feeds install luci

Also we have a small tool called "web console" along with the plugin, it exposes root shell to the web interface, and sometimes you may need it. 

## Technical support? 

I do this in my spare time, so I cannot promise too much. Anyway, you are welcome to feedback any issues/bugs/suggestions/patches here. That would be helpful for MTK to improve what they are doing.


