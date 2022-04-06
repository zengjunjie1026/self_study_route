root@pve:~# cat /etc/pve/qemu-server/116.conf
agent: 1
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
bios: ovmf
boot: order=virtio0;ide2;net0;ide0
cores: 8
cpu: Penryn
efidisk0: local-lvm:vm-116-disk-1,efitype=4m,size=4M
ide0: local:iso/Monterey-recovery.img,size=3141236K
ide2: local:iso/OpenCore-v15.iso,cache=unsafe
machine: q35
memory: 32768
meta: creation-qemu=6.1.0,ctime=1648655483
name: macos
net0: virtio=E2:57:D0:B3:FE:90,bridge=vmbr0,firewall=1
numa: 1
ostype: other
scsihw: virtio-scsi-pci
smbios1: uuid=0200069c-1c81-4c10-a1d4-be601e04c606
sockets: 1
vga: vmware
virtio0: local-lvm:vm-116-disk-0,cache=unsafe,size=1000G
vmgenid: 13ff400c-14df-49d2-8d4c-65a6fb9b0db1