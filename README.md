# What is Ibis?

Ibis is research infrastructure for running measurement applications on edge devices.

# What is Ibis-in-a-box?

Ibis-in-a-box is packaging of the core services that compose the Ibis Infrastructure. This includes

1. The Ibis Dashboard + API
1. An authentication service, Keycloak
1. Underlying device management service, [openBalena](https://open-balena-docs.balena.io/)
1. Underlying application management service, [k3s](https://k3s.io/)

This project is currently a work in progress, and supports only a development deployment of parts #1 and #2.

# Usage

In order to set up your own Ibis site, follow the below steps. We assume these steps take place on a fresh Ubuntu 22 VM.

1. Clone this repository
1. Edit `values.yaml` as needed fit
1. Run `./ibis install` - To install ansible dependencies, and docker runtime on host.
1. Run `./ibis keycloak` - To install the authentication service.
1. Run `./ibis dashboard` - To install the dashboard service.

Once complete, you can expose services via `sshuttle`. For example
```
sshuttle --auto-hosts --remote cc@$IP $(ssh cc@$IP ip -f inet addr show ens3 | awk '/inet / {print $2}')
```

Then in your browser, you can connect to services:

1. Keycloak - http://ibis.local

1. Dashboard - http://ibis.local:8080/
    - After initial log in, run `./ibis admin` to make a user an admin in the dashboard.