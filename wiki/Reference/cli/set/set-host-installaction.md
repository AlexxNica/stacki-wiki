## set host installaction

### Usage

`stack set host installaction {host ...} {action=string}`

### Description


	Set the install action for a list of hosts.
	
	

### Arguments

* `[host]`

   One or more host names.


### Parameters
* `[action=string]`

   The install action to assign to each host. To get a list of all actions,
	execute: "stack list bootaction".

### Examples

* `stack set host installaction backend-0-0 action=install`

   Sets the install action to "install" for backend-0-0.

* `stack set host installaction backend-0-0 backend-0-1 action="install i386"`

   Sets the install action to "install i386" for backend-0-0 and backend-0-1.



