<h1>Troubleshooting</h1>

### Cannot connect to Herd-View

1. Ensure all VPNs have been disconnected
2. Synchronize `client` device local time with `Herd-Server` time
3. Try to add the `client` again via `Herd-CLI` one-liner

### Cannot access Herd-View

1. Check if the `user` credentials are correct
2. Create a `user` via `Herd-CLI`
3. Download the CA certificate from `https://10.10.0.3:3000/ca.crt` and install it

### Error during asset joining

1. Remove the `asset` via `Herd-CLI` one-liner
2. Synchronize `asset` device local time with `Herd-Server` time
3. Try to add the `asset` again via `Herd-CLI` one-liner

### Commands not executed by online assets

1. Logout from the `Herd-View`
2. Login again into the `Herd-View` to get a fresh token
