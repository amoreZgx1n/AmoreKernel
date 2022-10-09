# Realize a operation kernel

## Initialize the Environment



### Install the unbutu

...

### Install the bochs

On the unbutu platform, we can just use the command to install

```
sudo apt install bochs
```

Also some dependent packages are required, and you can install it by the error information. I all install them by `apt`. If you unluckily can't install bochs by the command, you can download the compiled package from the official website. 

### Run the bochs

To new a virtual machine, we just need two things: a configure file and a image. And here is the configure file **bochsrc.txt**  :

 ```
 # RAM size
 megs: 32
 # Change to your Bochs installation path
 romimage: file=/usr/share/bochs/BIOS-bochs-latest
 vgaromimage: file=/usr/share/bochs/VGABIOS-lgpl-latest
 
 # Disk
 boot: disk
 ata0: enabled=1, ioaddr1=0x01f0, ioaddr2=0x03f0, irq=14
 ata0-master: type=disk, path="amoroll.img", mode=flat, cylinders=6, heads=16, spt=63
 
 log: bochsout.txt
 
 mouse: enabled=0
 keyboard:  keymap=/usr/share/bochs/keymaps/x11-pc-us.map
 clock: sync=realtime
 cpu: model=core2_penryn_t9600, count=1, ips=50000000, reset_on_triple_fault=1
 ```

You can see the function of the configure file. And when a long time has passed, many usages above may deprecate. Just coming to official document or forum.

About the configure(review the computer knowledge)

- 



Then it is time to make a kernel image file. Bochs has a command tool to make image. Just input the `bximage` to realize it. Then you will make some choices. You can follow the suggested choices(such as [10]). Here are part of the choices:

``` 
amore@amore-VirtualBox:~$ bximage
========================================================================
                                bximage
  Disk Image Creation / Conversion / Resize and Commit Tool for Bochs
         $Id: bximage.cc 13481 2018-03-30 21:04:04Z vruppert $
========================================================================

1. Create new floppy or hard disk image
2. Convert hard disk image to other format (mode)
3. Resize hard disk image
4. Commit 'undoable' redolog to base image
5. Disk image info

0. Quit

Please choose one [0] 
```

At the end, we initiate the bochs machine by `bochs -f bochsrc.txt`(-f refers to initiate by the configure file). You can see the windows:



The tree of directory:

├── amoroll.img
├── amoroll.img.lock
├── bochsout.txt
└── bochsrc.txt