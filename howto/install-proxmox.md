# Install on Proxmox

Kobozo Bot runs on your Proxmox host. The public installer starts an unprivileged
orchestrator LXC and opens a web setup wizard. Product source is not included.

## What you need

- Proxmox VE 9 on x86-64
- Root access on that host
- Disk storage, Linux-template storage and a network bridge
- DHCP or a reserved address for the orchestrator

## Download and install

1. Open the [latest release](https://github.com/kobozo/kobozo-bot-releases/releases/latest).
   `releases/latest/download/install.sh` is always the newest stable release.
2. Download `install.sh` (and `SHA256SUMS` if you want to compare it).
3. Run `bash install.sh --proxmox` as root on the Proxmox host. Without
   `--proxmox` the installer puts the desktop app on a normal computer instead
   (and refuses to run on a Proxmox host). It pins this release’s runtime
   archive URL and digest. It does not overwrite an existing installation on retry.

Before it installs anything the installer checks that the release is signed by
Kobozo: it downloads the release's `manifest.json` and `manifest.json.sig`,
verifies the signature with `openssl` against the keys built into the script,
and checks the runtime archive against the signed manifest. If any check fails
it says so and installs nothing; an existing installation is left as it was.
Do not work around a failed check; download a fresh `install.sh` instead.

### Try a beta

Betas are test releases published before a stable one. Run the installer with
`--beta` to install the newest beta, or `--version 2026.11.18-beta.1` to choose
one. They go through the same signature check. The choice is remembered as the
installation's update channel, so the server follows betas afterwards; an
administrator can change it under **My workspace → Server and version**.

The installer does not need a GitHub account or an email address. After the LXC
starts, open the printed HTTPS address. Trust the local Proxmox CA or put a
trusted proxy in front. Do not skip TLS verification.

## Web setup

1. Choose the first administrator email and password. That retires the
   installation token.
2. In **Proxmox**, confirm the host. In **Computers**, choose storage, bridge,
   VLAN if any, sizes and unused IDs, then install the project template.
3. In **Backups**, choose a Proxmox backup server, network share or disk. A backup server can be limited so Kobozo adds backups and cannot delete them; the server then prunes on its own schedule (7 daily, 4 weekly). Kobozo's own job keeps all copies; your backup server's prune job removes old ones. Other backup jobs on this storage are not changed. The page keeps saying that add-only setup is not verified until an administrator confirms the backup user, the datastore ACL and the prune job. A network share or USB disk cannot block deletion that way. The nightly job and Back up now both use that job's retention (7 daily, 4 weekly) and do not use the storage entry's retention. You can skip once. Skipping leaves a permanent warning until an administrator sets a destination under **My workspace → Backups**. A screenshot of this step is still pending a lab capture (`docs/backup-lab.md`).
4. In **Models**, pick local-only operation or named cloud endpoints. Enter the
   URL and key. **Detect models** lists what that server serves; you can also
   add a model ID by hand. **Test from this server** talks only to the model
   chosen for your first bot.
   When setup finishes, these connections move to **Administration → Model
   keys → Company keys**, where you manage them from then on. Models the server
   no longer serves are dropped; your first bot keeps its model.
5. In **Verify**, create the first bot and complete the desktop check. **Open my
   team** stays disabled until that check succeeds.

Keep the saved install script. A new download is a new installation identity.
Public hostname, certificate renewal, SMTP and passkey/OAuth origins
are not finished by the wizard. Nightly backups use the destination from step 3.

## After install

Administrators update the orchestrator from **My workspace → Server and version**.
There they choose the **Stable** or **Beta** channel and can switch on
**Update automatically** (off by default; the server then checks hourly).
Releases are signed and the server refuses anything that does not verify. See
[My workspace](my-workspace.md). Automatic agent upgrades are not implemented.
