targetd
=======

Remote configuration of a LIO-based storage appliance
-----------------------------------------------------
targetd turns Linux into a remotely-configurable storage appliance. It
supports an HTTP/jsonrpc-2.0 interface to let a remote administrator
allocate volumes from an LVM volume group, and export those volumes
over iSCSI.

targetd development
-------------------
Contributions are welcome. targetd is licensed
under the GPLv3. Please use target-devel@vger.kernel.org for
discussion. Source repo and bug tracking is at
https://github.com/agrover/targetd.

**NOTE: targetd is STORAGE-RELATED software, and may be used to
  remove volumes without warning from the LVM volume group it is
  configured to use. Please take care in its use.**

Getting Started
---------------
targetd has these Python library dependencies:
* [targetcli] (https://github.com/agrover/targetcli-fb) (must be fb*)
* [python-rtslib](https://github.com/agrover/rtslib-fb) 2.1.fb14+  (must be fb*)
* [python-lvm](https://github.com/agrover/python-lvm) 1.2.2+
* [python-setproctitle](https://github.com/dvarrazzo/py-setproctitle)
* [PyYAML](http://pyyaml.org/)
* [python-tlslite](http://trevp.net/tlslite/)

All of these are available in Fedora Rawhide.

### Configuring targetd

A configuration file may be placed at `/etc/target/targetd.yaml`, and
is in [YAML](http://www.yaml.org/spec/1.2/spec.html) format. Here's
an example:

    pool_name: test
    user: "foo" # strings quoted, or not
    password: bar
    ssl: false
    target_name: iqn.2003-01.org.example.mach1:1234

targetd defaults to using the "vg-targetd" volume group, and username 'admin'
password 'targetd' for the HTTP jsonrpc interface.

Then, run `sudo ./targetd.py`.

client.py is a basic testing script, to get started making API calls.
