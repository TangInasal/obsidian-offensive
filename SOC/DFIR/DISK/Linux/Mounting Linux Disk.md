**Pre-requisites:**
1. WSL
2. Disk image (on windows)
3. fdisk (on WSL)

**Steps:**
1. Download the disk image on windows
2. Open WSL
3. Download `fdisk`
		`sudo apt install -y fdisk`
4. check disk image info
		`fdisk -l image.dd`
		![[Pasted image 20251119182444.png]]
5.  Create empty directory to mount the image
		`sudo mkdir /mnt/image`
6.  Identify offset value of the image you want to mount
		`<start offset> * 512 (bytes) = offset_value`
		![[Pasted image 20251119182718.png]]
		
7. Mount disk
		`sudo mount -o ro,loop,offset=<offset_value>,noload <image.dd> /mnt/`