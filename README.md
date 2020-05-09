# Docker Swarm - Containers Health Monitor Production Deployment
[![License][license-image]][license-url] [![Commit][last-commit-image]][last-commit-url] [![Releases][releases-image]][releases-url] [![Contributors][contributors-image]][contributors-url] 

Repository with configuration files required for **Containers Health Monitor Production Deployment** using Docker Swarm.

## Main Features:
- **Simplified and automated startup through scripts.**

----

## Prerequisites
1. Linux _(Ubuntu 16.04+ recommended)_
2. Docker Engine 18.06.0+
   - Follow all the steps present in the [official documentation](https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce).
3. Docker Compose 1.22.0+
   - Follow all the steps present in the [official documentation](https://docs.docker.com/compose/install/).
4. Make sure that Swarm is enabled by typing `docker system info`, and looking for a message `Swarm: active` _(you might have to scroll up a little)_.
   - If Swarm isn’t running, simply type `docker swarm init` at a shell prompt to set it up.

## 1. Health monitor services stack 

### 1.1 Set the environment variables
To ensure flexibility, the health monitor services receive some parameters through environment variables, e.g. SMTP configurations, credentials (username and password), etc.

First, create the configuration file based on the `.env.monitor.example` file:

```sh
$ cp .env.monitor.example .env.monitor
```

After making the settings, execute the command to assign the values defined in the environment variables that are in the settings file:

```sh
$ set -a && source .env.monitor && set +a
```

#### 1.1.1 Authorization/Authentication Setup

Variables to define the administrator user's credentials the first time the Grafana is instantiated.

| Variable | Description | Example |
| -------- | ----------- | ------- |
| `ADMIN_USERNAME` | Username of the default admin user created automatically at the first time the Grafana is instantiated. | `admin` |
| `ADMIN_PASSWORD` | Password of the default admin user created automatically at the first time the Grafana is instantiated. | `admin` |

#### 1.1.2 External Services Ports

| Variable | Description | Example |
| -------- | ----------- | ------- |
| `GF_PORT` | Port used by the Grafana service to listen for HTTP request. | `3000` |

#### 1.1.3 SMTP Setup

| Variable | Description | Example |
| -------- | ----------- | ------- |
| `GF_SMTP_ENABLED` | Enable SMTP server settings. | `false` |
| `GF_SMTP_HOST` | Host where the SMTP server is allocated. | `smtp.gmail.com:465` |
| `GF_SMTP_USER` | Registered email on the SMTP server. It will be used to send emals when an alarm is detected. | `grafana@test.com` |
| `GF_SMTP_PASSWORD` | Password for the email registered on the SMTP server. | `secret` |

#### 1.1.4 Storage Data

| Variable | Description | Example |
| -------- | ----------- | ------- |
| `DATA_RETENTION` | Time the data remained stored in database. | `15d` - corresponds to 15 days |

### 1.2 Building and Deploying the containers

#### Start services stack

```sh
$ docker stack deploy -c docker-monitor-stack.yml <stack_name>
```


#### Stop services stack


```sh
$ docker stack rm <stack_name>
```

-----

[//]: # (These are reference links used in the body of this note.)
[license-image]: https://img.shields.io/badge/license-Apache%202-blue.svg
[license-url]: https://github.com/ocariot/docker-swarm/blob/master/LICENSE
[last-commit-image]: https://img.shields.io/github/last-commit/ocariot/docker-swarm.svg
[last-commit-url]: https://github.com/ocariot/docker-swarm/commits
[releases-image]: https://img.shields.io/github/release-date/ocariot/docker-swarm.svg
[releases-url]: https://github.com/ocariot/docker-swarm/releases
[contributors-image]: https://img.shields.io/github/contributors/ocariot/docker-swarm.svg
[contributors-url]: https://github.com/ocariot/docker-swarm/graphs/contributors
