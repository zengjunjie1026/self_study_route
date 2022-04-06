下载Ubuntu 18.04 LXC模板：
创建LXC容器：


ubuntu更新源：
sudo nano /etc/apt/sources.list

deb http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ bionic-backports main restricted universe multiverse

sudo apt-get update
sudo apt-get upgrade -y
apt install git qemu-utils make -y
git clone https://github.com/thenickdude/OSX-KVM.git
cd /root/OSX-KVM/scripts/monterey
make Monterey-recovery.img

拖文件：
pct pull 100 /root/OSX-KVM/scripts/monterey/Monterey-recovery.img /var/lib/vz/template/iso/Monterey-recovery.img

ISO位置：
cd /var/lib/vz/template/iso/
wget https://github.com/thenickdude/KVM-Opencore/releases/download/v15/OpenCore-v15.iso.gz
gzip -d OpenCore-v15.iso.gz

避免循环引导：
echo "options kvm ignore_msrs=Y" >> /etc/modprobe.d/kvm.conf && update-initramfs -k all -u


创建VM
1、操作系统：
类别：other
ISO镜像：opencore
2、系统
显卡：Vmware兼容
Qemu代理：勾选
BIOS：UEFI
机器：q35
3、硬盘：
总线：VirtIO
缓存：Write Back（不安全）

4、CPU
核心数：2的次幂
类型：penryn
Numa启用

5、网络
模型：virtIO

添加虚拟机安装盘


VM配置地址：
nano /etc/pve/qemu-server/101.conf

修改配置：
1、添加恢复镜像

2、添加参数：
intel:   args: -device isa-applesmc,osk="这里得自己找~" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
AMD:  args: -device isa-applesmc,osk="这里得自己找~" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -global ICH9-LPC.acpi-pci-hotplug-with-bridge-support=off -cpu Penryn,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc,+pcid,+ssse3,+sse4.2,+popcnt,+avx,+avx2,+aes,+fma,+fma4,+bmi1,+bmi2,+xsave,+xsaveopt,check

3、修改光驱属性


启动修改：
diskutil list
sudo dd if=/dev/dsikxxxx of=/dev/diskxxx