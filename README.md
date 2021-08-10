# xenbackup / xen-host-allbackup
XEN VM Backup Tool
------------------
XEN / LVM Host Auto-Snapshot-Backup for Xen DomUs (live and online)


It could be used to snapshot backup any kind of Xen DomU LVM volumes (Linux, FreeBSD, NetBSD and windows) and should work on products like Citrix XenServer (untested) too.

This Software provides easy automatic and grouped snapshot backups of LVM Volumes of hosted VMs and could be used even for other virtualization platforms with LVM backends (KVM / KQEMU and others). 

Currently it uses backup-manager to create and manage the tarballs, but could be modified to provide other kind of backup tools or just any suitable archivers up to rsync. If there is any real interest, i would add this.


HOW IT WORKS
------------
xenbackup backups Dom0 (root) as DomUs LVM volumes

xenbackup usually gets started by cron (i.e. daily)
`/etc/cron.daily/99_backup_iter`

where it mounts the backup medium (i.e. some umounted disk), creates temporary snapshots from the configured LVM volumes, mount it and read it by backup-manager tar incrementally. The increments could be changed in backup-manager.conf.

xenbackup works serial volume by volume to avoid any ressource exhaustion on dom0 (which is usually of small resource footprint).

when done, it unmounts all temporary mounted volumes and sends out an email with the log report.


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


CONFIGURATION
-------------

**/etc/xenbackup.conf**

you definitely have to adapt this settings to your setup and the directories (used mount points) should exist:
`
 # backup target device
BCKDEV="/dev/sdb2"
BCKDEV_FS="ext4"
`
if you change this settings:
`
 # backup device mount point
BCKMNTP="/backup/guests"

 # snapshots temp. mount directory
MNTSOURCEDIR="/4backup"
`

you have to make shure, the directories exist and adapt the pathes in /etc/backup-manager.conf as well!
`
there is no disk space used on dom0 for backup data during the backup process.

**/etc/xenback_vols**
add any volumes with required mount options (for the auto-created temporarily snapshot) to 
/etc/xenback_vols

`
mydomu1|root|/dev/vgxen/mydomu1-root|ext4|ro,noatime
mydomu2|var|/dev/vgxen/mydomu1-var||ufs|ro,ufstype=44bsd
...
`
in the format:

`DomU name|partition name|device file|fs-type|mount options (after -o - comma separated)`

important: you have to add some option to mount the snapshot read-only (i.e. ro) to avoid warnings in the log.

**/etc/backup-manager.conf**
the backup-manager config could be adapted as well if you're not satisfied with the defaults - i.e.:

``# Number of days we have to keep an archive (Time To Live)
export BM_ARCHIVE_TTL="5"

# At which frequency will you build your archives?
# You can choose either "daily" or "hourly".
# This should match your CRON configuration.
export BM_ARCHIVE_FREQUENCY="daily"
`


CHANGES
--------
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
