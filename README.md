
williamyeh.ganglia-monitor for Ansible Galaxy
============


## Summary

Role name in Ansible Galaxy: **[williamyeh.ganglia-monitor](https://galaxy.ansible.com/list#/roles/XXXX)**

This Ansible role has the following features for [Ganglia Monitoring Daemon](http://ganglia.sourceforge.net/):

 - Install ganglia-monitor (Ganglia Monitoring Daemon; `gmond`).
 - Install several Python modules, if specified.
 - Bare bone configuration (*real* configuration should be left to user's template files; see **Usage** section below).

If you need full Ganglia stuff (such as `gmetad` and web frontend) or support for RedHat family, try alternatives roles in Ansible Galaxy, such as:

 - [micafer.ganglia](https://galaxy.ansible.com/list#/roles/1028)
 - [remysaissy.ganglia](https://galaxy.ansible.com/list#/roles/1258)



## Role Variables

### Mandatory variables

Variables needed to be defined in user's playbook: None.


### Optional variables

User-configurable defaults:

```yaml
# conf file (usually gmond.conf) to be installed,
# relative to `playbook_dir`;
# the file will be copied verbatim
ganglia_monitor_conf_copy

# conf file (usually gmond.conf.j2) to be installed,
# relative to `playbook_dir`;
# the file will be copied through Ansible's template system
ganglia_monitor_conf_template


# an array of official python modules to be installed;
# @see https://github.com/ganglia/monitor-core/tree/master/gmond/python_modules
ganglia_pymodules


# an array of python modules (provided in user's playbook) to be installed,
# relative to `playbook_dir`;
#
# fields: `name` and `dir`
# @see Repository of user-contributed Gmond Python DSO metric modules:
#      https://github.com/ganglia/gmond_python_modules
ganglia_extra_pymodules
```



## Handlers

- `restart ganglia-monitor`

- `stop ganglia-monitor`




## Usage


### Step 1: add role

Add role name `williamyeh.ganglia-monitor` to your playbook file.



### Step 2: copy user's config file, if necessary

Set vars in your playbook file.

```yaml
---
# file: simple-playbook.yml

- hosts: all

  roles:
    - williamyeh.ganglia-monitor

  vars:

    # copy verbatim
    ganglia_monitor_conf_copy: my-ganglia-files/gmond-deaf.conf

    # copy through Ansible's template system
    ganglia_monitor_conf_template: my-ganglia-files/gmond.conf.j2
```


### Step 3: install official modules, if any

More practical example:

```yaml
---
# file: average-playbook.yml

- hosts: all

  roles:
    - williamyeh.ganglia-monitor

  vars:
    ganglia_pymodules:
      - tcpconn
      - diskstat
      - vm_stats
```


### Step 4: install user-supplied modules, if any

More customized example:

```yaml
---
# file: complex-playbook.yml

- hosts: all

  roles:
    - williamyeh.ganglia-monitor

  vars:
    ganglia_extra_pymodules:
      - name: iface
        dir:  my-ganglia-files
        # remaining fields are ignored...
        description: metrics for all interfaces and counters of the /proc/net/dev file.
        source: https://github.com/ganglia/gmond_python_modules/tree/master/network/iface
```




## Dependencies

None.

Some Python modules may require runtime libs or executables pre-installed.  For example, the `tcpconn` module assumes that `netstat` be installed.  Therefore, you may need to `apt-get install net-tools` beforehand.


## License

Licensed under the Apache License V2.0. See the [LICENSE file](LICENSE) for details.
