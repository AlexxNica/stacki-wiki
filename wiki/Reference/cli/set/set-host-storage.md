## set host storage

### Usage

`stack set host storage [host ...] {action=string} {enclosure=string} {slot=string}`

### Description


	Set state for a storage device for hosts (e.g., to change the state
	of a disk from 'offline' to 'online').

	

### Arguments

* `{host}`

   Zero, one or more host names. If no host names are supplied, this
	command will apply the state change to all known hosts.


### Parameters
* `[action=string]`
* `[enclosure=string]`
* `[slot=string]`

   An integer id for the slot that contains the storage device.

### Examples

* `stack set host storage backend-0-0 enclosure=32 slot=5  action=online`

   Set the storage device located at '32:5' to "online" for backend-0-0.



