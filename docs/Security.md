# Security

The web server serves the Web UI and the Web API. Anyone who reaches it can run commands and edit your config files. Treat it like an admin panel.

## Defaults

- Default: disabled. Before 5.0.0 it was enabled on non-Docker installs, including headless and seedbox installs.
- It binds to `127.0.0.1` on port `8181` (`0.0.0.0` in Docker, where the port mapping decides exposure).
- Any non-loopback bind needs authentication: Basic, API key (`api_only`), or External auth. Without it, the web server does not start and the log says why.
- Set `QBT_WEB_USERNAME` and `QBT_WEB_PASSWORD` to create the Basic login on first start. Only a hash is stored.
- External auth is accepted only from addresses in `trusted_proxies` (empty by default).
- `/api/health`, `/api/version`, and `/api/get_base_url` never need a login.

## Hardening

1. Leave the web server off if you do not need it. Command-line runs and schedules work without it. Turn it on with `--web-server` or `QBT_WEB_SERVER=true`.
2. Keep it bound to localhost when you can: `--host 127.0.0.1` or `QBT_HOST=127.0.0.1`. In Docker, publish the port on the host loopback, for example `"127.0.0.1:8181:8181"`.
3. Set up authentication (required on any non-loopback bind). Use basic auth for the Web UI, or `api_only` mode and an API key for scripts. Use a long, unique password.
4. To reach it from other machines, use a reverse proxy that adds HTTPS and its own login, or a VPN. See [Docker Installation](Docker-Installation#reverse-proxy) for an example.
5. Never expose it to the internet. Do not forward the port on your router.
6. Keep qbit_manage up to date.

## If it was exposed

1. Stop the web server.
2. Change the qBittorrent password and API key.
3. Rotate every secret in your config: the `qbt` credentials, Notifiarr and Apprise keys, and webhook URLs.
4. Generate a new qbit_manage API key and password.
5. Check your qBittorrent logs and qbit_manage logs for activity you do not recognize.

## Authentication notes

- Settings live in `qbm_settings.yml` in your config folder.
- After 10 failed attempts in one minute, an address is blocked until that minute passes.
- Leave `bypass_auth_for_local` off unless you trust every device on your network.
- If you lock yourself out, stop qbit_manage, set `authentication.enabled: false` in `qbm_settings.yml`, and start it again. Keep the web server bound to localhost while you do this.

See [SECURITY.md](https://github.com/StuffAnThings/qbit_manage/blob/develop/SECURITY.md) for the threat model, the full list of secure defaults, and how to report a vulnerability privately.
