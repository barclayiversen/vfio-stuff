# youtube links

https://www.youtube.com/watch?v=g--fe8_kEcw

https://www.youtube.com/playlist?list=PLG7vUqRxMOG6gsPXohhFht3UJbcCxYgcL

# hardware explorers

cpuid

hwinfo

# optimizing

https://angrysysadmins.tech/index.php/2022/07/grassyloki/vfio-tuning-your-windows-gaming-vm-for-optimal-performance/

# configure custom qemu builds
qemu doesn't build with usb support by default when compiling from source (wtf?) so it must be specified. 

./configure --prefix=/opt/qemu-custom --target-list=x86_64-softmmu --enable-libusb --enable-usb-redir
