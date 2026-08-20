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
 

RAM Fedora recommends at least 1GB of RAM, but at least 2GB or 3GB would be much
better. On my RHEL desktop, I’m running a web browser, word processor, and mail
reader, and I’m consuming over 2GB of RAM.
DVD or USB drive You need to be able to boot up the installation process from a DVD
or USB drive. In recent releases, the Fedora live media ISO has become too big to fit
on a CD, so you need to burn it to a DVD or USB drive. If you can’t boot from a DVD
or USB drive, there are ways to start the installation from a hard disk or by using a
PXE install. After the installation process is started, more software can sometimes be
retrieved from different locations (over the network or from hard disk, for example).


Note
PXE (pronounced pixie) stands for Preboot eXecution Environment (PXE). You can boot a client computer from a
Network Interface Card (NIC) that is PXE-enabled. If a PXE boot server is available on the network, it can provide
everything a client computer needs to boot. What it boots can be an installer. So, with a PXE boot, it is possible to do
a complete Linux installation without a CD, DVD, or any other physical medium.


Network card You need wired or wireless networking hardware to be able to add more
software or get software updates. Fedora offers free software repositories if you can connect
to the Internet. For RHEL, updates are available as part of the subscription price.
Disk space Fedora recommends at least 20GB of disk space for an average desktop
installation, although installations can range (depending on which packages you
choose to install) from 600MB (for a minimal server with no GUI install) to 7GB (to
install all packages from the installation DVD). Consider the amount of data that
you need to store. Although documents can consume very little space, videos can
consume massive amounts of space. (By comparison, you can install Tiny Core Linux
to disk with only about 16MB of disk space, which includes a GUI.)
Special hardware features Some Linux features require special hardware features. For
example, to use Fedora or RHEL as a virtualization host using KVM, the computer must
have a processor that supports virtualization. These include AMD-V or Intel-VT chips.
If you’re not sure about your computer hardware, there are a few ways to check what you
have. If you are running Windows, the System Properties window can show you the processor
you have as well as the amount of RAM that’s installed. As an alternative, with the
Fedora Live CD booted, open a shell and type dmesg | less to see a listing of hardware
as it is detected on your system.


With your hardware in place, you can choose to install Linux from a Live CD or from installation
media, as described in the following sections.
Installing Fedora from Live Media
In Chapter 2, you learned how to get and boot up Linux Live media. This chapter steps you
through an installation process of a Fedora Live DVD so that it is permanently installed on
your hard disk.
Simplicity is the main advantage of installing from Live media. Essentially, you are just
copying the kernel, applications, and settings from the ISO image to the hard disk. There
are fewer decisions that you have to make to do this kind of installation, but you also don’t
get to choose exactly which software packages to install. After the installation, you can
add and remove packages as you please.
The first decisions that you must make about your Live media installation include where
you want to install the system and whether you want to keep existing operating systems
around when your installation is done:
Single-boot computer The easiest way to install Linux is to not have to worry about
other operating systems or data on the computer and have Linux replace everything.
When you are done, the computer boots up directly to Fedora.
Multi-boot computer If you already have Windows installed on a computer and you
don’t want to erase it, you can install Fedora along with Windows on that system.
Then, at boot time, you can choose which operating system to start up. To be able
to install Fedora on a system with another operating system installed, you must
have either extra disk space available (outside the Windows partition) or be able
to shrink the Windows system to gain enough free space to install Fedora. Because
multi-boot computers are tedious to set up and risk damaging your installed system,
I recommend installing Linux on a separate computer, even an old used one, or on a
virtual machine, as opposed to multi-booting.
Bare metal or virtual system The resulting Fedora installation can be installed to
boot up directly from the computer hardware or from within an existing operating
system on the computer. If you have a computer that is running as a virtual host,
you can install Fedora on that system as a virtual guest. Virtualization host software
includes KVM, Xen, and VirtualBox (for Linux and UNIX systems as well as Windows
and the Mac OS), Hyper-V (for Microsoft systems), and VMware (for Linux, Windows,
and Mac OS). You can use the Fedora Live ISO image from disk or burned to a DVD to
start an installation from your chosen hypervisor host. (Chapter 27, “Using Linux for
Cloud Computing,” describes how to set up a KVM virtualization host.)
The following procedure steps you through the process of installing the Fedora Live ISO
described in Chapter 2 to your local computer. Because the Fedora 30 installation is very
similar to the Red Hat Enterprise Linux 8 installation described later in this chapter, you
can refer to that procedure if you want to go beyond the simple selections shown here (particularly
in the area of storage configuration).

Caution
Before beginning the procedure, be sure to make backup copies of any data on the computer that you still want to
keep. Although, you can choose not to erase selected disk partitions (as long as there is enough space available on
other partitions), there is always a risk that data can be lost when you are manipulating disk partitions. Also, unplug
any USB drives that you have plugged into your computer because they could be overwritten.

1. Get Fedora. Choose the Fedora Live media image that you want to use, download
it to your local system, and burn it to an appropriate medium. See Appendix A for
information on how to get the Fedora Live media and burn it to a DVD or USB drive.
2. Boot the Live image. Insert the DVD or USB drive. When the BIOS screen appears,
look for a message that tells you to press a particular function key (such as F12)
to interrupt the boot process and select the boot medium. Select the DVD or USB
drive, depending on which you have, and Fedora should come up and display the
boot screen. When you see the boot screen, select Start Fedora-Workstation-Live.
3. Start the installation. When the Welcome to Fedora screen appears, position your
mouse over the Install to Hard Drive area and select it. Figure 9.1 shows an example
of the Install to Hard Drive selection on the Fedora Live media.

<img width="530" height="493" alt="Screenshot 2026-08-20 154212" src="https://github.com/user-attachments/assets/0f02e92a-eeac-4c39-8f17-bdcc2e277558" />

4. Select the language. When prompted, choose the language type that best suits you
(such as U.S. English) and select Next. You should see the Installation summary
screen, as shown in Figure 9.2.

<img width="777" height="387" alt="Screenshot 2026-08-20 154342" src="https://github.com/user-attachments/assets/701718ee-35c0-43c4-a7d0-c2340c608f83" />


5. Select Time & Date. From the Time & Date screen, you can select your time zone
either by clicking the map or choosing the region and city from drop-down boxes.
To set the date and time, if you have an Internet connection, you can select the
Network Time button to turn it on, or you can select OFF and set the date and time
manually from boxes on the bottom of the screen. Select Done in the upper-right
corner when you are finished.
6. Select the installation destination. Available storage devices (such as your hard
drive) are displayed, with your hard drive selected as the installation destination.
If you want the installer to install Fedora automatically, reclaiming existing disk
space, make sure that your disk is selected (not a USB drive or other device connected
to your computer), then make the following selections:
a. Automatic . . . If there is enough available disk space on the selected disk drive,
you can continue with the installation by selecting Continue. Otherwise, you
need to reclaim disk space as follows:
I would like to make additional space available. . . If you want to erase the
hard drive completely, select this check box and click Continue. You can erase
some or all of the partitions that currently contain data.
b. Reclaim Disk Space. From this screen, you can select Delete All. Then select
Reclaim Space. Partitioning is set up automatically and you are returned to the
Installation Summary screen.

7. Select the keyboard. You can just use the default English (U.S.) keyboard or select
Keyboard to choose a different keyboard layout.
8. Begin installation. Select Begin Installation to begin installing to hard disk.
9. Finish the configuration. When the first part of the installation is complete, click Quit.
10. Reboot. Select the little on/off button from the menu on the top-right corner of the
screen. When prompted, click the Restart button. Eject or remove the Live media
when the system boot screen appears. The computer should boot to your newly
installed Fedora system. (You may actually need to power off the computer for it to
boot back up.)
11. Begin using Fedora. A first boot screen appears at this point, allowing you to create
a user account and password, among other things. You are automatically logged in
as that user account when configuration is done. That account has sudo privileges,
so you can immediately begin doing administrative tasks as needed.
12. Get software updates. To keep your system secure and up to date, one of the first
tasks that you should do after installing Fedora is to get the latest versions of the
software you just installed. If your computer has an Internet connection (plugging
into a wired Ethernet network or selecting an accessible wireless network from the
desktop takes care of that), you can simply open a Terminal as your new user and
type sudo dnf update to download and update all of your packages from the
Internet. If a new kernel is installed, you can reboot your computer to have that
new kernel take effect.
At this point, you can begin using the desktop, as described in Chapter 2. You can also use
the system to perform exercises from any of the chapters in this book.
Installing Red Hat Enterprise Linux from
Installation Media
In addition to offering a live DVD, most Linux distributions offer a single image or set of
images that can be used to install the distribution. For this type of installation media,
instead of copying the entire contents of the medium to disk, software is split up into
packages that you can select to meet your exact needs. A full installation DVD, for example,
can allow you to install anything from a minimal system to a fully featured desktop to a
full-blown server that offers multiple services.
In this chapter, I use a Red Hat Enterprise Linux 8 installation DVD as the installation
medium. Review the hardware information and descriptions of dual booting in the previous
section before beginning your RHEL installation.
Follow this procedure to install Red Hat Enterprise Linux from an installation DVD.
1. Get the installation media. The process of downloading RHEL install ISO images is
described on the Red Hat Enterprise Linux product page. If you are not yet a Red
Hat customer, you can apply for an evaluation copy here: https://www.redhat.com/
en/technologies/linux-platforms/enterprise-linux.
This requires that you create a Red Hat account. If that is not possible, you can
download an installation DVD from a mirror site of the CentOS project to get a similar
experience: https://wiki.centos.org/Download.
For this example, I used the 6.7G RHEL 8 DVD ISO rhel-8.0-x86_64-dvd.iso.
After you have the DVD ISO, you can burn it to a physical USB drive or dual-layer
DVD, as described in Appendix A.
2. Boot the installation media. Insert the USB drive or DVD into your computer
and reboot. (If you need to, interrupt the boot prompt to select to boot from the
selected USB or DVD.) The Welcome screen appears.
3. Select Install or Test Media. Select the Install or the “Test this media & install”
entry to do a new installation of RHEL. The media test verifies that the DVD has
not been corrupted during the copy or burning process. If you need to modify the
installation process, you can add boot options by pressing the Tab key with a boot
entry highlighted and typing in the options you want. See the section “Using
installation boot options” later in this chapter.
4. Select a language. Select your language and choose Continue. The Installation Summary
screen appears. From that screen, you can select to change any of the available
Localization, Software, and System features, as shown in Figure 9.3.

<img width="768" height="452" alt="Screenshot 2026-08-20 154552" src="https://github.com/user-attachments/assets/fb188e44-ebc9-4a9c-981b-22844cbb326f" />

5. Keyboard. Choose from different types of keyboards available with the languages
you selected earlier. Type some text to see how the keys are laid out.
6. Language Support. You have a chance to add support for additional languages
(beyond what you set by default earlier). Select Done when you are finished.
7. Time & Date. Choose a time zone for your machine from either the map or the list
shown (as described in the section “Installing Fedora from Live Media”). Either
set the time manually with up/down arrows or select Network Time to have your
system try to connect to networked time servers automatically to sync system
time. Select Done when you are finished.
8. Installation Source. The installation DVD is used, by default, to provide the RPM
packages that are used during installation. You have the option of selecting “On
the network” and choosing a Web URL (http, https, or ftp) identifying where
the Red Hat Enterprise Linux software repository is located. After choosing the DVD
or a network location, you can add additional yum repositories to have those repositories
used during installation as well. Select Done when you are finished.
9. Software Selection. The default “Server with GUI” selection provides a GNOME 3
desktop system on top of a basic server install. Other choices include "Server"
(which has no GUI), "Minimal Install" (which starts with a basic package set), and
"Workstation" (geared for end users). You can select to add other services or other
base environments to include. Select Done when you are ready to continue.
10. Installation Destination. The new RHEL system is installed, by default, on the local
hard drive using automatic partitioning. You also have the option of attaching network
storage or special storage, such as Firmware RAID. (See the section “Partitioning
hard drives” later in this chapter for details on configuring storage.) Click Done
when you are finished. You may be asked to verify that it’s okay to delete existing
storage.
11. Kdump. Enabling kdump sets aside RAM to be used to capture the resulting kernel
dump in the event that your kernel crashes. Without kdump, there would be no
way to diagnose a crashed kernel. By default, enabling kdump sets aside 160MB
plus 2 bits for every 4KB of RAM for saving kernel crashes.
12. Network & Host Name. Any network interface cards that are discovered can be configured
at this point. If a DHCP service is available on the network, network address
information is assigned to the interface after you select ON. Select Configure if you
prefer to configure the network interface manually. Fill in the Hostname box if you
want to set the system’s hostname. Setting up your network and hostname during
installation can make it easier to begin using your system after installation. Click
Done to continue.
13. Security Policy. By choosing a security policy (none is chosen by default), you can
ensure that your system complies with a selected security standard. All fields are
optional and can be changed later.
14. System Purpose. This optional selection lets you choose the system’s role, servicelevel
agreement, and usage.


15. Begin the installation. Click the Begin Installation button to start the install
process. A progress bar marks the progress of the installation. As the system is
installing, you can set the root password and create a new user account for your
new system.
16. Root Password. Set the password for the root user and verify it (type it again).
Click Done to accept it. If the password is too short or too weak, you stay on the
page (where you can set a new password). If you decide to keep the weak password
instead, click Done again to accept the weak password.
17. User Creation. It is good practice to log into a Linux system with a non-root user
account and request root privilege as needed. You can set up a user account, including
a username, full name, and password. You can select “Make this user administrator”
to give that user sudo privileges (allowing the account to act as the root
user as needed). Select Done when you are finished. If the password you enter is
too short or otherwise weak, you must change it or click Done again if you still
want to use the weak password.
18. Complete the installation. When installation is finished, click Reboot. Pop out the
DVD when the system restarts and Red Hat Enterprise Linux starts up from the
hard disk.
19. Run firstboot. If you installed a desktop interface, the firstboot screen appears the
first time you boot the system. Here’s what you do:
a. License Information. Read and click the check box to accept the license information,
then click Done.
b. Subscription Manager. When prompted, you can leave the default subscription
management system in place (subscription.rhn.redhat.com) or enter the
location of a Red Hat Satellite server to register your system. Click Next. Enter
your Red Hat account and password, then click Register to register and entitle
your system to updates. If the subscription found is acceptable, click Attach to
enable the subscription.
20. Select Finish Configuration when you are done.
You should now be able to log in to your Red Hat Enterprise Linux system. One of the first
things that you should do is to get software updates for the new system. Do this by logging
into the system and running sudo dnf upgrade from a Terminal window.
Understanding Cloud-Based Installations
When you install a Linux system on a physical computer, the installer can see the computer’s
hard drive, network interfaces, CPUs, and other hardware components. When you
install Linux in a cloud environment, those physical components are abstracted into a pool
of resources. So, to install a Linux distribution in an Amazon EC2, Google Compute Engine,
or OpenStack cloud platform, you need to go about things differently.

The common way of installing Linux in a cloud is to start with a file that is an image of
an installed Linux system. Typically, that image includes all of the files needed by a basic,
running Linux system. Metadata is added to that image from a configuration file or by
filling out a form from a cloud controller that creates and launches the operating system as
a virtual machine.
The kind of information added to the image might include a particular hostname, root
password, and new user account. You might also want to choose to have a specific amount
of disk space, a particular network configuration, and a certain number of CPU processors
and RAM.
Methods for installing Linux in a local cloud-like KVM environment are discussed in Chapter
28, “Deploying Linux to the Cloud.” That chapter covers how to run a Linux system
as a virtual machine image on a KVM environment, Amazon EC2 cloud, or OpenStack
environment.
Installing Linux in the Enterprise
If you were managing dozens, hundreds, even thousands of Linux systems in a large enterprise,
it would be terribly inefficient to have to go to each computer to type and click through
each installation. Fortunately, with Red Hat Enterprise Linux and other distributions, you
can automate installation in such a way that all you need to do is to turn on a computer and
boot from the computer’s network interface card to get your desired Linux installation.
Although we have focused on installing Linux from a DVD or USB media, there are many
other ways to launch a Linux installation and many ways to complete an installation. The
following descriptions step through the installation process and describe ways of changing
that process along the way:
Launch the installation medium. You can launch an installation from any medium
that you can boot from a computer: CD, DVD, USB drive, hard disk, or network interface
card with PXE support. The computer goes through its boot order and looks at the
master boot record on the physical medium or looks for a PXE server on the network.
Start the anaconda kernel. The job of the boot loader is to point to the special
kernel (and possibly an initial RAM disk) that starts the Linux installer (called
anaconda). So, any of the media types just described simply needs to point to the
location of the kernel and initial RAM disk to start the installation. If the software
packages are not on the same medium, the installation process prompts you for
where to get those packages.
Add kickstart or other boot options. Boot options (described later in this chapter)
can be passed to the anaconda kernel to configure how it starts up. One option
supported by Fedora and RHEL allows you to pass the location of a kickstart file to
the installer. That kickstart can contain all of the information needed to complete
the installation: root password, partitioning, time zone, and so on to configure the
installed system further. After the installer starts, it either prompts for needed
information or uses the answers provided in the kickstart file.

Find software packages. Software packages don’t have to be on the installation
medium. This allows you to launch an installation from a boot medium that contains
only a kernel and initial RAM disk. From the kickstart file or from an option
you enter manually to the installer, you can identify the location of the repository
holding the RPM software packages. That location can be a local CD (cdrom), website
(http), FTP site (ftp), NFS share (nfs), NFS ISO (nfsiso), or local disk (hd).
Modify installation with kickstart scripts. Scripts included in a kickstart can
run commands you choose before or after the installation to further configure the
Linux system. Those commands can add users, change permissions, create files and
directories, grab files over the network, or otherwise configure the installed system
exactly as you specify.
Although installing Linux in enterprise environments is beyond the scope of this book, I
want you to understand the technologies that are available when you want to automate the
Linux installation process. Here are some of those technologies available to use with Red
Hat Enterprise Linux, along with links to where you can find more information about them:
Install server If you set up an installation server, you don’t have to carry the software
packages around to each machine where you install RHEL. Essentially, you
copy all of the software packages from the RHEL installation medium to a web
server (http), FTP server (ftp), or NFS server (nfs) and then point to the location
of that server when you boot the installer. The RHEL 8 Installation Guide describes
how to set up a local or network installation source:
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/
html-single/performing_a_standard_rhel_installation/index#prepareinstallation-
source_preparing-for-your-installation
PXE server If you have a computer with a network interface card that supports PXE
booting (as most do), you can set your computer’s BIOS to boot from that NIC. If you
have set up a PXE server on that network, that server can present a menu to the
computer containing entries to launch an installation process. The RHEL Installation
Guide provides information on how to set up PXE servers for installation:
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/
html-single/performing_a_standard_rhel_installation/index#booting-theinstallation-
using-pxe_booting-the-installer
Kickstart files To automate an installation completely, you create what is called a
kickstart file. By passing a kickstart file as a boot option to a Linux installer, you
can provide answers to all of the installation questions that you would normally
have to click through.
When you install RHEL, a kickstart file containing answers to all installation questions
for the installation you just did is contained in the /root/anaconda-ks.cfg
file. You can present that file to your next installation to repeat the installation configuration
or use that file as a model for different installations.

See the Advanced RHEL Installation Guide for information on performing a kickstart
installation: https://access.redhat.com/documentation/en-us/red_hat_enterprise_
linux/8/html-single/performing_an_advanced_rhel_installation/
index/#performing_an_automated_installation_using_kickstart
. . . and creating your own kickstart files https://access.redhat.com/documentation/
en-us/red_hat_enterprise_linux/8/html-single/
performing_an_advanced_rhel_installation/index/#creating-kickstart-files_
installing-rhel-as-an-experienced-user
Exploring Common Installation Topics
Some of the installation topics touched upon earlier in this chapter require further explanation
for you to be able to implement them fully. Read through the following sections to
get a greater understanding of specific installation topics.
Upgrading or installing from scratch
If you have an earlier version of Linux already installed on your computer, Fedora, Ubuntu,
and other Linux distributions offer an upgrade option. Red Hat Enterprise Linux offers a
limited upgrade path from RHEL 7 to RHEL 8.
Upgrading lets you move a Linux system from one major release to the next. Between minor
releases, you can simply update packages as needed (for example, by typing yum update).
Here are a few general rules before performing an upgrade:
Remove extra packages. If you have software packages that you don’t need, remove
them before you do an upgrade. Upgrade processes typically upgrade only those
packages that are on your system. Upgrades generally do more checking and comparing
than clean installs do, so any package that you can remove saves time during
the upgrade process.
Check configuration files. A Linux upgrade procedure often leaves copies of
old configuration files. You should check that the new configuration files still
work for you.

> Tip
> Installing Linux from scratch goes faster than an upgrade. It also results in a cleaner Linux system. So, if you don’t
> need the data on your system (or if you have a backup of your data), I recommend that you do a fresh installation.
> Then you can restore your data to a freshly installed system.

Some Linux distributions, most notably Gentoo, have taken the approach of providing
ongoing updates. Instead of taking a new release every few months, you simply continuously
grab updated packages as they become available and install them on your system.

Dual booting
It is possible to have multiple operating systems installed on the same computer. One way
to do this is by having multiple partitions on a hard disk and/or multiple hard disks and
then installing different operating systems on different partitions. As long as the boot
loader contains boot information for each of the installed operating systems, you can
choose which one to run at boot time.

> Caution
Although tools for resizing Windows partitions and setting up multi-boot systems have improved in recent years, there
is still some risk of losing data on Windows/Linux dual-boot systems. Different operating systems often have different
views of partition tables and master boot records that can cause your machine to become unbootable (at least
temporarily) or lose data permanently. Always back up your data before you try to resize a Windows filesystem to
make space for Linux.

If the computer you are using already has a Windows system on it, quite possibly the entire
hard disk is devoted to Windows. Although you can run a bootable Linux, such as KNOPPIX
or Tiny Core Linux, without touching the hard disk, to do a more permanent installation,
you’ll want to find disk space outside of the Windows installation. There are a few ways
to do this:
Add a hard disk. Instead of messing with your Windows partition, you can simply
add a hard disk and devote it to Linux.
Resize your Windows partition. If you have available space on a Windows partition,
you can shrink that partition so that free space is available on the disk to devote
to Linux. Commercial tools such as Acronis Disk Director (https://www.acronis.com/
en-us/personal/disk-manager) are available to resize your disk partitions and set
up a workable boot manager. Some Linux distributions (particularly bootable Linux
distributions used as rescue media) include a tool called GParted (which includes
software from the Linux-NTFS project for resizing Windows NTFS partitions).

Note
Type dnf install gparted (in Fedora) or apt-get install gparted (in Ubuntu) to install GParted.
Run gparted as root to start it.

Before you try to resize your Windows partition, you might need to defragment it. To
defragment your disk on some Windows systems so that all your used space is put in order
on the disk, open My Computer, right-click your hard disk icon (typically C:), select Properties,
click Tools, and select Defragment Now.

Defragmenting your disk can be a fairly long process. The result of defragmentation is that
all of the data on your disk are contiguous, creating lots of contiguous free space at the
end of the partition. Sometimes, you have to complete the following special tasks to make
this true:
■■ If the Windows swap file is not moved during defragmentation, you must remove it.
Then, after you defragment your disk again and resize it, you need to restore the
swap file. To remove the swap file, open the Control Panel, open the System icon,
click the Performance tab, and select Virtual Memory. To disable the swap file, click
Disable Virtual Memory.
■■ If your DOS partition has hidden files that are on the space you are trying to free
up, you need to find them. In some cases, you can’t delete them. In other cases,
such as swap files created by a program, you can safely delete those files. This is
a bit tricky because some files should not be deleted, such as DOS system files.
You can use the attrib -s -h command from the root directory to deal with
hidden files.
After your disk is defragmented, you can use commercial tools described earlier (Acronis
Disk Director) to repartition your hard disk to make space for Linux. Or, you can use the
open-source alternative GParted.
After you have cleared enough disk space to install Linux (see the disk space requirements
described earlier in this chapter), you can install Ubuntu, Fedora, RHEL, or another Linux
distribution. As you set up your boot loader during installation, you can identify Windows,
Linux, and any other bootable partitions so that you can select which one to boot when
you start your computer.
Installing Linux to run virtually
Using virtualization technology, such as KVM, VMware, VirtualBox, or Xen, you can configure
your computer to run multiple operating systems simultaneously. Typically, you have
a host operating system running (such as your Linux or Windows desktop), and then you
configure guest operating systems to run within that environment.
If you have a Windows system, you can use commercial VMware products to run Linux on
your Windows desktop. Get a trial of VMware Workstation (https://www.vmware.com/tryvmware)
to see if you like it. Then run your installed virtual guests with the free VMware
Player. With a full-blown version of VMware Workstation, you can run multiple distributions
at the same time.
Open-source virtualization products that are available with Linux systems include VirtualBox
(https://www.virtualbox.org), Xen (https://xenproject.org), and KVM (https://
www.linux-kvm.org). Some Linux distributions still use Xen. However, all Red Hat systems
currently use KVM as the basis for Red Hat’s hypervisor features in RHEL, Red Hat Virtualization,
and other cloud projects. See Chapter 28 for information on installing Linux as a
virtual machine on a Linux KVM host.

Using installation boot options
When the anaconda kernel launches at boot time for RHEL or Fedora, boot options provided
on the kernel command line modify the behavior of the installation process. By interrupting
the boot loader before the installation kernel boots, you can add your own boot options
to direct how the installation behaves.
When you see the installation boot screen, depending on the boot loader, press Tab or some
other key to be able to edit the anaconda kernel command line. The line identifying the
kernel might look something like the following:
vmlinuz initrd=initrd.img ...
The vmlinuz is the compressed kernel and initrd.img is the initial RAM disk (containing
modules and other tools needed to start the installer). To add more options, just type
them at the end of that line and press Enter.
So, for example, if you have a kickstart file available from /root/ks.cfg on a CD, your
anaconda boot prompt to start the installation using the kickstart file could look like the
following:
vmlinuz initrd=initrd.img ks=cdrom:/root/ks.cfg
For Red Hat Enterprise Linux 8 and the latest Fedora releases, kernel boot options used during
installation are transitioning to a new naming method. With this new naming, a prefix
of inst. can be placed in front of any of the boot options shown in this section that are
specific to the installation process (for example, inst.xdriver or inst.repo=dvd). For
the time being, however, you can still use the options shown in the next few sections with
the inst. prefix.
Boot options for disabling features
Sometimes, a Linux installation fails because the computer has some non-functioning or
non-supported hardware. Often, you can get around those issues by passing options to the
installer that do such things as disable selected hardware when you need to select your
own driver. Table 9.1 provides some examples.
Boot options for video problems
If you are having trouble with your video display, you can specify video settings as noted
in Table 9.2.
Boot options for special installation types
By default, installation runs in graphical mode when you're sitting at the console
answering questions. If you have a text-only console, or if the GUI isn't working properly,
you can run an installation in plain-text mode: by typing text, you cause the installation
to run in text mode.

TABLE 9.1 Boot Options for Disabling Features
Installer Option Tells System
nofirewire Not to load support for firewire devices
nodma Not to load DMA support for hard disks
noide Not to load support for IDE devices
nompath Not to enable support for multipath devices
noparport Not to load support for parallel ports
nopcmcia Not to load support for PCMCIA controllers
noprobe Not to probe hardware; instead prompt user for drivers
noscsi Not to load support for SCSI devices
nousb Not to load support for USB devices
noipv6 Not to enable IPV6 networking
nonet Not to probe for network devices
numa-off To disable the Non-Uniform Memory Access (NUMA) for AMD64 architecture
acpi=off To disable the Advanced Configuration and Power Interface (ACPI)
TABLE 9.2 Boot Options for Video Problems
Boot Option Tells System
xdriver=vesa Use standard vesa video driver
resolution=1024x768 Choose exact resolution to use
nofb Don't use the VGA 16 framebuffer driver
skipddc Don't probe DDC of the monitor (the probe can hang the installer)
graphical Force a graphical installation



If you want to start installation on one computer, but you want to answer the installation
questions from another computer, you can enable a VNC (virtual network computing)
installation. After you start this type of installation, you can go to another system and
open a vnc viewer, giving the viewer the address of the installation machine (such as
192.168.0.99:1). Table 9.3 provides the necessary commands, along with what to tell the
system to do.
Boot options for kickstarts and remote repositories
You can boot the installation process from an installation medium that contains little more
than the kernel and initial RAM disk. If that is the case, you need to identify the repository
where the software packages exist. You can do that by providing a kickstart file or by
identifying the location of the repositories in some way. To force the installer to prompt for
the repository location (CD/DVD, hard drive, NFS, or URL), add askmethod to the installation
boot options.


TABLE 9.3 Boot Options for VNC Installations
Boot Option Tells System
vnc Run installation as a VNC server
vncconnect=hostname[:port] Connect to VNC client hostname and optional port
vncpassword=password Client uses password (at least 8 characters) to connect
to installer


Using repo= options, you can identify software repository locations. The following examples
show the syntax to use for creating repo= entries:
repo=hd:/dev/sda1:/myrepo
Repository in /myrepo on disk 1 first partition
repo=http://abc.example.com/myrepo
Repository available from /myrepo on web server
repo=ftp://ftp.example.com/myrepo
Repository available from /myrepo on FTP server
repo=cdrom
Repository available from local CD or DVD
repo=nfs::mynfs.example.com:/myrepo/
Repository available from /myrepo on NFS share
repo=nfsiso::nfs.example.com:/mydir/rhel7.iso
Installation ISO image available from NFS server
Instead of identifying the repository directly, you can specify it within a kickstart file. The
following are examples of some ways to identify the location of a kickstart file.
ks=cdrom:/stuff/ks.cfg
Get kickstart from CD/DVD.
ks=hd:sda2:/test/ks.cfg
Get kickstart from test directory on hard disk(sda2).
ks=http://www.example.com/ksfiles/ks.cfg
Get kickstart from a web server.
ks=ftp://ftp.example.com/allks/ks.cfg
Get kickstart from a FTP server.
ks=nfs:mynfs.example.com:/someks/ks.cfg
Get kickstart from an NFS server.
Miscellaneous boot options
Here are a few other options that you can pass to the installer that don’t fit in a category.
rescue
Instead of installing, run the kernel to open Linux rescue mode.
mediacheck
Check the installation CD/DVD for checksum errors.


For further information on using the anaconda installer in rescue mode (to rescue a broken
Linux system), see Chapter 21, “Troubleshooting Linux.” For information on the latest boot
options use in RHEL 8, refer to the RHEL 8 Installation Guide:
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/
html-single/performing_a_standard_rhel_installation/index#custom-bootoptions_
booting-the-installer
Using specialized storage
In large enterprise computing environments, it is common to store the operating system
and data outside of the local computer. Instead, some special storage device beyond the
local hard disk is identified to the installer, and that storage device (or devices) can be
used during installation.
Once identified, the storage devices that you indicate during installation can be used the
same way that local disks are used. You can partition them and assign a structure (filesystem,
swap space, and so on) or leave them alone and simply mount them where you want
the data to be available.
The following types of specialized storage devices can be selected from the Specialized
Storage Devices screen when you install Red Hat Enterprise Linux, Fedora, or other Linux
distributions:
Firmware RAID A firmware RAID device is a type of device that has hooks in the
BIOS, allowing it to be used to boot the operating system, if you choose.
Multipath devices As the name implies, multipath devices provide multiple paths
between the computer and its storage devices. These paths are aggregated, so these
devices look like a single device to the system using them, while the underlying
technology provides improved performance, redundancy, or both. Connections can
be provided by iSCSI or Fibre Channel over Ethernet (FCoE) devices.
Other SAN devices Any device representing a Storage Area Network (SAN).
While configuring these specialized storage devices is beyond the scope of this book, know
that if you are working in an enterprise where iSCSI and FCoE devices are available, you can
configure your Linux system to use them at installation time. You need the following types
of information to do this:
iSCSI devices Have your storage administrator provide you with the target IP address
of the iSCSI device and the type of discovery authentication needed to use the
device. The iSCSI device may require credentials.
Fibre Channel over Ethernet Devices (FCoE) For FCoE, you need to know the network
interface that is connected to your FCoE switch. You can search that interface
for available FCoE devices.


Partitioning hard drives
The hard disk (or disks) on your computer provide the permanent storage area for your data
files, applications programs, and the operating system itself. Partitioning is the act of dividing
a disk into logical areas that can be worked with separately. In Windows, you typically
have one partition that consumes the whole hard disk. However, with Linux there are several
reasons you may want to have multiple partitions:
Multiple operating systems If you install Linux on a PC that already has a Windows
operating system, you may want to keep both operating systems on the computer.
For all practical purposes, each operating system must exist on a completely separate
partition. When your computer boots, you can choose which system to run.
Multiple partitions within an operating system To protect their entire operating system
from running out of disk space, people often assign separate partitions to different areas
of the Linux filesystem. For example, if /home and /var were assigned to separate partitions,
then a gluttonous user who fills up the /home partition wouldn’t prevent logging
daemons from continuing to write to log files in the /var/log directory.
Multiple partitions also make doing certain kinds of backups (such as an image
backup) easier. For example, an image backup of /home would be much faster (and
probably more useful) than an image backup of the root filesystem (/).
Different filesystem types Different kinds of filesystems have different structures.
Filesystems of different types must be on their own partitions. Also, you might
need different filesystems to have different mount options for special features (such
as read-only or user quotas). In most Linux systems, you need at least one filesystem
type for the root of the filesystem (/) and one for your swap area. Filesystems
on CD-ROM use the iso9660 filesystem type.

Tip
When you create partitions for Linux, you usually assign the filesystem type as Linux native (using the ext2, ext3,
ext4, or xfs type on most Linux systems). If the applications that you are running require particularly long filenames,
large file sizes, or many inodes (each file consumes an inode), you may want to choose a different filesystem type.


Coming from Windows
If you have only used Windows operating systems before, you probably had your whole hard disk
assigned to C: and never thought about partitions. With many Linux systems, you have the opportunity
to view and change the default partitioning based on how you want to use the system.


During installation, systems such as Fedora and RHEL let you partition your hard disk
using graphical partitioning tools. The following sections describe how to partition your
disk during a Fedora installation. See the section “Tips for creating partitions” for some
ideas for creating disk partitions.


Understanding different partition types
Many Linux distributions give you the option of selecting different partition types when
you partition your hard disk during installation. Partition types include the following:
Linux partitions Use this option to create a partition for an ext2, ext3, or ext4 filesystem
type that is added directly to a partition on your hard disk (or other storage
medium). The xfs filesystem type can also be used on a Linux partition. (In fact, xfs
is now the default filesystem type for RHEL 8 systems.)
LVM partitions Create an LVM partition if you plan to create or add to an LVM volume
group. LVMs give you more flexibility in growing, shrinking, and moving partitions
later than regular partitions do.
RAID partitions Create two or more RAID partitions to create a RAID array. These
partitions should be on separate disks to create an effective RAID array. RAID
arrays can help improve performance, reliability, or both as those features relate to
reading, writing, and storing your data.
Swap partitions Create a swap partition to extend the amount of virtual memory
available on your system.
The following sections describe how to add regular Linux partitions and LVM, RAID, and
swap partitions using the Fedora graphical installer. If you are still not sure when you
should use these different partition types, refer to Chapter 12, “Managing Disks and Filesystems,”
for further information on configuring disk partitions.
Tips for creating partitions
Changing your disk partitions to handle multiple operating systems can be very tricky, in
part because each operating system has its own ideas about how partitioning information
should be handled as well as different tools for doing it. Here are some tips to help you
get it right:
■■ If you are creating a dual-boot system, particularly for a Windows system, try to
install the Windows operating system first after partitioning your disk. Otherwise,
the Windows installation may make the Linux partitions inaccessible.
■■ The fdisk man page recommends that you use partitioning tools that come with
an operating system to create partitions for that operating system. For example,
the Windows fdisk knows how to create partitions that Windows will like, and the
Linux fdisk will happily make your Linux partitions. After your hard disk is set
up for dual boot, however, you should probably not go back to Windows-only partitioning
tools. Use Linux fdisk or a product made for multi-boot systems (such as
Acronis Disk Director).
■■ A master boot record (MBR) partition table can contain four primary partitions, one
of which can be marked to contain 184 logical drives. On a GPT partition table, you
can have a maximum of 128 primary partitions on most operating systems, including
Linux. You typically won’t need nearly that many partitions. If you need more
partitions, use LVM and create as many logical volumes as you like.
Part III: Becoming a Linux System Administrator
216
If you are using Linux as a desktop system, you probably don’t need lots of different partitions.
However, some very good reasons exist for having multiple partitions for Linux
systems that are shared by lots of users or are public web servers or file servers. Having
multiple partitions within Fedora or RHEL, for example, offers the following advantages:
Protection from attacks Denial-of-service attacks sometimes take actions that try
to fill up your hard disk. If public areas, such as /var, are on separate partitions, a
successful attack can fill up a partition without shutting down the whole computer.
Because /var is the default location for web and FTP servers, and is expected to
hold lots of data, entire hard disks often are assigned to the /var filesystem alone.
Protection from corrupted filesystems If you have only one filesystem (/), its
corruption can cause the whole Linux system to be damaged. Corruption of a smaller
partition can be easier to fix and often allows the computer to stay in service while
the correction is made.
Table 9.4 lists some directories that you may want to consider making into separate filesystem
partitions.
TABLE 9.4 Assigning Partitions to Particular Directories
Directory Explanation
/boot Sometimes, the BIOS in older PCs can access only the first 1024 cylinders of your
hard disk. To make sure that the information in your /boot directory is accessible to
the BIOS, create a separate disk partition (by default, RHEL 8 sets this partition to
1024 MiB) for /boot. Even with several kernels installed, there is rarely a reason for /
boot to be larger than 1024 MiB.
/usr This directory structure contains most of the applications and utilities available
to Linux users. The original theory was that if /usr were on a separate partition,
you could mount that filesystem as read-only after the operating system had been
installed. This would prevent attackers from replacing or removing important
system applications with their own versions that may cause security problems. A
separate /usr partition is also useful if you have diskless workstations on your local
network. Using NFS, you can share /usr over the network with those workstations.
/var Your FTP (/var/ftp) and web server (/var/www) directories are, by default in many
Linux systems, stored under /var. Having a separate /var partition can prevent an
attack on those facilities from corrupting or filling up your entire hard disk.
/home Because your user account directories are located in this directory, having a separate
/home account can prevent a reckless user from filling up the entire hard disk. It
also conveniently separates user data from your operating system (for easy backups
or new installs). Often, /home is created as an LVM logical volume, so it can grow in
size as user demands increase. It may also be assigned user quotas to limit disk use.
/tmp Protecting /tmp from the rest of the hard disk by placing it on a separate partition
can ensure that applications that need to write to temporary files in /tmp can complete
their processing, even if the rest of the disk fills up.
Chapter 9: Installing Linux
217
9
Although people who use Linux systems rarely see a need for lots of partitions, those who
maintain and occasionally have to recover large systems are thankful when the system
they need to fix has several partitions. Multiple partitions can limit the effects of deliberate
damage (such as denial-of-service attacks), problems from errant users, and accidental
filesystem corruption.
Using the GRUB boot loader
A boot loader lets you choose when and how to boot the operating systems installed
on your computer’s hard disks. The GRand Unified Bootloader (GRUB) is the most popular
boot loader used for installed Linux systems. There are two major versions of GRUB available
today:
GRUB Legacy (version 1). This version of GRUB was used with earlier versions of RHEL,
Fedora, and Ubuntu.
GRUB 2. The current versions of Red Hat Enterprise Linux, Ubuntu, and Fedora use
GRUB 2 as the default boot loader.

Note
SYSLINUX is another boot loader that you will encounter with Linux systems. The SYSLINUX boot loaders are not typically
used for installed Linux systems. However, SYSLINUX is commonly used as the boot loader for bootable Linux
CDs and DVDs. SYSLINUX is particularly good for booting ISO9660 CD images (isolinux) and USB sticks (syslinux)
and for working on older hardware or for PXE booting (pxelinux) a system over the network.



If you want to boot to a particular run level, you can add the run level you want to the
end of the kernel line. For example, to have RHEL boot to run level 3 (multiuser plus networking
mode), add 3 to the end of the kernel line. You can also boot to single-user mode
(1), multiuser mode (2), or X GUI mode (5). Level 3 is a good choice if your GUI is temporarily
broken. Level 1 is good if you have forgotten your root password.
By default, you will see a splash screen as Linux boots. If you want to see messages showing
activities happening as the system boots up, you can remove the option rhgb quiet
from the kernel line. This lets you see messages as they scroll by. Pressing Esc during bootup
gets the same result.
GRUB 2 represents a major rewrite of the GRUB Legacy project. It was adopted as the default
boot loader for the latest Red Hat Enterprise Linux, Fedora, and Ubuntu releases. The major
function of the GRUB 2 boot loader is still to find and start the operating system you want,
but now much more power and flexibility is built into the tools and configuration files that
get you there.
In GRUB 2, the configuration file is now named /boot/grub2/grub.cfg or /etc/grub2-
efi.cfg (for systems booted with EFI). Everything from the contents of grub.cfg to the
way grub.cfg is created is different from the GRUB Legacy grub.conf file.


Here are some things you should know about the grub.cfg file:
■■ Instead of editing grub.cfg by hand or having kernel RPM packages add to it,
grub.cfg is generated automatically from the contents of the /etc/default/
grub file and the /etc/grub.d/ directory. You should modify or add to those
files to configure GRUB 2 yourself.
■■ The grub.cfg file can contain scripting syntax, including such things as
functions, loops, and variables.
■■ Device names needed to identify the location of kernels and initial RAM disks can
be more reliably identified using labels or universally unique identifiers (UUIDs).
This prevents the possibility of a disk device such as /dev/sda being changed
to /dev/sdb when you add a new disk (which would result in the kernel not
being found).
■■ For Fedora and RHEL systems, *conf files in the /boot/loader/entries directory
are used to create entries that appear on the GRUB menu that appears at
boot time.
You could create your own entry for the GRUB boot menu by following the format of an
existing entry. The following file in the /boot/loader/entries directory creates a
menu entry for booting a RHEL 8 kernel and initrd:
title Red Hat Enterprise Linux (4.18.0-80.el8.x86_64) 8.0 (Ootpa)
version 4.18.0-80.el8.x86_64
linux /vmlinuz-4.18.0-80.el8.x86_64
initrd /initramfs-4.18.0-80.el8.x86_64.img $tuned_initrd
options $kernelopts $tuned_params
id rhel-20190313123447-4.18.0-80.el8.x86_64
grub_users $grub_users
grub_arg --unrestricted
grub_class kernel
The menu entry for this selection appears as Red Hat Enterprise Linux (4.18.
0-80.el8.x86_64) 8.0 (Ootpa) on the GRUB 2 boot menu.
The linux line identifies the location of the kernel (/vmlinuz-4.18.0-80.el8.x86_64),
followed by the location of the initrd (/initramfs-4.18.0-80.el8.x86_64.img).
There are many, many more features of GRUB 2 that you can learn about if you want to
dig deeper into your system’s boot loader. The best documentation for GRUB 2 is available
by typing info grub2 at the shell. The info entry for GRUB 2 provides lots of information
for booting different operating systems, writing your own configuration files, working
with GRUB image files, setting GRUB environment variables, and working with other
GRUB features.


Summary
Although every Linux distribution includes a different installation method, you need to
do many common activities, regardless of which Linux system you install. For every Linux
system, you need to deal with issues of disk partitioning, boot options, and configuring
boot loaders.
In this chapter, you stepped through installation procedures for a Fedora Workstation
(using a live media installation) and Red Hat Enterprise Linux (from installation media).
You learned how deploying Linux in cloud environments can differ from traditional installation
methods by combining metadata with prebuilt base operating system image files to
run on large pools of compute resources.
The chapter also covered special installation topics, including using boot options and disk
partitioning. With your Linux system now installed, Chapter 10, “Getting and Managing
Software,” describes how to begin managing the software on your Linux system.
































