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


# NVIDIA安装
<h1 style="text-align: left;"><span style="font-size: 18px;"><strong>1. 禁用nouveau</strong></span></h1>

<div>打开/etc/modprobe.d/blacklist.conf&nbsp; 添加 blacklist nouveau</div><br>
<div>打开 /usr/lib/modprobe.d/dist-blacklist.conf</div>
<div>添加两行：</div>
<br>
<div>blacklist nouveau</div>  
<br>
<div>options nouveau modeset=0</div>
<br>

<h1><span style="font-size: 18px;">重建文件系统</span></h1>
<p>备份原来的initramfs nouveau image镜像&nbsp;&nbsp;<span class="cnblogs_code"><span style="color: #0000ff;">mv</span> /boot/initramfs-$(<span style="color: #0000ff;">uname</span> -r).img /boot/initramfs-$(<span style="color: #0000ff;">uname</span> -r)-nouveau.img</span>&nbsp;</p>
<div>重建文件系统&nbsp;&nbsp;<span class="cnblogs_code">dracut /boot/initramfs-$(<span style="color: #0000ff;">uname</span> -r).img $(<span style="color: #0000ff;">uname</span> -r)</span>&nbsp;</div>
<div>&nbsp;</div>
<h1><span style="font-size: 18px;">安装dkms</span></h1>
<div class="cnblogs_code">
<pre><span style="color: #008080;">1</span> <span style="color: #0000ff;">sudo</span> <span style="color: #0000ff;">yum</span> <span style="color: #0000ff;">install</span> kernel-<span style="color: #000000;">devel 
</span><span style="color: #008080;">2</span> <span style="color: #0000ff;">sudo</span> <span style="color: #0000ff;">yum</span> -y <span style="color: #0000ff;">install</span> epel-<span style="color: #000000;">release 
</span><span style="color: #008080;">3</span> <span style="color: #0000ff;">sudo</span> <span style="color: #0000ff;">yum</span> -y <span style="color: #0000ff;">install</span> dkms </pre>
</div>

<br>
<h1><span style="font-size: 16px;">重启安装NVIDIA驱动</span></h1>
<div>&nbsp;<span class="cnblogs_code">./NVIDIA-Linux-x86_64-<span style="color: #800080;">384.90</span>-1080ti.run</span>&nbsp;</div>
<h1>&nbsp;</h1>
