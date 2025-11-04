
bruteforcing disk

acky is not very knowledgable about the best security passwords and used a simple password to encrypt their BitLocker drive. See if you can break through the encryption!
Download the disk image

```
❯ fdisk -l bitlocker-1.dd                                                                                                                                         
Disk bitlocker-1.dd: 100 MiB, 104857600 bytes, 204800 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x78787878

Device          Boot      Start        End    Sectors   Size Id Type
bitlocker-1.dd1      2021161080 4042322159 2021161080 963.8G 78 unknown
bitlocker-1.dd2      2021161080 4042322159 2021161080 963.8G 78 unknown
bitlocker-1.dd3      4294932600 8589899894 4294967295     2T 78 unknown
bitlocker-1.dd4      4294967295 5035196669  740229375   353G ff BBT

```

create hash
`bitlocker2john -i bitlocker-1.dd > bitlocker_hash.txt`

dictionary attack
`hashcat -m 22100 -a 0 bitlocker_hash.txt /usr/share/wordlist/rockyou.txt -w 3`

recover
`mkdir bitlocker1`
`sudo dislocker bitlocker-1.dd -ujacqueline dislocker`

open
`sudo mount -o loop disk/dislocker-file mounted`
