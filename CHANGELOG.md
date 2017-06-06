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

1.0.1 (2017-05-07)

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
