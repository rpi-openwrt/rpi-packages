rpi-packages
============

This is a package feed for OpenWRT specifically tailored for Raspberry Pi, including some rpi specific tools and extra packages that are supposed to bring OpenWRT on Raspberry Pi to the level with other available Raspberry Pi distributions.

These packages include all kinds of goodies including userland and EGL accelerated Weston..

Depencies
=========
Yes, it's not quite that simple. To get everything working, you need somethings:<br/>
 1) packages feed must be installed<br/>
 2) Some patching has to be done<br/>
 
Patches?
========
Yes, most of them are just updates to "old" not yet updated versions in the openwrt trunk and some or minor enhancements and some are add-ons. All patches are available from here:<br/>
https://github.com/rpi-openwrt/patches<br/>

Or you can download them from OpenWrt Trac one by one and also see the explanation of the patch, list of patches and Trac URLS is provided next.<br/>

Patches from Trac against base system
=====================================
openwrt-populatefs-fixed.patch: https://dev.openwrt.org/raw-attachment/ticket/14770/openwrt-populatefs-fixed.patch<br/>
xorg-macros-upgrade.patch: https://dev.openwrt.org/raw-attachment/ticket/14699/xorg-macros-upgrade.patch<br/>
udev-add-hostbuild.patch: https://dev.openwrt.org/raw-attachment/ticket/15645/udev-add-hostbuild.patch<br/>
lua-add-fpic.patch: https://dev.openwrt.org/raw-attachment/ticket/15647/lua-add-fpic.patch<br/>

Patches from Trac against packages tree
=======================================
diffutils.patch: https://dev.openwrt.org/raw-attachment/ticket/14641/diffutils.patch<br/>
dialog-v2.patch: https://dev.openwrt.org/raw-attachment/ticket/14799/dialog-v2.patch<br/>
dbus.patch: https://dev.openwrt.org/raw-attachment/ticket/15646/dbus.patch<br/>

How to include this package tree in my trunk sources?
=====================================================
If you patched from rpi-openwrt/patches, you should be all set, if not - Add following line to your <b>trunk/feeds.conf.default</b>:<br />
src-git raspberry https://github.com/rpi-openwrt/rpi-packages.git<br/>

And then just use:<br />
 ./scripts/feeds update -a<br/>
 ./scripts/feeds install -a -p raspberry<br/>
 
Hints for compiling?
====================
To get everything working perfect, you should make sure you are using <b>gcc-linaro 4.8.x</b> as your compiler and for binutils version choose <b>linaro</b> version as well. Especially for development environment, this is very crucial step.

Sometimes, there are issues when trying to compile libefl and/or Elementary. Luckily, there's also a fix for that, although, it needs a bit manual labor..<br />This is because everytime, for some reason, everything isn't compiled in the right order.<br/>I got around this issue by noticing the error and then before retrying, I executed following commands:<br/>
 make package/system/udev/host/compile V=99<br/>
 make package/libefl/compile V=99<br/>
 make package/libefl/install V=99<br/>
 
And after this, I again commanded make to build the image and all packages I wanted and everything worked out.
