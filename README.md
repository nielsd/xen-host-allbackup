# xenbackup / xen-host-allbackup
XEN VM Backup Tool
------------------
XEN / LVM Host Auto-Snapshot-Backup for Xen DomUs (live and online)


It could be used to snapshot backup any kind of Xen DomU LVM volumes (Linux, FreeBSD, NetBSD and windows) and should work on products like Citrix XenServer (untested) too.

This Software provides easy automatic and grouped snapshot backups of LVM Volumes of hosted VMs and could be used even for other virtualization platforms with LVM backends (KVM / KQEMU and others). 

Currently it uses backup-manager to create and manage the tarballs, but could be modified to provide other kind of backup tools or just any suitable archivers up to rsync. If there is any real interest, i would add this.


REQUIREMENTS
------------
 - install the "backup-manager" program
 - install "ssmtp" or any simple email sender program ("sendmail") for email notifications



INSTALLATION
------------
As root on the LVM Host system ("Dom0" in XEN):

 - copy files to the host system
 - edit config file /etc/xenbackup.conf
 - list your volumes in /etc/xenback_vols
 - check config of backup-manager /etc/backup-manager.conf (mainly point BM_REPOSITORY_ROOT="/backup/guests" to your real backup volumes mountpoint and/or adapt mountpoint in /etc/fstab)


CHANGES
----
This is productive software, but comes without any warranty!

1.2 RELEASE
 - bugfix in auto creation of mount dirs for new volumes


1.1 RELEASE
 - simplified config for more modern environments
 - mount / backup job delays
 - bug fixes

1.0a
 - single config file
 - generic pathes
 - strong code cleanout


DISCLAIMER
-----------
ANY USAGE ON YOUR OWN RISK!!!

BE AWARE IN CHANGING ANY OF THE BACKUP PATHES - DAMAGE OR DATA LOSS MAY HAPPEN IF YOU OVERWRITE YOUR HOST!!!
