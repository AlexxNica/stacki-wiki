| NAME | DEFAULT | APPLIANCE | RACK | RANK | IP | MAC | INTERFACE | NETWORK | CHANNEL | OPTIONS | VLAN |
| ---- | ------- | --------- | ---- | ---- | -- | --- | --------- | ------- | ------- | ------- | ---- |
| node219 | TRUE | backend | 1 | 9 | 10.1.2.219 | 90:b1:1c:09:eb:af | eno1 | private |  |  |  |
| node219 |  |  |  |  |  | 90:b1:1c:09:eb:b0 | eno2 |  |  |  |  |
| node219 |  |  |  |  |  | 90:b1:1c:09:eb:b1 | eno3 |  | bond0 |  |  |
| node219 |  |  |  |  |  | 90:b1:1c:09:eb:b2 | eno4 |  | bond0 |  |  |
| node219 |  |  |  |  |  |  | bond0 |  | br0 | bonding-opts="mode=1 primary=eno3" |  |
| node219 |  |  |  |  |  |  | br0 |  |  | bridge |  |
| node219 |  |  |  |  | 10.11.2.219 |  | br0.77 | vlad |  |  | 77 |
| node240 | TRUE | backend | 1 | 7 | 10.1.2.240 | ec:f4:bb:d6:c3:a8 | em1 | private |  |  |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:a9 | em2 |  |  |  |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:aa | em3 |  | bond0 |  |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:ab | em4 |  | bond0 |  |  |
| node240 |  |  |  |  |  |  | bond0 |  | br0 | bonding-opts="mode=1 primary=em3" |  |
| node240 |  |  |  |  |  |  | br0 |  |  | bridge |  |
| node240 |  |  |  |  | 10.11.2.240 |  | br0.77 | vlad |  |  | 77 |
