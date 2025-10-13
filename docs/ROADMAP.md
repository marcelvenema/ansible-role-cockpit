# Vision

| ![Cockpit Icon](media/icon_cockpit.png) | Ansible role for installation and configuration of RedHat Cockpit, a web-based UI for managing RedHat servers. If detected, plugins for Podman and KVM virtual machines are automatically installed.
|---|---|

***

# Roadmap


## Near-term (next releases)

- Automatic updates and kpatch toggles
	- Add defaults under `cockpit.application.updates` and `cockpit.application.kpatch` (e.g., `apply_updates`, `upgrade_type`, `emit_via`, `enabled`) to parameterize the existing tasks in `tasks/configure.yml`.
	- Guard kpatch enablement with package presence and OS family to avoid failures on distros without kpatch.

- TLS certificate management for Cockpit
	- Manage certificates in `/etc/cockpit/ws-certs.d/` with variables: `cockpit.tls.enabled`, `cockpit.tls.source` (`openbao|letsencrypt|file`), `cockpit.tls.domains`, `cockpit.tls.files` (key/cert/chain).
	- For `openbao` integrate with the repo’s Vault/OpenBao conventions (derive `vault_secret_name` from host IP, secret engine from `cockpit.secrets.*`) to read certs and install them; reload `cockpit.socket` on change.


- Firewalld handling and idempotency
	- Add `cockpit.manage_firewalld: true` default (referenced in `install.yml`) and skip firewall tasks cleanly when disabled or firewalld missing.

- Branding improvements
	- Move branding into structured defaults: `cockpit.branding.logo`, `cockpit.branding.banner`, `cockpit.branding.name`, and color tokens used by `templates/branding.css.j2`.
	- Ensure SELinux contexts and OS path compatibility (Rocky/RHEL, `/usr/share/cockpit/branding/...`).

- Security hardening
	- Manage `/etc/cockpit/cockpit.conf` with variables for `[WebService]` and `[Session]`:
		- `AllowUnencrypted=false` (default), `LoginTitle`, `IdleTimeout`, allowed `Origins`.
		- Optional access control to restrict login to specific groups (wheel/admin) via PAM guidance.

- Kafka event emission
	- Replace the TODO in `tasks/main.yml` with an optional `community.kafka` produce step when `kafka_bootstrap_servers` is set; emit lifecycle events (install/configure/start/stop/update) with minimal payload.

- Module consistency
	- Standardize on `ansible.builtin.systemd_service` across tasks and handlers (handler currently uses `systemd`).

- Molecule tests (initial coverage)
	- Extend `molecule/default` to assert:
		- Packages installed per flags, `cockpit.socket` enabled/active, port 9090 listening.
		- Branding files deployed when variables set; firewall rule present when managed.
	- Prepare matrix for Rocky 9 (current) and optionally Rocky 10 images when available.

## Mid-term

- SSO and directory integration
	- Optional join to FreeIPA/AD via `realmd/sssd` with variables for domain, admin group mapping, and documentation on Cockpit login behavior.

- Reverse proxy mode
	- Support running behind nginx/traefik: provide a systemd drop-in to bind Cockpit to localhost and disable TLS (`AllowUnencrypted=true`) when explicitly configured; include example proxy configs in docs.

- Observability and logs
	- Emit role facts (installed plugins, socket status, version) and optionally write a small JSON status under `/var/lib/cockpit/ansible-status.json` for scraping.
	- Document Prometheus/node_exporter alignment and journald forwarding options.

- Multi-host/Podman UX
	- Investigate pre-provisioning of additional hosts in Web Console (if a supported config file exists); if user-scoped only, document a helper task to seed per-user preferences.
	- Improve Podman UX: ensure rootless `podman` user has necessary permissions and document login flow to the Cockpit Podman plugin.

- Airgapped readiness
	- Validate that all optional packages exist in the PSP Nexus mirrors; add a preflight that warns when packages are missing.

## Long-term

- Check mode and idempotency polish across all tasks; add `changed_when`/`failed_when` where appropriate.
- Centralize version pins and optional package lists alongside the main repo’s versioning plan (see server-PSP docs/DESIGN.md guidance).
- Ansible-lint/CI pipeline: GitHub Actions to run Molecule on PR, markdown link checks for docs.

## Documentation tasks

- Expand role README with:
	- TLS management examples (OpenBao/file/LE), reverse proxy setup, and security hardening variables.
	- Updated examples for `start`, `stop`, and `configure` now that they’re implemented.
	- Table of optional plugins with defaults and auto-detection rules.

---

Existing items (refined wording):

- Enable automatic software update installation. → Covered under “Automatic updates and kpatch toggles”.
- Enable SSL certificate webconsole. → Covered under “TLS certificate management for Cockpit”.
- Add extra host in webconsole for user podman. → See “Multi-host/Podman UX”.
- Branding parameters in default cockpit variable. → Covered under “Branding improvements”.
- Software update parameters in default cockpit variable. → Covered under “Automatic updates and kpatch toggles”.
- Implement molecule testing. → Covered under “Molecule tests (initial coverage)”.
