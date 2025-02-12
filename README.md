New Server bringup

1) Fresh install of Ubuntu Server (install openSSH but don't install anything else, including docker as it uses the snap store which is terrible and we will remove later)

2) disable cloud-init "sudo touch /etc/cloud/cloud-init.disabled"

3) remove snap "sudo apt remove snapd"

4) Update Server "sudo apt update" "sudo apt upgrade"

5) edit netplan and add option to each interface "sudo nano /etc/netplan/50-cloud-init.yaml" example below for a network bond 
network:
  bonds:
    bond0:
      dhcp4: true
      interfaces:
        - enp1s0
        - enp2s0
        - usbports
      parameters:
        mode: balance-alb
  ethernets:
    enp1s0:
      optional: true
    enp2s0:
      optional: true
    usbports:
      match:
        name: enx*
      optional: true
  version: 2

7) Install docker "curl -sSL https://get.docker.com | sh" then "sudo usermod -aG docker $USER"

8) Reboot "sudo reboot"

10) Install portainer "sudo docker pull portainer/portainer-ce:latest" then "sudo docker run -d -p 9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /opt/appdata/portainer:/data portainer/portainer-ce:latest"

11) Configure Portianer-  in web broswer enter "serverIpAddress:9000" (password must be 12 charaters)

12) Click get started

13) Click local, Click Stacks, click + Add Stack

14) Name stack, click Repository, add "https://github.com/SzordrinRoy/lanparty" to Reposiroty URL

15) Under Environment variables click advanced mode. Go to "https://github.com/SzordrinRoy/lanparty/blob/main/.env" in your webbrowser and copy the contents into the box and change host IP to the lanparty server IP

16) Click deploy the stack



