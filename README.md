# vulndev-tools

Just a repository for random tools that can be helpful during vulnerability
research and exploit development. For now, it only contains a script to set up
a kernel debugging environment.

![setup-kernel-debugging](setup-kernel-debugging.gif)

Dependencies: Multipass (https://multipass.run), QEMU, GDB and tmux.

To install dependencies under Ubuntu:
```bash
sudo snap install multipass
sudo apt-get -y install qemu-system-x86 gdb tmux
```

Pull requests are welcome. Examples of features to add:

 Add getopts-based command line argument handling.
- Add option for making system update-step optional.
- Add option for specifying a specific kernel to install.
- Add support for non-Ubuntu-based guests. For instance, CentOS: https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.2.2004-20200611.2.x86_64.qcow2
- Add option for normal boot instead of using init=/bin/bash when starting the
  emulator. Need to provide QEMU command line options for using the built-in
  DHCP server etc as well in that case.
- Determine the path to multipass instance data more reliably, rather than
  use a hardcoded path based on where it's installed by default when using
  "snap install multipass".

Example usage:

```bash
# Set up an Ubuntu 20.04-based VM and start a kernel source debugging session
./setup-kernel-debugging 20.04 dev

# The same as above, but with a specific "cloud image" URL
./setup-kernel-debugging \
  https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-amd64.img \
  dev
```

The second argument (i.e. "dev" in the examples above) is just the name to use
for the VM, and the directory where the files for the VM, as well as the scripts
to run it, will be placed.

Read the source.
