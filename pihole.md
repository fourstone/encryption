## Setting up Pihole with Stubby on raspbian

based on the explanation from heise.de and the stubby homepage. Mostly this is to keep it neatly and updated in a single place and easy to both read and copy-paste into the terminal

# Pre-Boot
- raspbian lite with etcher onto microSD-card
- create ssh file on boot partition after reinserting card into reader
- eject card

# boot
- find IP-adress via DHCP, tell DHCP to always use a certain address
- `passwd`
- `sudo raspi-config`
  - network
    - Hostname
    - Wi-Fi
    - Network Interface Names
- `sudo nano /boot/config.txt` -> comment out audio
- `sudo reboot`
- verify system has no more warnings when logging in

# Install pi-hole
- `curl -sSL https://install.pi-hole.net | bash`
- note down frontend password

# Install Stubby
```
sudo apt-get install libtool autoconf m4 libssl-dev libyaml-dev
git clone https://github.com/getdnsapi/getdns.git
cd getdns
git checkout develop
git submodule update --init
libtoolize -ci
autoreconf -fi
mkdir build
cd build
../configure --prefix=<install_location> --without-libidn --without-libidn2 --enable-stub-only --with-ssl=<openssl_location> --with-stubby
make
sudo make install
sudo /sbin/ldconfig
sudo nano /usr/local/etc/stubby/stubby.yml
```
listen_addresses:
        - 127.0.0.1@5353
        - 0::1@5353

`nano /home/pi/getdns/stubby/systemd/stubby.service`
- /usr/local/bin/stubby
`sudo cp /home/pi/getdns/stubby/systemd/stubby.service /lib/systemd/system/`
`useradd stubby`
`sudo mkdir /var/cache/stubby`
`sudo systemctl enable stubby`
`sudo systemctl start stubby`

# Change Setup in Pihole
-
