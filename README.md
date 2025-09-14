# 4100i, 6000, 6100 Switch Series - Basic Configuration Commands
---

### Common Terminology

- **Trunk**
	- Processes **tagged** frames only
	- Can pass/transmit traffic from *multiple* VLANs
	- Offer higher bandwidth and lower latency than access ports
	- Typically for linking switches

- **Access**
	- Only sends and receives frames that are **untagged** (and only those which have the access VLAN number)
	- Accepts traffic only for a *single* VLAN
  	- Typically for linking end-user devices (these are usually not 'VLAN-aware')

---

- Trunk ***Allowed***
	- For allowing specified VLANs through a trunk port

- Trunk ***Native***
	- A native VLAN is one that is associated with all untagged traffic on a trunk port
  	- A trunk port can only contain 1 native VLAN at a time
	- Default: VLAN 1

```
vlan trunk allowed	tagged
vlan trunk native	untagged
vlan access		untagged
```

---

## Keyboard Shortcuts (putty)
- ``?`` display a list of available commands for given context in detail
- ``Tab`` display available commands for given context
- ``Ctrl``+``S`` freeze terminal
- ``Ctrl``+``Q`` unfreeze terminal
- ``Ctrl``+``A`` go to beginning of input line
- ``Ctrl``+``E`` go to end of input line

---

# System Info/Config

## Startup Config
context: ``config``

### Save running-config to startup-config
```write memory```

### Reset startup-config to factory default config
```erase startup-config```

### Show current OS and BIOS info
```show version```

### Change default hostname
context: ``config``

```6100(config)# hostname <new-hostname>```

Note: To be compliant with RFC 1123, the hostname must contain only letters, numbers and hyphens, and must not start or end with a hyphen.

---

## User Management
context: ``config``

### Change password
```user <name> password ( ciphertext | plaintext ) <password>```

### Create user
```user <name> group ( administrators | auditors | operators ) password ( ciphertext | plaintext ) <password>```

- Default Privilege Levels:
	- admin - 15
	- op - 1
	- audit - 19

- [User Group Privileges](https://arubanetworks.com/techdocs/AOS-CX/10.07/HTML/5200-7885/Content/Chp_Mbg_Use/bui-in-use-gro-the-pri-10.htm)

### Delete user
```no user <name>```

### Show list of existing users
```show user-list```

### Show existing user-group info
```show user-group <groupname>```

### Delete user group
```no user-group <groupname>```

---

## Checkpoints

### Show existing checkpoints
context: ``config``

```show checkpoint list```

default checkpoint format: ``CPC<YYYYMMDD><hh:mm:ss>``

### Delete specific checkpoint
``erase checkpoint <name>``

### Delete all checkpoints
``erase checkpoint all``

---

## VLAN

### Create VLAN
context: ``config``

```6100(config)# vlan 100```

### Name VLAN
context: ``config-vlan-100``

```6100(config-vlan-100)# name <VLAN-name>```

---

## Physical Interface (Ports)

context: ``config-int`` (e.g. ``int 1/1/1``)

### Trunk - Native
```6100(config-if)# vlan trunk native 100```

### Trunk - Allowed, Single
```6100(config-if)# vlan trunk allowed 100```

### Trunk - Allowed, Multiple
```6100(config-if)# vlan trunk allowed 100, 200, 300```

### Access
``6100(config-if)# vlan access 100``

---

## IP & Web Interface

context: config-if-vlan

### Assign IP addr (to VLAN)
``6100(config-if-vlan)# ip address ( A.B.C.D/X | A.B.C.D W.X.Y.Z )``

### Allow access to web interface
``6100(config-if-vlan)# vlan trunk native 206``

### IP routing
``ip route 0.0.0.0/0 A.B.C.D``

---

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

---

## Basic security measures

### Session timeout
context: config-cli-session

``6100(config)# cli-session``
``6100(config-cli-session)# timeout <time in minutes 0-43200>``

### Display session timeout
``6100(config-cli-session)# show session-timeout``
output 	>> ``session-timeout: 15 minutes``

---

# References

https://documentation.meraki.com/General_Administration/Tools_and_Troubleshooting/Fundamentals_of_802.1Q_VLAN_Tagging

https://www.n-able.com/blog/vlan-trunking

    AOS-CX-10-08 was used as reference
