# centos安装过程经验
# 使用u盘安装须知
* 查看自己u盘
选择第一个选项，按e进入编辑模式，把：“ linuxefi /images/pxeboot/vmlinuz inst.stage2=hd:LABEL=CentOS\x207\x20x86_64 quiet”  自己 改为：“ linuxefi /images/pxdboot/vmlinuz linux dd quiet” ，如图所示，在按ctrl + x 键
* 更改u盘号
  linuxefi /images/pxeboot/vmlinuz inst.stage2=hd:LABEL=CentOS\x207\x20x86_64 quiet  改为：linuxefi /images/pxeboot/vmlinuz inst.stage2=hd:/dev/sdc4 quiet(我的u盘号是sdc4）
 * 安装过程中出现"X startup failed , falling back to text mode"而不加载
 原因在于显卡不兼容
 解决方法：增加"nomodeset"
 例：linuxefi /images/pxeboot/vmlinuz inst.stage2=hd:/dev/sdc4 nomodeset quiet
 * 磁盘分区中注意自己的磁盘选择，放在误删数据
