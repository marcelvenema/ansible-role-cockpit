# role: RedHat Cockpit

<table style="border:0px; width:100%"><tr><td width=160px valign=top><img src="media/icon_cockpit.png" alt="Cockpit icon" width=128 height=128></td>
<td>
Ansible role for installation, configuration, usage and management of RedHat Cockpit, a web-based UI for managing RedHat servers. If detected, plugins for Podman and KVM virtual machines are automatically installed. The UI is accessible after installation via `https://(servername/ip-address):9090`<br><br>Official website: `https://project-cockpit.org`<br><br>
</td>
</tr></table>

Ansible role Cockpit : [Design](docs/DESIGN.md)  |  [Examples](examples)  |  [Test](molecule)  |  [Issues]()  |<br>
Latest version:

# Actions:

<table style="border:0px; width:100%">
<tr><th>Deployment</th><th>Administration</th></tr>
<tr>
  <td valign=top>install<br>uninstall<br>update</td>
  <td valign=top>configure<br>start<br>stop<br></td>
</tr></table>

## Deployment

action: **install**<br>
Installation of the latest Cockpit version. Basic configuration of Cockpit.<br>
variables:<br>
<kbd>cockpit_branding_logo</kbd> (optional) : Custom logo on the login page.<br>
<kbd>cockpit_branding_banner</kbd> (optional) : Banner text file on the login page.<br>
<kbd>uninstall</kbd> (optional) : Uninstall existing Cockpit instance before installation.<br>

```
- name: Install and configure RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : install
```


action: **uninstall**<br>
Uninstallation of RedHat Cockpit. Removal of configuration folder.<br>
variables:<br>
<kbd>remove_data</kbd> (optional) : Remove all Cockpit data during uninstallation.<br>

```
- name: Uninstall RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : uninstall
```


action: **update**<br>
Update of RedHat Cockpit.<br>
variables:<br>
<kbd>backup_config</kbd> (optional) : true/false. Backup configuration before update.<br>
<kbd>notify_users</kbd> (optional) : true/false. Notify users before update.<br>

```
- name: Update RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : update
```


## Administration

action: **start**<br>
Start of Cockpit service. `ROADMAP`.<br>
variables:<br>
<kbd>(none)</kbd> : No variables required.<br>

```
- name: Start Cockpit service
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : start
```


action: **stop**<br>
Stop of Cockpit service. `ROADMAP`.<br>
variables:<br>
<kbd>(none)</kbd> : No variables required.<br>

```
- name: Stop Cockpit service
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : stop
```


action: **configure**<br>
Reconfiguration of RedHat Cockpit. `ROADMAP`.<br>
variables:<br>
<kbd>cockpit_branding_logo</kbd> (optional) : Custom logo on the login page.<br>
<kbd>cockpit_branding_banner</kbd> (optional) : Banner text file on the login page.<br>

```
- name: Configure Cockpit service
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : configure
```


***

- **changelog**<br>
  Change log.
  See [changelog](CHANGELOG.md)

- **roadmap**<br>
  Vision and future developments.
  See [roadmap](ROADMAP.md)

***

## Preparations
(none).


## Dependencies
Dependencies are listed in the **requirements.yml** file.<br>
Use `ansible-galaxy install ./requirements.yml --force` for installation.<br>
If this role is used in other playbooks or Ansible projects, the URL of this role must be added to the `requirements.yml` file. Using the above command, the role will be placed in the correct folder structure.


## Installation and configuration
Installation via the action variable <kbd>install</kbd>. (Re-)configuration via the action variable <kbd>configure</kbd>.

When using this role in other playbooks or Ansible projects:
```
- name: Install and configure RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : install
```


When used as a stand-alone Ansible project:
```
- name: Install and configure RedHat Cockpit
  hosts: localhost
  tasks:

    - name: Install RedHat Cockpit
      ansible.builtin.include_tasks:
        file: tasks/install.yml
```

## Additional information
The UI is accessible via `https://<servername/ip>:9090`. The username for login must be a member of the local administrator group.

## License
MIT

## Author
Marcel Venema
