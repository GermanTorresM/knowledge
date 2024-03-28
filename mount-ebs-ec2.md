lsblk

mkfs -t ext4 /dev/nvme1n1

Create folder

mkdir -p /mnt/nvar

Mount the volume to folder

mount /dev/nvme1n1 /mnt/nvar

df -khT


#copy original /var to /dev/xvdj
mkdir /mnt/new
mount /dev/xvdj /mnt/new
cd /var
cp -Rax * /mnt/new
cd /
mv var var.old
#mount EBS as new /var
umount /dev/xvdj
mkdir /var
mount /dev/xvdj /var

blkid

root@ip-10-0-62-202:~# blkid
/dev/nvme1n1: UUID="a005a1e5-bcde-4460-a065-cdd8fcb585b4" TYPE="ext4"
/dev/nvme2n1: UUID="146c727a-99e5-4b20-bf1f-0cd25de764d4" TYPE="ext4"
/dev/nvme0n1p1: LABEL="cloudimg-rootfs" UUID="9cf7073a-6786-43dc-895e-8bbebe712a1e" TYPE="ext4" PARTUUID="f8d1fa9f-182a-450e-af39-225ba2d429f6"
/dev/nvme0n1p15: LABEL="UEFI" UUID="DF7C-28A1" TYPE="vfat" PARTUUID="3cb70898-43f7-4253-aaed-549418eae0a4"
/dev/nvme0n1: PTUUID="e9e9eac1-9ebe-4a02-b414-fa3991929d2c" PTTYPE="gpt"
/dev/nvme0n1p14: PARTUUID="c731059e-fda1-4a53-8025-9215aa2e77eb"
root@ip-10-0-62-202:~# 


lsblk -o +UUID

root@ip-10-0-62-202:~# lsblk -o +UUID
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT UUID
nvme1n1      259:0    0    30G  0 disk            a005a1e5-bcde-4460-a065-cdd8fcb585b4
nvme3n1      259:1    0 209.6G  0 disk            
nvme2n1      259:2    0   100G  0 disk            146c727a-99e5-4b20-bf1f-0cd25de764d4
nvme0n1      259:3    0    10G  0 disk            
├─nvme0n1p1  259:4    0   9.9G  0 part /          9cf7073a-6786-43dc-895e-8bbebe712a1e
├─nvme0n1p14 259:5    0     4M  0 part            
└─nvme0n1p15 259:6    0   106M  0 part /boot/efi  DF7C-28A1
root@ip-10-0-62-202:~#

/dev/nvme1n1: UUID="a005a1e5-bcde-4460-a065-cdd8fcb585b4" TYPE="ext4"
/dev/nvme2n1: UUID="146c727a-99e5-4b20-bf1f-0cd25de764d4" TYPE="ext4"

sudo lsblk -o +UUID

UUID=a005a1e5-bcde-4460-a065-cdd8fcb585b4 /opt ext4 defaults,nofail  0  2

UUID=146c727a-99e5-4b20-bf1f-0cd25de764d4 /var ext4 defaults,nofail  0  2


sudo vi /etc/fstab

resize2fs /dev/xvda1




umount /dev/xvdg

umount /dev/xvdi

mount /dev/xvdi /var

sudo lsblk -o +UUID


lsof /dev/xvdg