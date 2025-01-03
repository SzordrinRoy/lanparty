New Server bringup

1) Fresh install of Ubuntu Server minimal (install openSSH but don't install anything else, including docker as it uses the snap store which is terrible and we will remove later)

2) disable cloud-init "sudo touch /etc/cloud/cloud-init.disabled"

3) remove snap "sudo apt remove snapd"

4) Update Server "sudo apt update" "sudo apt upgrade"

5) Install Nano "sudo apt install nano"

6) edit netplan "sudo nano /etc/netplan/50-cloud-init.yaml"

7) Install docker "curl -sSL https://get.docker.com | sh" "sudo usermod -aG docker $USER"

8) Reboot "sudo reboot"

9) Install portainer "sudo docker pull portainer/portainer-ce:latest" "sudo docker run -d -p 9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /data/bay0/Config/portainer_data:/data portainer/portainer-ce:latest"

10) Install stack



