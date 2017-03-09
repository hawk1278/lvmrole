# README.md
# Ansible Role: lvmrole 1.0

This role is able to create a VG, create an LV, mount the fs and add permissions. Use booleans to activate/deactivate functions.

### Requirements

This role requires Ansible 2.2 or higher, and platform requirements are listed in the metadata file.

### Role Variables

Available variables are listed below, along with default values:

### Partitioning
Partitioning is handled by a separate role</br>

### Activate/Deactivate create VG/LV - fs manage
create_vg: false<br />
create_lv: false<br />
fs_manage: false<br />

### Load Profile - VG/LV
profile: empty

### Filesystem type depend on RHEL mayor version 
fstype_OS: rhel7-xfs/rhel6-ext4/rhel5-ext3  - or you can set with variable

### Profile example
        profile: list_name	
        list_name:
        -  pvname: "/dev/sdc1"
          vgname: VolumeGroupNameVG
          lvs:
            - { lvname: fs01_lv, size: 60G, fstype: "{{ fstype_OS }}", mntpoint: "/fs01", user: user, group: user }
            - { lvname: fs02_lv, size: 10G, fstype: "{{ fstype_OS }}", mntpoint: "/fs01/fs02", user: user, group: user }

### Dependencies
There is no dependencies with other roles.
 
### License
GPLv3
