HarryHarcourt.Ansible-RHEL7-CIS-Benchmarks
=========

All Credit goes to anthcourtney for the original framework found here: https://github.com/anthcourtney/ansible-role-cis-amazon-linux

This implementation has been converted to Red Hat Enterprise Linux 7.X (tested 7.0 - 7.5) and CentOS 7.4 (note CentOS version below 7.4 may have issues with SSH). 

This implementation has been made idempotent in many places, and continues to be

This implementation allows the enabling of and configuration of some services.

The CIS RHEL Linux Benchmark. <https://benchmarks.cisecurity.org/tools2/linux/CIS_Red_Hat_Enterprise_Linux_7_Benchmark_v2.1.1.pdf>

This role was developed and tested against Red Hat Linux 7.0, 7.1, 7.2, 7.3, 7.4 and 7.5 using standard AWS AMI's.
This role was developed and tested against CentOS 7.4 using standard AWS AMI's.

Why Would I Use This Role?
--------------------------

If you are attempting to obtain compliance against an industry-accepted security standard, like PCI DSS, APRA or ISO 27001, then you need to demonstrate that you have applied documented hardening standards against all systems within scope of assessment.

If you are running Red Hat Linux, then this role attempts to provide one piece of the solution to the compliance puzzle.

Here Be Dragons!
----------------

If you are considering applying this role to any servers, you should have a basic familiarity with the CIS Benchmark (or other similar benchmarks) and an appreciation for the impact that it may have on a system.

Please take the time to familarise yourself with the standard and with the configurable default values, and exclude any items before applying to a system.

An examples of items that should be immediately considered for exclusion (or at least, for modification of the related default values) include:

* ```3.4.2``` and ```3.4.3```, which by default effectively limit access to the host (including via ssh) to localhost only.

Example Playbook
----------------

An example playbook which uses this role is as follows:

```
---

- hosts: localhost
  connection: local
  gather_facts: true
  become: yes

  roles:
    - Ansible-RHEL7-CIS-Benchmarks 
```

A more advanced example, which includes modifications to the default values used, as well as the exclusion of some items in the benchmark which are considered unnecessary for a fictional environment, is as follows:

```
---

- hosts: localhost
  connection: local
  gather_facts: true
  become: yes

  vars:
    cis_level_1_exclusions:
      - 5.4.4
      - 3.4.2
      - 3.4.3
      - 6.2.13   
    cis_pass_max_days: 45
    cis_umask_default: 002
 
  roles:
    - Ansible-RHEL7-CIS-Benchmarks

```

Note that the use of ```become: yes``` is required as 99% of tasks require privileged access to execute.

Role Variables
--------------

See ```defaults/main.yml``` for variables which can be overriden according to preference.

Options
-------

Tags (and combinations thereof) can be used to run a particular level of the CIS standard, a section, or an individual recommendation. For example:

* Run only Level 1 tasks

```
ansible-playbook playbook.yml -t level-1
```

* Run only Section 3 tasks

```
ansible-playbook playbook.yml -t section-3
```

* Run tasks 1.3.1 and 2.2.10 only

```
ansible-playbook playbook.yml -t 1.3.1,2.2.10
```

* Run scored tasks only

```
ansible-playbook playbook.yml -t scored
```

Limitations
-----------

At present, only the Level 1 items of the benchmark are implemented. Level 2 items will be added as time permits.

The following checks have not been implemented:

* 3.6.2. Firewall rulesets are environment specific.
* 3.6.3. Firewall rulesets are environment specific.
* 3.6.4. Firewall rulesets are environment specific.
* 3.6.5. Firewall rulesets are environment specific.
* 4.2.1.2. The determination of what should be logged and the destination of messages is environment specific.
* 4.2.2.2. The determination of what should be logged and the destination of messages is environment specific.
* 4.2.2.3. Inline editing of syslog-ng configuration file is considered too imprecise and is best solved by a supplied configuration file which addresses this and other related requirements.
* 4.2.2.4. Inline editing of syslog-ng configuration file is considered too imprecise and is best solved by a supplied configuration file which addresses this and other related requirements.
* 4.2.2.5. Inline editing of syslog-ng configuration file is considered too imprecise and is best solved by a supplied configuration file which addresses this and other related requirements.
* 4.3. The configuration of logrotate is site-specific.
* 5.3.2. Multi-line editing of pam configuration files is considered too imprecise and dangerous, and is best solved by a supplied configuration file which addresses this and other related requirements.
* 5.3.3. Multi-line editing of pam configuration files is considered too imprecise and dangerous, and is best solved by a supplied configuration file which addresses this and other related requirements.

Compatibility
-------------

This role is compatible with the following versions of ansible:

* 2.0.2
* 2.1.3
* 2.2.0
* 2.3.0

This role has not been tested against any other versions of ansible.

Testing
-------

The following testing processes are applied by the developer of this role:

* The syntax of the role is checked. See ```make syntax```.
* ```ansible-review``` is run against the role and any warnings which are deemed appropriate are remediated. See ```make review```.
* The role is applied against a docker container using both ansible v2.1.3 and ansible v2.2. see ```make test```.

The following tests have been flagged but are not yet implemented:

* Test application of the role against the Vagrant ```mvbcoding/awslinux``` image, using the ansible provisioner.

License
-------

BSD. 

Author Information
------------------

The role was originally developed by [Anth Courtney](https://au.linkedin.com/in/anthcourtney).

This role was further developed by [Ben Wright](https://www.linkedin.com/in/ben-wright-4a088033).

All feedback, issues and PRs are encouraged and appreciated.
