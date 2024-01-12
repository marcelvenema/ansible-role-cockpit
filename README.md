# RedHat Cockpit

<table border="0">
  <tr>
    <td width="160px" valign="top"><img src="media/icon_cockpit.png" align="left" height="128" width="128" /></td>
    <td>Ansible role voor installatie en configuratie van Redhat Cockpit, een webbased UI voor het beheer van Redhat servers.<br/> 
        Indien gedetecteerd, worden plugins voor Podman en KVM virtuele machines automatisch geinstalleerd.<br/>
        De UI is na installatie bereikbaar via `https://<servernaam/ip>:9090`<br/>
        <br/>
        Website leverancier: `https://project-cockpit.org`<br/>
        <br/>
    </td>
  </tr>
</table>

# Diensten:


action: **install**<br/>
Installatie van laatste Cockpit versie. Basis configuratie van Cockpit.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>

Voorbeeld:
```
- name: Install and configure RedHat Cockpit
  hosts: localhost
  roles:
   - role: cockpit
     vars:
      action        : install

```


action: **uninstall**<br/>
De-installatie van RedHat Cockpit. Verwijderen configuratie folder.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **configure**<br/>
Her-configuratie van RedHat Cockpit. `ROADMAP`.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>


action: **update**<br/>
Update van RedHat Cockpit.<br/>
variablen:<br/>
<kbd>(geen)</kbd> : Geen variabelen benodigd.<br/>
<br/>







Bij installatie worden volgende configuratie instellingen gedaan:<br />
- Tonen banner tekst bij login pagina.<br />
  Tekst in banner_cockpit.txt bestand in ./media folder.<br/>
- Aanpassen custom logo bij login pagina.<br/>
  Logo in media folder, media/logo_cockpit.png bestand.<br/>


***

- **changelog**<br/>
  Wijzigingen logboek.<br/>
  Zie [changelog](CHANGELOG.md)<br/>



- **roadmap**<br/>
  Visie en toekomstige ontwikkelingen.<br/>
  Zie [roadmap](ROADMAP.md)<br/>


***


## Voorbereidingen
(geen).<br/>


## Afhankelijkheden
Afhankelijkheden zijn benoemd in het **requirements.yml** bestand. Gebruik `ansible-galaxy install ./requirements.yml --force` voor installatie.<br/>


## Installatie en configuratie
Installatie via action 'install'. (Her-)configuratie via action 'configure'.<br/>
Voorbeeld voor installatie RedHat Cockpit:

```
---

- hosts: lab_server
  vars:
  roles:
    - role: cockpit
      vars:
        action : install

```


## Overige informatie
De UI is bereikbaar via `https://<servernaam/ip>:9090`. Gebruikersnaam voor login dient lid te zijn van lokale administrator groep. 


## Licentie
MIT


## Auteur
Marcel Venema
