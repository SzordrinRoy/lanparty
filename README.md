New Server bringup

1) Fresh install of Ubuntu Server minimal (install openSSH but don't install anything else, including docker as it uses the snap store which is terrible and we will remove later)

2) disable cloud-init "sudo touch /etc/cloud/cloud-init.disabled"

3) remove snap "sudo apt remove snapd"

4) Update Server "sudo apt update" "sudo apt upgrade"

5) Install Nano "sudo apt install nano"

6) edit netplan and add option to each interface "sudo nano /etc/netplan/50-cloud-init.yaml" example below if for a netowrk bond a network bond 
network:
    bonds:
        bond0:
            dhcp4: true
            interfaces:
            - enp1s0
            - enp2s0
            - enx9cebe8b28dcc
            parameters:
                mode: balance-alb
    ethernets:
        enp1s0:
            optional: true
        enp2s0:
            optional: true
        enx9cebe8b28dcc:
            optional: true
    version: 2

7) Install docker "curl -sSL https://get.docker.com | sh" "sudo usermod -aG docker $USER"

8) Reboot "sudo reboot"

9) Install portainer "sudo docker pull portainer/portainer-ce:latest" "sudo docker run -d -p 9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v /data/bay0/Config/portainer_data:/data portainer/portainer-ce:latest"

10) Configure Portianer-  in web broswer enter "serverIpAddress:9000" (password must be 12 charaters)

11) Click get started

12) Click local, Click Stacks, click + Add Stack

13) Name stack, click Repository, add "https://github.com/SzordrinRoy/lanparty" to Reposiroty URL



