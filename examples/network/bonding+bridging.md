| NAME | DEFAULT | APPLIANCE | RACK | RANK | IP | MAC | INTERFACE | NETWORK | CHANNEL | OPTIONS | VLAN |
| ---- | ------- | --------- | ---- | ---- | -- | --- | --------- | ------- | ------- | ------- | ---- |
| node240 | TRUE | backend | 1 | 7 | 10.1.2.240 |  | br0 | private |  | bridge |  |
| node240 |  |  |  |  |  |  | bond0 |  | br0 | bonding-opts="mode=1 primary=em1" |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:a8 | em1 |  | bond0 |  |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:a9 | em2 |  | bond0 |  |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:aa | em3 |  |  |  |  |
| node240 |  |  |  |  |  | ec:f4:bb:d6:c3:ab | em4 |  |  |  |  |
