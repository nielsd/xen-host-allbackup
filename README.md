# xen-host-allbackup
XEN / LVM Host Auto-Backup for Xen DomU (live and online)
(version 0.5)


It could be used to snapshot backup any kind of LVM.

This Software provides easy automatic snapshot backups of LVM Volumes of hosted VMs. 

Currently it uses backup-manager to create and manage the tarballs, but could be modified to provide other kind of backup tools or just any suitable archivers up to rsync. If there is any real interest, i would add this.


REQUIREMENTS
------------
 - install the "backup-manager" program
 - install "ssmtp" or any simple email sender program for email notifications


INSTALLATION
------------
As root on the LVM Host system ("Dom0" in XEN):

 - open the scripts in /usr/local/sbin/ and adapt the config sections
 - copy files to the host system
 - list your volumes in /etc/xenback_vols
 - check config of backup-manager /etc/backup-manager.conf (mainly point BM_REPOSITORY_ROOT="/backup/guests" to the "BCKMNTP" mountpoint in the scripts)


TODO
----
This is very early, but working, software.

 - single config file
 - make more generic (name and docs independent from Xen)


DISCLAIMER
-----------
ANY USAGE ON YOUR OWN RISK!!!

BE AWARE IN CHANGING ANY OF THE BACKUP PATHES - DAMAGE OR DATA LOSS MAY HAPPEN IF YOU OVERWRITE YOUR HOST!!!
