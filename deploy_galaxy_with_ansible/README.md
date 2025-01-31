# Introduction

Files used to deploy Galaxy in local Linux machine.

## Cautions

1. Using `sudo galaxyctl restart galaxy` (which does not work sometimes, use `sudo galaxyctl restart` directly) to restart Galaxy by hand.

2. Using `sudo galaxyctl follow` or `journalctl -fu 'galaxy-*'` to see the logs of Galaxy.

3. Using `sudo galaxyctl follow <service>` or `journalctl -fu <service-unit>` to see the logs of individual services.

4. Using `sudo galaxyctl status` to inspect Galaxy status.

5. Using `sudo galaxyctl status <service>` or `sudo systemctl status <service-unit>` to inspect individual services in detail.

6. **Don't forget to run `sudo galaxyctl update` after Galaxy has been installed if no Galaxy-associated `systemd` services are found when running `sudo galaxyctl status`!**

7. Check out the nginx logs with `journalctl -fu nginx`.

8. Due to that NGINX won't be started successfully if it was started before all Galaxy services are started, a possible solution is to add the following two lines below the `[Service]` section, which ensures that NGINX can always be restarted after a failure:

If all Galaxy services can be started successfully, then NGINX can finally be started successfully after several attempts.

```{bash}
Restart=always
RestartSec=120
```

In brief, you have three options: `galaxyctl`, `systemctl`, or `journalctl`.
