# Setup

```bash
# requirements: do inside Qubes template not AppVM
sudo pacman -Sy docker docker-compose

cd docker

# download and prepare hhg multistore CE
wget "http://web.archive.org/web/20220206191311if_/https://www.hhg-multistore.com/index.php?module=downloads&download=7734842fd32c9c30e484ca32ab75abc5" -O hhg.zip

unzip hhg.zip -d src

# docker stuff
sudo systemctl start docker
sudo docker-compose build
sudo docker-compose up
# chown www-data:www-data within container maybe required
```