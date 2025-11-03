
Can you find the flag in this disk image? The right one is Linux! One wrong step and its all gone!

`fdisk -l disk.dd`

recover 
```
dd if=disko-2.dd of=part1.img bs=512 skip=2048 count=51200
sudo mkdir /mnt/part1
sudo mount -o loop part1.img /mnt/part1/
```

filter
`strings part1.img | grep -r flag`

