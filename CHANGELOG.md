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


