# Aruba 6100 - Basic Switch Config Commands
---

### VLAN Reference

- Native
	- for frames that are not tagged
 - Allowed
	- for VLANs that are allowed over the specified trunk port (tagged or native)


---

## Keyboard Shortcuts (putty)
- ``?`` display a list of available commands for given context in detail
- ``Tab`` display available commands for given context
- ``Ctrl``+``S`` freeze terminal
- ``Ctrl``+``Q`` unfreeze terminal
- ``Ctrl``+``A`` go to beginning of input line
- ``Ctrl``+``E`` go to end of input line

---

## System Info/Config

## Startup Config
context: ``config``

### Save running-config to startup-config
```write memory```

### Reset startup-config to factory default config
```erase startup-config```

### Show current OS and BIOS info
```show version```

### Change default hostname
context: config

```6100(config)# hostname <new-hostname>```

Note: To be compliant with RFC 1123, the hostname must contain only letters, numbers and hyphens, and must not start or end with a hyphen.

---

## User Management
context: ``config``

### Change password
```user <name> password <ciphertext/plaintext> <password>```

### Create user
```user <name> group <administrators/auditors/operators> password <ciphertext/plaintext> <password>```

Default Privilege Levels:
- admin - 15
- op - 1
- audit - 19

[User Group Privileges](https://arubanetworks.com/techdocs/AOS-CX/10.07/HTML/5200-7885/Content/Chp_Mbg_Use/bui-in-use-gro-the-pri-10.htm)

### Delete user
```no user <name>```

### Show list of existing users
```show user-list```

### Show existing user-group info
```show user-group <groupname>```

### Delete user group
```no user-group <groupname>```

-----------------------------------------------

## Checkpoints

### Show existing checkpoints
context: ``config``

```show checkpoint list```

default checkpoint format: ``CPC yyyy/mm/dd hh:mm:ss``

### Delete specific checkpoint
``erase checkpoint <name>``

### Delete all checkpoints
``erase checkpoint all``

-------------------------------------------------

## VLAN

### Create VLAN
context: config

``6100(config)# vlan 200``

### Name VLAN
context: config-vlan-200

``6100(config-vlan-200)# name <VLAN-name>``

-----------------------------------------------

## Physical Interface (Ports)

context: config-int (e.g. int 1/1/1)

### Untagged (Native-untagged)
``6100(config-if)# vlan trunk native 200``

### Tagged (multiple)
``6100(config-if)# vlan trunk allowed 200``

### Untagged (single)
``6100(config-if)# vlan access 200``



vlan trunk allowed	tagged
vlan trunk native	untagged
vlan access		untagged



-----------------------------------------------

## IP & Web Interface

context: config-if-vlan

### Assign IP addr (to VLAN)
``6100(config-if-vlan)# ip address A.B.C.D/X``

### Allow access to web interface
``6100(config-if-vlan)# vlan trunk native 206``

### IP routing
``ip route 0.0.0.0/0 A.B.C.D``

-----------------------------------------------

## Clock / Timezone

### Set timezone
context: config

``6100(config)# clock timezone <region/timezone>``

e.g.
``6100(config)# clock timezone asia/karachi``

### Display clock
``6100(config)# show clock``

output 	>> Sun Jul 23 15:10:07 PKT 2023
	>> System is configured for timezone : Asia/Karachi

-----------------------------------------------

## Basic security measures

### Session timeout
context: config-cli-session

``6100(config)# cli-session``
``6100(config-cli-session)# timeout <time in minutes 0-43200>``

### Display session timeout
``6100(config-cli-session)# show session-timeout``
output 	>> ``session-timeout: 15 minutes``


-----------------------------------------------














































