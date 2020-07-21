# Stock enviroment

baudrate=115200

bootargs=

bootcmd=for dtype in sata mmc usb ; do for disk in 0 1 ; do ${dtype} dev ${disk} ;for fs in fat ext2 ; do ${fs}load ${dtype} ${disk}:1 10008000 /6x_bootscript&& source 10008000 ; done ; done ; done; setenv stdout serial,vga ; echo ; echo 6x_bootscript not found ; echo ; echo serial console at 115200, 8N1 ; echo ; echo details at http://boundarydevices.com/6q_bootscript ; setenv stdout serial

bootdelay=3

clearenv=if sf probe || sf probe ; then sf erase 0xc0000 0x2000 && echo restored environment to factory default ; fi

cmd_hdmi=fdt set fb_hdmi status okay;fdt set fb_hdmi mode_str 1280x720M@60;

cmd_lvds=fdt set fb_lvds status disabled;fdt set ldb/lvds-channel@0 status disabled

console=ttymxc1

dfu_alt_info=u-boot raw 0x0 0xc0000

dtbname=imx6qd-adk.dtb

ethact=FEC

ethprime=FEC

fb_hdmi_name=1280x720M@60

fdt_addr=13000000

fdt_high=0xffffffff

fileaddr=10008000

filesize=c1f

fuse1=0 5

fuse1_val=18000030

fuse2=0 6

fuse2_val=00000010

fuse_mac1a=4 3

fuse_mac1a_val=00000019

fuse_mac1b=4 2

initrd_high=0xffffffff

loadaddr=0x12000000

loadsplash=if sf probe ; then sf read ${splashimage} ${splashflash} ${splashsize} ; fi

net_fuses=dhcp 10008000 prog_fuses.scr && source 10008000

net_program=next=prog_fuses.scr; run net_upgradeu

net_upgradeu=dhcp 10008000 net_upgradeu.scr && source 10008000

otg_fuses=run usbnetwork; tftp 10008000 prog_fuses.scr && source 10008000

otg_program=next=prog_fuses.scr; run otg_upgradeu

otg_upgradeu=run usbnetwork; tftp 10008000 net_upgradeu.scr && source 10008000

program=next=prog_fuses.scr; run upgradeu

rundfu=dfu 0 sf 0:0:25000000:0

scriptaddr=10008000

sfname=sst25vf016b

splashflash=c2000

stdout=serial

uboot_defconfig=imx6q-adk

upgradeu=for dtype in sata mmc usb ; do for disk in 0 1 ; do ${dtype} dev ${disk} ;for fs in fat ext2 ; do ${fs}load ${dtype} ${disk}:1 10008000 /6x_upgrade && source 10008000 ; done ; done ; done

usb_pgood_delay=2000

usbnet_devaddr=00:19:b8:00:00:02

usbnet_hostaddr=00:19:b8:00:00:01

usbnetwork=setenv ethact usb_ether; setenv ipaddr 10.0.0.2; setenv netmask 255.255.255.0; setenv serverip 10.0.0.1;

usbrecover=run usbnetwork;setenv bootargs console=${console},115200; tftpboot 10800000 10.0.0.1:uImage-${board}-recovery && tftpboot 12800000 10.0.0.1:uramdisk-${board}-recovery.img && bootm 10800000 12800000

# Extra added enviroment

allow_noncea=1

board=sabrelite

bootdelay=0

bootfile=u-boot.q1g.18.adk.imx

dtbname=imx6q-sabrelite.dtb

fb_hdmi=boe:24:68152388,1920,720,5,63,2,39,1,1

# Fix for - Error: FEC address not set

setenv netdev eth0

setenv ethprime FEC0

setenv ethact FEC0

setenv ethaddr 00:01:02:03:04:05

setenv fec_addr 00:01:02:03:04:05

setenv ipaddr 192.168.0.150

setenv serverip 192.168.0.86

setenv gatewayip 192.168.0.1

saveenv
