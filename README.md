# youtube links

https://www.youtube.com/watch?v=g--fe8_kEcw

https://www.youtube.com/playlist?list=PLG7vUqRxMOG6gsPXohhFht3UJbcCxYgcL

# hardware explorers

cpuid

hwinfo

# optimizing

https://angrysysadmins.tech/index.php/2022/07/grassyloki/vfio-tuning-your-windows-gaming-vm-for-optimal-performance/

-huge pages-

For persistent configuration, add the following line to /etc/sysctl.conf:
vm.nr_hugepages = 8192



# configure custom qemu builds
qemu doesn't build with usb support by default when compiling from source (wtf?) so it must be specified. 

-depends on-

libusb-1.0-0 

-run-

./configure --prefix=/opt/qemu-custom --target-list=x86_64-softmmu --enable-libusb --enable-spice --enable-usb-redir

# Sound

Setting up sound sucks. The easiest thing to do is pass a device through but then you're stuck with having two different sets of speakers for host and guest.

apparently libvirt runs vms as root, and will route audio to the root user pulse audio server. This can supposedly be mitigated with these lines in your xml

    <qemu:env name="QEMU_AUDIO_DRV" value="pa"/>
    <qemu:env name="QEMU_PA_SERVER" value="/run/user/1000/pulse/native"/>

but it didn't work for me. 