
A Stacki frontend can be installed on top of an existing Red Hat based server. The server must be running the x86_64 version of CentOS or RHEL 7.x.

**__REALLY IMPORTANT__**: During the Stacki installation it is possible that Stacki will overwrite certain system files.  Please don't install onto an existing production server without prior testing.

To perform this installation, log into the frontend and download two pallets and one RPM

**_IMPORTANT_**: It is very important that you supply the _stacki_ ISO and not the _stackios_ ISO. Very.

1. **Stacki ISO**. Download the Stacki ISO and put it on the server you want as the Stacki frontend.

    * [Stacki 5.0 (built for CentOS 7.x)](http://teradata-stacki.s3.amazonaws.com/release/stacki/5.x/stacki-5.0_20171128_b0ed4e3-redhat7.x86_64.disk1.iso) (md5: f4c021dd6d7febe1b72a2a8cb81c8a81)

2. **OS Pallet** You'll need to download ONE of the following OS pallets:

      * [The minimal OS (for stacki 5.0 - minimal CentOS 7.4)](http://teradata-stacki.s3.amazonaws.com/release/stacki/5.x/os-7.4_20171128-redhat7.x86_64.disk1.iso)
      * [CentOS 7.4](https://www.centos.org/download/mirrors/) Use the "Everything" or "DVD" ISOs.
      * Oracle Linux 7.4 - You have a subscription right?
      * RedHat 7.4. - You have subscription right?
      * Scientific Linux - It's out there somewhere. Someone used to use it.

3. **stacki-fab RPM**. Download the [stacki-fab RPM](http://teradata-stacki.s3.amazonaws.com/release/stacki/5.x/stacki-fab-5.0_20171213_56d2cb1-all.x86_64.rpm) and put it on the server you want to transform into a Stacki frontend.

Install the `stacki-fab` RPM:

    # rpm -i stacki-fab-5.x_*-all.x86_64.rpm

This installs a program call frontend-install.py, which you will invoke to
install Stacki.

"cd" to the directory where you have downloaded your stacki and OS isos.

Execute frontend-install.py:

    # /opt/stack/bin/frontend-install.py --stacki-iso=stacki-5.0_20171128_b0ed4e3-redhat7.x86_64.disk1.iso

Using just the stacki iso will create a frontend but then you have to add an OS pallet after the reboot. To shortcut that step, add an os pallet on the command line with the "--extra-iso" option and supply any OS pallets you have:

With minimal OS pallet:

    #  /opt/stack/bin/frontend-install.py --stacki-iso=stacki-5.0_20171128_b0ed4e3-redhat7.x86_64.disk1.iso --extra-iso=os-7.4_20171128-redhat7.x86_64.disk1.iso

With the full CentOS iso ( or rhel-server iso or Oracle etc.)

    #  /opt/stack/bin/frontend-install.py --stacki-iso=stacki-5.0_20171128_b0ed4e3-redhat7.x86_64.disk1.iso --extra-iso=CentOS-7-x86_64-Everything-1708.iso

  You can also add the updates pallet while you're at:

    #  /opt/stack/bin/frontend-install.py --stacki-iso=stacki-5.0_20171128_b0ed4e3-redhat7.x86_64.disk1.iso --extra-iso=CentOS-7-x86_64-Everything-1708.iso,CentOS-Updates-7.4_20171128-redhat7.x86_64.disk1.iso

If you want to use the current network, route, DNS, timezone, root password and do not want to use the wizard, throw the ""--use-existing" option:

With minimal OS pallet and "--use-existing":

    #  /opt/stack/bin/frontend-install.py --stacki-iso=stacki-5.0_20171128_b0ed4e3-redhat7.x86_64.disk1.iso --extra-iso=os-7.4_20171128-redhat7.x86_64.disk1.iso --use-existing


If you have not used the "--use-existing command", the above any of the previous steps display the [Installation Wizard](#installation-wizard) to set system configuration including: network, password, timezone, pallets, and partitioning.

## Installation Wizard

The Installation Wizard is the same for either the New or the Existing installation methods. The installation that happens after going through the wizard is either a typical CentOS/RHEL server install (New) or a set of scripts that run to create the Stacki software stack (Existing).

The Installation Wizard is now text-based, because, The 90s!

## Timezone

The first screen will appear and you will be prompted to enter your timezone:

![frontend_install_vbox_8](images/frontend/frontend_install_vbox_8.png)

## Network

_**Do not get this network wrong! Changing it after the fact means a RE-INSTALL of the frontend.**_

The network configuration screen allows you to set up the network that will
be used by the frontend to install backend hosts.

1. _Fully Qualified Host Name_ - Input the FQDN for the frontend.
2. Choose from the network _Devices_ to select the frontend's network interface.
3. _IP_ address of the interface.
4. _Netmask_.
5. _Gateway_.
5. _DNS Servers_ - More than one DNS Server can be entered as a comma-separated list (i.e., 8.8.8.8, 4.2.2.2, 8.8.4.4).

Click _Continue_ to configure the network interface.

![frontend_install_vbox_10](images/frontend/frontend_install_vbox_10.png)

## Password

Enter the password for the **root** account on the frontend.  This is also the root password for the backend nodes. Choose a better one than shown here.

![frontend_install_vbox_11](images/frontend/frontend_install_vbox_11.png)

## Choose Partition

If _Automated_ mode is selected, the installer will
repartition and reformat the first discovered hard drive
that is connected to the frontend. All other drives
connected to the frontend will be left untouched.

| Partition Name                                     | Size                   |
|:---------------------------------------------------|:-----------------------|
| /                                                  | 16GB                   |
| /var                                               | 16GB                   |
| swap                                               | 1GB                    |
| /export (symbolically linked to /state/partition1) | remainder of root disk |

When using automatic partitioning, the installer repartitions
and reformats the first hard drive (e.g. _sda_) that the installer
discovers. All previous data on this drive will be erased.
All other drives will be left untouched. If you are unsure about how
the drives will be discovered in a multi-disk frontend,
select _Manual_ mode.

In _Manual_ mode, the installer brings up a partition setup
screen after the wizard exits. In this mode, specify at least 16 GB
for the root partition and a separate /export partition - which should be the largest partition. You should add a swap partition, and /var if you have made / only 16GB.

## Add Pallets

Choose the _Pallets_ you want to install.

Booting from a DVD/USB, pallets should automatically load onto the list for you to choose.

** Please note:** In an Existing installation you will only see the stacki pallet - even if you have supplied the --extra-isos parameter.

In a New installation with the stackios pallet, you should see two pallets: the the _stacki_ and _os_ pallets to install.

If you want to add pallets from another Stacki frontend or from a webserver hosting pallet ISOs, Choose _Add Pallets_ and supply the correct url. Once you've added all the pallets, choose _Continue_

![frontend_install_vbox_13](images/frontend/frontend_install_vbox_13.png)


## Summary

Review the installation parameters and click _Continue_ to proceed.

![frontend_install_vbox_14](images/frontend/frontend_install_vbox_14.png)


Once the install is done, you will be prompted to reboot. Reboot.

    # reboot

## Verify
Once the frontend is up, check to make sure you have what you think you have:

You should see one host:

```
# stack list host
HOST        RACK RANK APPLIANCE OS     BOX     ENVIRONMENT OSACTION INSTALLACTION STATUS COMMENT
stacki50    0    0    frontend  redhat default ----------- default  default       up
```

And you should see two pallets:

```
# stack list pallet
NAME   VERSION              RELEASE ARCH   OS     BOXES
os     7.4_20171128         redhat7 x86_64 redhat default
stacki 5.0_20171128_b0ed4e3 redhat7 x86_64 redhat default
```

Your Stacki frontend is now ready to [install backend servers](Backend-Installation).

** However **

If you didn't supply an OS pallet with the "--extra-iso" option to frontend-install.py, and if you only see the stacki pallet:

```
# stack list pallet
NAME   VERSION              RELEASE ARCH   OS     BOXES
stacki 5.0_20171128_b0ed4e3 redhat7 x86_64 redhat default
```

You need to add an **OS pallet**.

The OS pallet is used as the base OS to install onto the backend nodes.
This will be either the CentOS installation DVD(s) or the Red Hat installation DVD.

To add an ISO pallet to the Stacki Frontend, using OS minimal, first download the OS minimal iso to the frontend, then execute:

```
# stack add pallet os-7.4_20171128-redhat7.x86_64.disk1.iso
```

Then _enable_ the 'os' pallet. This makes the 'os' repository on the Stacki frontend available for backend installs:

```
# stack enable pallet os
# stack list pallet
```

Should produce output similar to:

```
NAME   VERSION              RELEASE ARCH   OS     BOXES
os     7.4_20171128         redhat7 x86_64 redhat default
stacki 5.0_20171128_b0ed4e3 redhat7 x86_64 redhat default
```

And now Your Stacki frontend is now ready to [install backend servers](Backend-Installation).
