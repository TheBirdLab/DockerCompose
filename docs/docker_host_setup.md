# Docker Host Setup

Here is a quick guide for how we setup our docker hosts in our lab.

Enter the following command(s):

```bash
sudo apt update && sudo apt upgrade -y;
sudo apt-get install ca-certificates curl gnupg -y;
sudo install -m 0755 -d /etc/apt/keyrings;
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg;
sudo chmod a+r /etc/apt/keyrings/docker.gpg;
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null;
sudo apt-get update;
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y;
```

These commands do the following:

- Update and upgrade your Linux operating system
- Adds the docker repositories
- Installs docker and all of its dependencies

Bam! Thats it. For Now.