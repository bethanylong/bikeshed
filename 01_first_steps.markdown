First steps
===========

Virtual machines
----------------

One of the core technologies allowing developers today to manage their environments quickly and easily is **virtualization**. We've probably all had bad experiences trying to install or upgrade software and making a mess. With virtual machines, you can run a completely separate operating system and environment on your computer without the risk of altering your main machine. Additionally, if other people want to use a development environment identical to yours for the sake of consistency, you can share your virtual machine itself or instructions for making the same one.

At any rate, regardless of how you create or acquire VMs, having the flexibility and control they provide makes all the concepts and techniques we'll be talking about much easier and more pleasant to play with.

### Hypervisors

Many operating systems come with virtualization capabilities by default, like Linux's LXC, but the virtualization software packages (sometimes known as **hypervisors**) easiest to use are available for download. If you want to run virtual machines on your own computer, we recommend using either **Virtualbox** or **VMware Workstation**. If you're running Ubuntu or Debian, you can run `sudo apt-get install virtualbox` in a terminal window to install Virtualbox, and if you're on another operating system, you can download an installer from [their website](https://www.virtualbox.org/wiki/Downloads). VMware Workstation normally costs money, but WWU computer science students can download it for free (legally) using [instructions available](https://support.cs.wwu.edu) from CS Support's website. If you're on a CS lab machine, both Virtualbox and VMware Workstation are already available for you.

### Vagrant

It's perfectly reasonable to use your favorite hypervisor to install an OS on your VM as though it were a physical computer, using an ISO file and going through the OS install process manually. However, if you need to set up a bunch of VMs, or if you're allergic to doing things manually when it's possible to automate them, fear not: there are tools like **Vagrant** that can easily automate setting up VMs. As with Virtualbox, on Ubuntu/Debian you can run `sudo apt-get install vagrant` in a terminal to install it, or download an installer from [their website](https://www.vagrantup.com/downloads.html) on other OSs.

Vagrant integrates with Virtualbox really well by default, though it can also integrate with other hypervisors. If you're using Virtualbox, or if you've set Vagrant up to use another hypervisor, you can set up a clean Ubuntu environment super easily:

    vagrant box add ubuntu/trusty64
    vagrant init ubuntu/trusty64

### Cloud providers

Another option for running VMs, especially if you'd rather not run them on your own hardware or want to access them from anywhere, is to use a public cloud provider. One such provider, Digital Ocean, provides $100 in free credit via GitHub's [student developer pack](https://education.github.com/pack) to people with .edu email accounts. Additionally, Amazon provides [a year of free access](https://aws.amazon.com/free/) to certain cloud services (including VMs through their EC2 service) for new users.

SSH
---

If you've never been up close and personal with a Unix command line, now is a wonderful time to start. There exist methods of accessing a graphical environment remotely (which is still technically the case even if you're running a VM on your local machine), but by far the most popular and efficient is through the command line. In turn, the best way to get a shell on a remote Linux machine is via `ssh`. If the machine you're trying to access has an `ssh` server running on port 22 (which is the default), you can get a shell by simply doing `ssh username@hostname` in a terminal, substituting `username` for your user on the remote machine and `hostname` for the hostname or IP address of the remote machine. If you don't have an `ssh` server running on the remote machine and it's running Ubuntu/Debian, you can run `sudo apt-get install ssh` in a local console.

The `man` (manual) page for `ssh`, conveniently available by doing `man ssh`, explains the wealth of options available. One of the most common options, `-p`, lets you connect to an `ssh` server on a non-default port. For example, at the time of writing, the canonical way to remotely connect to a WWU CS machine is port 922 on `linux-01.cs.wwu.edu` through `linux-12.cs.wwu.edu` (or just `linux.cs.wwu.edu`). You can do this with:

    ssh -p 922 username@linux.cs.wwu.edu

If you set up [SSH keys](http://blog.packetdisarray.com/2015/08/06/passphrase-ssh-keys-without-repetitive-typing/), you won't have to type your password in every time.

As a side note, if you've never encountered `man` pages, it's worth doing `man man` to see what they're all about. In short, `man` pages are your system's built-in documentation for installed programs and certain other system features.

### tmux

`tmux`, which stands for "terminal multiplexer", is an excellent way to manage your `ssh` connections, especially if you're connecting to multiple machines or even if you just want to avoid constantly setting up a new session. Many people connect to different machines in completely separate terminal windows, but with `tmux`, you can connect to one machine running your `tmux` session, attach to your session, and have access to as many persistent `ssh` connections as you can stomach.

Tucker probably has a cool gif/webm he can use to demonstrate this.

`tmux` is highly configurable and has features like horizontally and vertically splitting windows. Even if you don't think you need it yet, it's worth giving it a try -- you might find it more useful than you anticipated.
