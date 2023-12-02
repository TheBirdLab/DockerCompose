![TheBirdLab](../../docs/imgs/thebirdlab_banner.png)

Welcome. Gitea is an amazing self-hosted service so here are some of our configurations which include:

- HTTPS Gitea web support
- TLS communication with the database
- Postgres database

# Setup

Clone the repository to the machine of your choice (we recommend one that has docker already installed and configured):

```bash
git clone https://github.com/TheBirdLab/DockerCompose.git
cd DockerCompose/stacks/gitea
```

## Create the Postgres Password Secret File

Create the `postgres_passwd` secret file and enter a password:

```bash
echo [ENTER YOUR PASSWORD HERE] >> postgres_password.passwd
```

## Option A: Self-Signed Gitea Certificates

Run the following command from the `DockerCompose/stacks/gitea` directory on your docker host to bring the stack online:

```bash
docker compose up -d
```

Enter into the `gitea-server-1` container's shell:

```bash
docker exec -it gitea-server-1 /bin/bash
```

Run the gitea command to generate self-signed certificates

```bash
gitea certs --host [HOSTNAME]
```

This will put the certificates in the root directory of wherever you ran the previous command.

Copy out the `cert.pem` and `key.pem` file contents:

```bash
cat ./cert.pem
cat ./key.pem
```

Paste the contents of each into the `DockerCompose/stacks/gitea/certificates` directory with the following names:

- `cert.pem` -> `gitea_web_cert.pem`
- `key.pem` -> `gitea_web_key.pem`

Stop the stack by running the following command:

```bash
docker compose down
```

Run the stack by running the following command:

```bash
docker compose up -d
```

Navigate to `https://HOSTNAME:GITEA_HTTPS_PORT` to configure Gitea for the first time. There is no default login as you will setup an admin during the initial install.

# Running

Run the following command from the `DockerCompose/stacks/gitea` directory on your docker host to bring the stack online:

```bash
docker compose up -d
```

To stop the stack run the following command:

```bash
docker compose down
```

To remove all data from previous runs run the following command:

```bash
rm -rf server_data/ db_data/
```