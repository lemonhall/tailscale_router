

### fedora下安装 tailscale

https://tailscale.com/download/linux/fedora

sudo dnf config-manager --add-repo https://pkgs.tailscale.com/stable/fedora/tailscale.repo
sudo dnf install tailscale

sudo systemctl enable --now tailscaled

### 开子网路由

https://tailscale.com/kb/1019/subnets/?tab=linux

echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf
sudo sysctl -p /etc/sysctl.conf

开子网

sudo tailscale up --advertise-routes=192.168.50.0/24,172.16.200.0/24

转到页面
https://login.tailscale.com/admin/machines

看到有子网的机器，点击最右，有subnet配置

Linux稍微特殊一点：
sudo tailscale up --accept-routes

需要走一个这个命令