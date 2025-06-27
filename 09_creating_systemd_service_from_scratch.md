# Creating a systemd service from scratch

---

## 1 ⟩ Decide on the runtime command

* **Absolute path** is safest (`/usr/bin/java`, `/usr/bin/python3`, `/opt/myapp/bin/server`).
* Verify it runs correctly under the intended user before touching systemd.
* Create a service file in /etc/systemd/system/
* File Name atlasmap.service

Example:
---
```bash

[Unit]
Description=AtlasMap Standalone Application
After=network.target

[Service]
User=pangadik
WorkingDirectory=/home/pangadik/atlas-map
ExecStart=java -cp "atlasmap-standalone.jar:libs/*" io.atlasmap.standalone.ApplicationMain
Restart=always
StandardOutput=append:/home/pangadik/atlas-map/atlasmap.log
StandardError=append:/home/pangadik/atlas-map/atlasmap-error.log

[Install]
WantedBy=multi-user.target
```

## 2 ⟩ `[Unit]` section – How systemd treats the service

| Directive                                     | Meaning                                                 | Why it matters                                                        |
| --------------------------------------------- | ------------------------------------------------------- | --------------------------------------------------------------------- |
| `Description=AtlasMap Standalone Application` | Free-form text shown by `systemctl status` and in logs. | Purely informational.                                                 |
| `After=network.target`                        | Starts this service only after basic networking is up.  | AtlasMap often exposes an HTTP endpoint, so networking must be ready. |




## 3 ⟩ `[Service]` section – How the process runs

| Directive                                                                                    | Meaning                                                         | Common pitfalls / comments                                                      |
| -------------------------------------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| `User=pangadik`                                                                              | Runs the JVM as unprivileged user `pangadik`.                   | Makes the service safer. Files it writes must be writable by `pangadik`.        |
| `WorkingDirectory=/home/pangadik/atlas-map`                                                  | Sets working directory before launching JVM.                    | Relative paths (configs, mapping files) resolve here. Directory must exist.     |
| `EnvironmentFile=-/etc/myapp/myapp.env`                                                      | Loads environment variables from optional key=value file.       | The leading `-` means it's optional. Useful for separating secrets/configs.     |
| `Environment=JAVA_OPTS=-Xms256m -Xmx512m`                                                    | Sets inline environment variables.                              | Example of passing JVM options. Can be expanded for other tunables.             |
| `ExecStart=java -cp "atlasmap-standalone.jar:libs/*" io.atlasmap.standalone.ApplicationMain` | Command systemd executes to launch AtlasMap.                    | If `JAVA_HOME` isn't set, specify full path to `java` or use `Environment=`.    |
| `Restart=always`                                                                             | Restarts process indefinitely if it exits (crash or otherwise). | Useful for "keep-alive" services.                                               |
| `StandardOutput=append:/home/pangadik/atlas-map/atlasmap.log`                                | Appends stdout to log file.                                     | Requires systemd ≥ 240. Log files and directory must be writable by `pangadik`. |
| `StandardError=append:/home/pangadik/atlas-map/atlasmap-error.log`                           | Appends stderr to separate log file.                            | Same permissions requirement as above. Logs also viewable with `journalctl`.    |


## 4 ⟩ `[Install]` section – How it's enabled at boot

| Directive                    | Meaning                                                               |
| ---------------------------- | --------------------------------------------------------------------- |
| `WantedBy=multi-user.target` | Creates symlink under `multi-user.target`, enabling autostart at boot |


## 5 ⟩ Typical systemd Management Commands

```bash
# Reload systemd to recognize new/updated unit files
sudo systemctl daemon-reload

# Start service immediately
sudo systemctl start atlasmap

# Enable service to start at boot
sudo systemctl enable atlasmap

# Check status and recent logs
sudo systemctl status atlasmap -n 10

# View live logs
journalctl -u atlasmap -f  # Ctrl+C to stop following
```


## 6 ⟩ Monitor & troubleshoot

```bash
systemctl status myapp           # Health summary
journalctl -u myapp -f           # Live logs (Ctrl+C to quit)
systemctl restart myapp          # Restart with updated config
systemctl stop myapp             # Graceful shutdown
```

### Common Issues

| Symptom                            | Likely Cause                                     | Fix                                                     |
| ---------------------------------- | ------------------------------------------------ | ------------------------------------------------------- |
| `permission denied` opening logs   | Log file owned by root but service runs as myapp | `sudo chown -R myapp:myapp /var/lib/myapp`              |
| Unit exits immediately after start | Wrong `ExecStart` command or app exits `0`       | Double-check paths; use `Restart=always` only if needed |
| No logs in `journalctl`            | Logs redirected to unwritable files              | Check `StandardOutput=` paths & permissions             |

---

## 7 ⟩ Typical systemd Management Commands

```bash
# Reload systemd to recognize new/updated unit files
sudo systemctl daemon-reload

# Start service immediately
sudo systemctl start atlasmap

# Enable service to start at boot
sudo systemctl enable atlasmap

# Check status and recent logs
sudo systemctl status atlasmap -n 10

# View live logs
journalctl -u atlasmap -f  # Ctrl+C to stop following
```

---

## 8 ⟩ Fixing the "log is unwritable" Error

### Ownership Fix

The service runs as `pangadik`, so both the log directory and files must be owned by that user:

```bash
sudo chown -R pangadik:pangadik /home/pangadik/atlas-map
```

### Permissions Fix

Standard safe permissions:

```bash
sudo find /home/pangadik/atlas-map -type d -exec chmod 755 {} \;
sudo find /home/pangadik/atlas-map -type f -name 'atlasmap*.log' -exec chmod 644 {} \;
```

⚠️ Avoid using `777` unless absolutely necessary.

### SELinux/AppArmor

Some distributions may enforce additional security policies. In most cases, correcting ownership and permissions resolves the issue.

---

## 9 ⟩ Verify the Fix

After correcting ownership and permissions:

```bash
sudo systemctl restart atlasmap
sudo systemctl status atlasmap
```

Ensure the service is running and no "permission denied" errors appear.

---


