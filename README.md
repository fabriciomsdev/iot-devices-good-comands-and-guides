# iot-devices-good-comands-and-guides

This Repository are focused to save & distribute knowledge about IOT devices applied to real life in plain english.

## Raspberry

### Unable And enable WI-FI on Raspberries and Linux based OS

Option 1: Killing wifi
```sh
    sudo rfkill block wifi
```

Option 2: Remove network from wi-fi storage

```sh
    sudo nano /etc/wpa_supplicant/wpa_supplicant.conf
```

Inside this file you will need to remove the variable called as: network

## Time sync using N.T.P.:

Network Time Protocol (NTP) is an internet protocol used to synchronize with computer clock time sources in a network.

#### Do you interesed to learn more?

Watch: <https://www.youtube.com/watch?v=oCtkwEjhyD4>  <br />
For Brazilians: <https://www.youtube.com/watch?v=WDimwYFau1I>

### How to setup this on device?

#### Setup Timezone:

```sh
    sudo timedatectl set-timezone {YOUR TIMEZONE HERE}
```

#### Install NTP

```sh
    apt-get update && apt-get install ntp -y
```


```sh
    cp -p /etc/ntp.conf /etc/ntp.conf.default
```

Clear the new archive:


```sh
    echo "" > /etc/ntp.conf
```

```sh
    nano /etc/ntp.conf
```

Have atention on coments about country NTP servers lists, you can find your zone or set global using: <https://www.pool.ntp.org/pt/zone/>@

Ex. Only For Brazilians:

server a.st1.ntp.br iburst <br />
server b.st1.ntp.br iburst <br />
server c.st1.ntp.br iburst <br />
server d.st1.ntp.br iburst <br />
server gps.ntp.br iburst <br />
server a.ntp.br iburst <br />
server b.ntp.br iburst <br />
server c.ntp.br iburst <br />
server 0.pool.ntp.org iburst <br />
server 1.pool.ntp.org iburst <br />
server 2.pool.ntp.org iburst <br />
server 3.pool.ntp.org iburst <br />

```txt
driftfile /var/lib/ntp/ntp.drift
 

# ENABLE LOGS AND STATICS OF USE
statsdir /var/log/ntpstats/
statistics loopstats peerstats clockstats
filegen loopstats file loopstats type day enable
filegen peerstats file peerstats type day enable
filegen clockstats file clockstats type day enable
 
# PUBLIC NTP SERVERS GLOBAL OR YOU CAN SET ONE OF YOUR REGION USING: https://www.pool.ntp.org/pt/zone/
server 0.pool.ntp.org iburst
server 1.pool.ntp.org iburst
 
# SETUP PERMISSIONS TO RUN
restrict -4 default kod notrap nomodify nopeer noquery limited
restrict -6 default kod notrap nomodify nopeer noquery limited
restrict 127.0.0.1
restrict ::1
```

Restart NTP SERVER:
```sh
    sudo systemctl restart ntp
```

## Network
### How to find all devices on network

```sh
    sudo apt-get install nmap \
    && nmap -sn 192.168.1.0/24
```