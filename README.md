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
    ---
    - hosts: web
      become: true
      roles:
      - role: parted
        vars:
        - create_label: true
        - label: msdos
        - hdds:
          - /dev/xvdg
        - partitions:
          - {'partition_type':'primary','start_point':'0%','end_point':'100%'}
 
      - role: lvmrole
        create_vg: true
        create_lv: true
        fs_manage: true
        fstype_OS: ext4
        profile: apache
        apache:
        - pvname: "/dev/xvdg1"
          vgname: ApacheVG2
          lvs:
           - { lvname: webdata_lv, size: 100%FREE, fstype: "{{ fstype_OS }}", mntpoint: "/data1", user: root, group: root, mode: 770 }
          

### Dependencies
There is no dependencies with other roles.
 
### License
GPLv3
