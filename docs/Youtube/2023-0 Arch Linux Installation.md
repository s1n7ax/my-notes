# What is Arch Linux

A Linux distribution that is,
1. Highly customizable
2. Lightweight
3. DIY
4. Rolling release

---

# Why Arch Linux

1. Because you can flex on internet
2. Privilege to say "BTW I use Arch"
3. To learn how Linux distributions work
4. Latest and the greatest software
5. AUR

---

# UEFI vs BIOS

These are types of firmware in your mother board

| UEFI                                       	| BIOS                                                     	|
|--------------------------------------------	|----------------------------------------------------------	|
| New                                        	| Old                                                      	|
| GUID Partition Table                       	| MBR Partition Table                                      	|
| 9 Zettabytes of storage (9 × 10^9 TB)      	| 2TB-16TB (with Advanced Format) of storage               	|
| 128 Primary partitions                     	| 4 Primary partitions                                     	|
| Fast                                       	| Slow                                                     	|
| Graphical interface with mouse support     	| Text based interface                                     	|
| Support UEFI & BIOS Legacy boot modes      	| BIOS only                                                	|
| EFI system partition is used to store data 	| First sector of storage device is used to store the data 	|

---

# Changing MBR to GPT

- Change from Legacy boot mode (BIOS) to UEFI in firmware (You will **NOT** be able to boot to existing OSes after this) 
- Change the partition table from scratch to be GPT (data will be **ERASED**)
- [Converting MBR to GPT](https://wiki.archlinux.org/title/GPT_fdisk#Convert_between_MBR_and_GPT)

---

# Dual Booting

- Create a partition for new Arch Linux system beforehand if a dedicated storage drive is not available

---

# Pre-requisites

- Internet connection
- Pen drive 4GB