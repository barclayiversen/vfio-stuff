# youtube links

https://www.youtube.com/watch?v=g--fe8_kEcw

https://www.youtube.com/playlist?list=PLG7vUqRxMOG6gsPXohhFht3UJbcCxYgcL

https://www.youtube.com/watch?v=n463QJ4cjsU --building a kernel driver. Useful info in here about setting up a system for kernel development. 

# hardware explorers

cpuid

hwinfo

# vm detection tools

VMaware
paranoid fish
msr-cmd

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


# Not totally VFIO related but....

I set up my windows guest with vmware player to run another VM inside my VM (nested virtualization). I did this so I could have a VM to run my first kernel driver in since I needed a windows "host" (my level 1 windows guest) to write my code and a windows guest (my level 2 VM) to test the kernel driver.

What I didn't know at the time was that when I enabled debug in my system configuration (msconfig.exe in the boot tab) that it would cause VMProtect to go completely nuclear on my system if I tried to start it. 

VMProtect protects itself by crashing your system as an anti debug measure if you have debug enabled in msconfig. 