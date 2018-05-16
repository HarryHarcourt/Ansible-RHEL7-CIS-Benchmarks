1.1.33 (2018-05-15)
* thorian93 (issue number 8) noted that sudo nolonger required to enter password after applying 5.3.2 task
* further investigation showed that the CIS Benchmarks recommendations were more reliable than RedHat
* Template updated and tested, all good again
* Will tidy up after feedback from thorian93 

1.1.32 (2018-05-14)
* Merging various commits from martinbaillie and thorian93
* martinbaillie - corrected code for hosts.allow to make a list in defaults/main.yml
* thorian93 - added code to include chronyd as a configuration option and a template file

1.1.31 (2018-04-28)
* Trying to fix merge from Martin by removing end of list spaces

1.1.30 (2018-04-28)
* Added support for CentOS by including it in vars/main.yml and following Martin Baillie merge request
* Tested on CentOS 7.4 and RHEL 7.4 and 7.5 on AWS AMI's - all seemed to work

1.1.29 (2018-04-28)
* Tested and added RHEL 7.5 for standard test configuration (as you see)

1.1.28 (2018-01-03)
* Creation of task 4.1.3 to address auditing in the grub file
* Creation of task 4.1.n to address 4.1.4 - 4.1.17 - no optional flags (although 4.1.10 is not completed yet)

1.1.27 (2018-01-02)
* Creation of task 4.1 which is an accumulation of 4.1.1.1 and 4.1.1.2, all auditd.conf options are included in the default/main.yml - using a template file
* Creation of task 4.1.2 which ensures that the auditd service is installed and is running

1.1.26 (2017-12-18)
* Updated task 1.4.2, more specificially the variable it calls in vars/main.yml for the boot loader /boot/grub2/grub.conf.  Previous entry has been commented out - brings the change in line with the CIS-CAT Tester
* Updated security options to bring in line with the CIS-CAT Tester, thus added additional variable, cis_passwd_hash and cis_pwretry_number, as well as updating the password-auth-local and system-auth-local template files

1.1.25 (2017-11-14)
* Updated task 4.3 for the logrotate configuration and added default variables and tested

1.1.24 (2017-11-13)
* Updated namespaces by adding cis_ at the front for future role integration on the following tasks, 2.2.1.2, 2.2.14, 3.1.1, 3.1.2, 3.2.1, 3.2.2, 3.2.3, 3.2.4, 3.2.5, 3.2.6, 3.2.7, 3.3.1, 3.3.2, 3.3.8
* Updated 6.1.6 to stat the file getting its mode first then, if it does not match 0600 it will change it (still having challenges with this file.....

1.1.23 (2017-09-19)
* Updated the meta/main.yml to change from RHEL to EL, reduced versions to just EL 7 (from 7.0, 7.1 etc, these are contained in the vars)
* Tested, loosely on RHEL 7.4 and it worked - need to do more testing - Ansible containers?

1.1.22 (2017-07-31)
* Commented out chage on 5.4.1.2 on last two sections, there should be a qualifier that checks if 7 is present before resetting the user because I think this does not let the user actually change their password if it is run within 7 days

1.1.21 (2017-07-21)
* Addressing 5.3.2 and 5.3.3 - because of nature merging them together into one template file
* Fixed white space from ansible-lint in 4.2.4
* Addressed "failed" in 5.1.8 if the file does not exist, test for presents and then chown, chmod
* Fixed 5.4.1.2 where stdout needed to be changed to stdout_lines for multiple users

1.1.20 (2017-07-19)
* Added variables for 5.3.2 and 5.3.3 for failed logins and password reuse to default/main.yml

1.1.9 (2017-07-18)
* 1.5.4 - prelink binary check - got rid of error message, but could not validate "installed" state to restore the prelink binaries prior to prelink removal

1.1.8 (2017-07-17)
* These are the modules that require idempotent changes: 
1.5.4 - prelink binary - challenge - trying to get rid of failed error message
* 4.2.1.1 - Check if rsyslog is installed - fixed by using yum module and the variable check in the defaults/main.yml
* 4.2.4 - Check log file permissions are configured - fixed, changed command to two part, find and then set using the file module
5.1.8 - Ensure cron/allow is restricted for authorized users, think same problem with ansible file module
* 6.1.6 - Ensure permissions on /etc/passwd- is set correct, problem with - at end of file name - fixed by wrapping the path in quotes


1.1.7 (2017-07-12)
* Tested against RHEL7, 7.1, 7.2 and 7.3
* Updated 1.2.2 to make idempotent, currently displaying the GPG Keys not validating them, how? Seems to only be oone set of keys as well, is this true with so many repositories? Display issue?

1.1.6 (2017-07-11)
* Updated 6.1.11, 6.1.12, 6.1.13 and 6.1.14 to changed_when false to stop changes appearing
* Updated the vars/main to be specific to RHEL and CentOS (will test at a later date)
* Updated the meta/main to include myself #:-) and update the versions it can be applied to

1.1.5 (2017-07-10)
* Updated for Ansible-lint to pass
 
1.1.4 (2017-06-23)
* Removed the ~ file from the default directory (sorry)
* 5.4.1.4 - updated the when clause on the set max password so that if there are no users it won't error out
* MOVING ALL MY CHANGES BELOW THIS ONE:
* Updated many of the tasks from 3.1.1 -> 3.3.2 and made them idempotent, thus they set the value in sysctl, then check the /proc values before setting the value in the kernel
* Updated many of the tasks from 2.1.1 -> 2.1.11 to make them idempotent, they will also take lead from the defaults where instead of disabling the services we remove their binaries
* Moved 2.1.11 to run before 2.1.1 because without the xinetd package installed you cannot configure the other bases services
* Updated NTP, and xorg-X11
* Updated multiple sections, Avahi, DHCP, OpenLDAP, CUPS, so the services can be installed and enabled if required
* Updated further sections, HTTP Servers, BIND, FTP, NFS and RPC
* Finished off the section 2.2.* stuff ran through and still so odd things so will validate over next couple of days
* Found error on the 3.1.1 -> 3.3.2 section, updated to include |bool at end of each when condition, enabled RedHat, 7.3 first
* Fixed issues required for our Security Values so that it is all Idempotent, however have concerns over the file module as I had to add a "changed_when" to stop it "changed"
* Updated 1.1.18 to remove changed status but added debug message to check for any errors
* Updated 1.1.18 to show what files are being set (thus idempotent)
* Currently an error on the Yum Repo check (for me)
* Uncommented other rules and ran through ok, there are still 1 which are not idempotent (1.2.2), and 2 which are fatal errors (1.5.4 - because of the way it checks for a binary, 5.1.8 - I think this is a file module bug) - one of these must also register a change
* Not sure if stable or not - passed through "ansible-lint" - corrected NTP and SNMP for octets in relation file permissions
* Also removed all white spaces at end of lines as per: find . -name \*.yml -exec sed -i '' -e 's/ $//' {} \;
* Needs testing but think foobar'd it when enabling checks
* Seems all clear with a couple of run throughs, enabled more but there are still a number of changes that need to be addressed
* Will fix my additions to change logs in next iteration
* Fixed 5.4.3 to make it idempotent and specific to the ask that GID of root is 0

1.1.3 (2017-01-10)

Enhancement:

* Refactored auditing shell scripts to add ability to handle commented entries in ```/etc/passwd``` and ```/etc/group```, as well as optimisation of loops. Credit: @lorensk
* Improve identification of information gathering tasks to ensure execution during check mode and idempotency. Credit: @lorensk
* Minor documentation fixes. Credit: @lorensk

1.1.2 (2017-01-05)

Enhancement:

* Refactor 6.2.x tasks to support running them in check mode. Credit: @jvgutierrez.
* Refactor 5.4.2 task to support running in check mode, as well as modify approach from passively flagging manual remediation activites, to actively locking system accounts. A new list ```cis_skip_lock_users``` can be defined to indicate which system accounts should not be locked. Credit: @jvgutierrez.

1.1.1 (2017-01-01)

Enhancement:

* Support running preflight checks over SSH. Credit: @jvgutierrez.
* Add '2016.09' to supported versions for Amazon in metadata.

1.1.0 (2016-12-02)

Bugfixes:

* #1 - Role now works with Ansible 2.2.0.

1.0.0 (2016-10-11)

* Initial release.


