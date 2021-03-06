Building a CentOS image
=======================

This repo contains packer templates and related files to build a CentOS image.

Available templates:

  * [CentOS x86_64 minimal with updates](centos-x86_64-updates.json)

The version of CentOS to install is defined by the `centos_version` parameter in the above templates. As of 2016-04-14 the default version is *7.2.1511*.

Here are the additions to the base install:

  * yum --releasever=7.2.1511 update
  * kernel-devel and kernel-headers are installed
  * EPEL repo is enabled
  * NTP is installed and enabled
  * Manpages are installed
  * SELinux is disabled
  * *UseDNS* and *PermitRootLogin* are both set to *no* in /etc/ssh/sshd_config
  * IPTables is open
  * For CentOS >=7, predictable interface names have been disabled (retaining the pre-7 behavior of ethN interface names)

Additional options can be included by specifying command line variables:

  * To download the iso from a different mirror: `-var iso_url=http://...`
  * To specify a different CentOS version: `-var centos_version=X.Y`
    * You will most likely also need to pass iso_checksum and iso_url
  * To set root's password hash: `-var root_hash='encrypted_string'`
  * To have sssd installed specify the location of an sssd.conf: `-var sssd_conf='/local/path/to/sssd.conf'`
  * An additional user-provided shell provisioner can be included: `-var custom_provisioner='/local/path/to/shell_script'`

Available builders:

  * [vbox4ami](AWS.md) - build an image (from scratch) suitable for AWS
  * [vbox4vagrant](VAGRANT.md) - build a Vagrant box for VirtualBox
  * [vbox4vbox](VIRTUALBOX.md) - build a box for VirtualBox
  * [vmware4vagrant](VAGRANT.md) - build a Vagrant box for VMware
  * [vmware4vmware](VMWARE.md) - build a box for VMware
