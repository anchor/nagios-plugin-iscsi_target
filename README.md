# nagios-plugin-iscsi_target

## Overview 

A Nagios plugin to check the reachability of an iSCSI target.

The check is very basic and only attempts to ensure that the target is reachable and can be read from. The intended use case is a "dumb" initiator that has no access to the contents of the initiator, which may be a complex clustered filesystem or similar.

## Usage

The script takes a few arguments, also documented in the output of `--help`

        -n, --node      The name (IQN) of the target
        -a, --address   IP address of the target
        -p, --port      (Optional) Port to connect to on the target, defaults to 3260

### Example

* Typical usage

        check_iscsi_target  -n iqn.1992-01.com.example:backups.syd1  -a 172.16.1.1

* Configuration with non-standard port

        check_iscsi_target  -n iqn.1992-01.com.example:backups.rbx2  -a 172.19.40.17  -p 2501


## Configuration

There are no tuning options, though the script can be trivially edited if desired.

By default, we attempt to read 1 KiB of data from the device. If this doesn't succeed within 100ms we return a CRITICAL state.


## Bugs and limitations

We're not aware of any bugs, though the script is limited by its simplicity and may not work seamlessly on all systems.

* The script was written for [Open-iSCSI](http://www.open-iscsi.org/) and assumes that your initiator is already fully configured and working - this is a very high-level check.

* Targets are expected to be visible under `/dev/disk/by-path/ip-$address:$port-iscsi-$iqn-*`


## Author

Steven McDonald, for [Anchor](http://www.anchor.com.au/)

