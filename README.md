# vulndev-tools

Just a repository for random tools that can be helpful during vulnerability
research and exploit development. For now, it only contains a script to set up
a kernel debugging environment.

![setup-kernel-debugging](setup-kernel-debugging.gif)

The tool works as-is for setting up kernel debugging environments for (at
least) Ubuntu 14.04, 16.04, 18.04 and 20.04 kernels right now, and would be
easy to adapt to support non-Ubuntu-based Linux distributions as well (would
need some adaptations for each dist).

Dependencies: Multipass (https://multipass.run), QEMU, GDB and tmux.

To install dependencies under Ubuntu:
```bash
sudo snap install multipass
sudo apt-get -y install qemu-system-x86 gdb tmux
```

Pull requests are welcome. Examples of features to add:

- Add getopts-based command line argument handling.
- Add option for making system update-step optional.
- Add option for specifying a specific kernel to install.
- Add support for non-Ubuntu-based guests. For instance, CentOS:
  https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.2.2004-20200611.2.x86_64.qcow2
- Add check for each of the dependencies, and for supported hosts, check for
  sudo-access and automatically install the required dependencies.
- Add option for normal boot instead of using init=/bin/bash when starting the
  emulator. Need to provide QEMU command line options for using the built-in
  DHCP server etc as well in that case.
- Determine the path to multipass instance data more reliably, rather than
  use a hardcoded path based on where it's installed by default when using
  "snap install multipass".
- Add option and/or environment variable for the GDB server port to use, rather
  than the default 1234 (to allow for parallell kernel debugging environments
  running).
- Feed customized cloud-init configuration to multipass launch, to set a
  password etc (comes in handy if we boot interactively in QEMU for a
  kernel-debugging session, rather than just use init=/bin/bash)

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
