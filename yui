cd /tmp/upg
umount /mnt/img

sleep 20
umount ${lodev}p1
umount ${lodev}p2
e2fsck -yf ${lodev}p2 || true
resize2fs ${lodev}p2

losetup -d $lodev
echo -e '\e[92m正在打包...\e[0m'
echo -e '\e[92m开始写入，请勿中断...\e[0m'
if [ -f FriendlyWrt.img ]; then
	echo 1 > /proc/sys/kernel/sysrq
	echo u > /proc/sysrq-trigger && umount / || true
	#pv FriendlyWrt.img | dd of=/dev/mmcblk0 conv=fsync
	../ddnz FriendlyWrt.img /dev/mmcblk0
	echo -e '\e[92m刷机完毕，正在重启...\e[0m'
	echo b > /proc/sysrq-trigger
fi
