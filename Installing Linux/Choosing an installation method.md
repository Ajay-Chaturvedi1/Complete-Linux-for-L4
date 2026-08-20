IN THIS CHAPTER
Choosing an installation method
Installing a single- or multi-boot system
Performing a Live media installation of Fedora
Installing Red Hat Enterprise Linux
Understanding cloud-based installations
Partitioning the disk for installation
Understanding the GRUB boot loader


Installing Linux has become a fairly easy thing to do—if you are starting with a computer that is
up to spec (hard disk, RAM, CPU, and so on) and you don’t mind totally erasing your hard drive.
With cloud computing and virtualization, installation can be even simpler. It allows you to
bypass traditional installation and spin a Linux system up or down within a few minutes by adding
metadata to prebuilt images.

This chapter starts off with a simple installation on a physical computer from Live media and progresses
to more complex installation topics.

To ease you into the subject of installing Linux, I cover three different ways of installing Linux and
step you through each process:

**Installing from Live media**     A Linux Live media ISO is a single, read-only image that contains
everything you need to start a Linux operating system. That image can be burned to a DVD
or USB drive and booted from that medium. With the Live media, you can totally ignore your
computer’s hard disk; in fact, you can run Live media on a system with no hard disk. After
you are running the Live Linux system, some Live media ISOs allow you to launch an application
that permanently installs the contents of the Live medium to your hard disk. The
first installation procedure in this chapter shows you how to install Linux permanently from
a Fedora Live media ISO.

**Installing from an installation DVD**      An installation DVD, available with Fedora,
RHEL, Ubuntu, and other Linux distributions, offers more flexible ways of
installing Linux. In particular, instead of just copying the whole Live media contents
to your computer, with an installation DVD you can choose exactly which
software package you want. The second installation procedure I show in this chapter
steps you through an installation process from a Red Hat Enterprise Linux 8
installation DVD.

**Installing in the enterprise**       Sitting in front of a computer and clicking through
installation questions isn’t inconvenient if you are installing a single system.
But what if you need to install dozens or hundreds of Linux systems? What if
you want to install those systems in particular ways that need to be repeated
over multiple installations? Later in this chapter, I describe efficient ways of
installing multiple Linux systems using network installation features and kickstart
files.

A fourth method of installation not covered in this chapter is to install Linux to a cloud
environment (such as Amazon Web Services) or virtual machine on a virtualization host, such
as Virtual Box or a VMware system. Chapter 27 and Chapter 28 describe ways of installing or
deploying a virtual machine on a Linux KVM host or in a cloud environment.

To try the procedures in this chapter along with me, you should have a computer in front
of you that you don’t mind totally erasing. As an alternative, you can use a computer that
has another operating system installed (such as Windows), as long as there is enough
unused disk space available outside of that operating system. I describe the procedure,
and risk of data loss, if you decide to set up one of these “dual boot” (Linux and Windows)
arrangements.

**Choosing a Computer**

You can get a Linux distribution that runs on handheld devices or an old PC in your closet
with as little as 24MB of RAM and a 486 processor. To have a good desktop PC experience
with Linux, however, you should consider what you want to be able to do with Linux when
you are choosing your computer.

Be sure to consider the basic specifications that you need for a PC-type computer to run the
Fedora and Red Hat Enterprise Linux distributions. Because Fedora is used as the basis for
Red Hat Enterprise Linux releases, hardware requirements are similar for basic desktop and
server hardware for those two distributions.

Processor A 1GHz Pentium processor is the minimum for a GUI installation. For most
applications, a 32-bit processor is fine (x86). However, if you want to set up the
system to do virtualization, you need a 64-bit processor (x86_64).


> Note:
> 
> If you have a less powerful computer than the minimum described here, consider using a lightweight Linux
distribution. Lightweight Ubuntu distributions include Peppermint OS (https://peppermintos.com/) and
Lubuntu (https://lubuntu.net/). For a lightweight Fedora-based distribution, try the LXDE desktop
(https://spins.fedoraproject.org/lxde/). For a Linux distribution requiring the least resources, you
could try Tiny Core Linux (http://tinycorelinux.net/).
 
