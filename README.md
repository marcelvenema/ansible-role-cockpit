# RedHat Cockpit

| ![Cockpit Icon](media/icon_cockpit.png) | Ansible role for installation and configuration of RedHat Cockpit, a web-based UI for managing RedHat servers. If detected, plugins for Podman and KVM virtual machines are automatically installed. The UI is accessible after installation via `https://<servername/ip>:9090`<br/><br/>Official website: `https://project-cockpit.org`
|---|---|

# Actions:


action: **install**
Installation of the latest Cockpit version. Basic configuration of Cockpit.
variables:
<kbd>cockpit_branding_logo</kbd> (optional) : Custom logo on the login page.
<kbd>cockpit_branding_banner</kbd> (optional) : Banner text file on the login page.

```
- name: Install and configure RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : install
```


action: **uninstall**
Uninstallation of RedHat Cockpit. Removal of configuration folder.
variables:
<kbd>(none)</kbd> : No variables required.

```
- name: Uninstall RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : uninstall
```



action: **configure**<br/>
Reconfiguration of RedHat Cockpit. `ROADMAP`.
variables:<br/>
<kbd>(none)</kbd> : No variables required.


action: **update**<br/>
Update of RedHat Cockpit.<br/>
variables:<br/>
<kbd>(none)</kbd> : No variables required.

```
- name: Update RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
       action : update
```

***

- **changelog**<br/>
  Change log.<br/>
  See [changelog](CHANGELOG.md)



- **roadmap**<br/>
  Vision and future developments.
  See [roadmap](ROADMAP.md)

***


## Preparations
(none).


## Dependencies
Dependencies are listed in the **requirements.yml** file. Use `ansible-galaxy install ./requirements.yml --force` for installation.
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
