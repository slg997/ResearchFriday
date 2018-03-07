# Moloch 0.20 AND Ubuntu Server 16.0.4
Add Oracle Java Repository
```
sudo add-apt-repository ppa:webupd8team/java
```
Update Repository  
```
sudo apt-get update
```
Install Zip
```
sudo apt-get install zip
```
Install NPM 
```
sudo apt-get install npm
```
Install Java 8 
```
sudo apt-get install oracle-java8-installer
```
Upgrade 
```
sudo apt-get upgrade && sudo apt-get dist-upgrade
```
Disable Swap 
```
sudo swapoff -a
```
Edit fstab and comment out swap (disable swap) 
```
sudo nano /etc/fstab
``` 
Edit your interfaces for configuration (optional) 
```
sudo nano /etc/network/interfaces
```
Configure your NIC's as required (optional) 
```
auto lo
iface lo inet loopback
auto {eth0}
iface {eht0} inet static
address 10.#.#.#
gateway 10.#.#.#
netmask 255.255.255.0
dns-nameservers 8.8.8.8 8.8.4.4

auto {ethX}
iface {ethX} inet manual
ethtool -G ens192 rx 4096 tx 4096
ethtool -K ens192 rx off tx off gs off tso off gso off
```
Reboot 
```
sudo reboot
```
Download (check for latest moloch.deb build) 
```
wget https://files.molo.ch/builds/ubuntu-16.04/moloch_0.20.2-2_amd64.deb
```
Install (moloch.deb) 
```
sudo dpkg -i moloch_0.20.2-2_amd64.deb
```
Install Dependencies [If the previous step halts due to errors]
```
sudo apt-get install -f
```
Configure Moloch 
```
sudo /data/moloch/bin/Configure

#specify your monitoring interface: ethX
#Elasticsearch URL: Default
#Install Elasticsearch locally for demo: no
#Password for S2S: {anything}
```
Download (elasticsearch.deb) 
```
wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/deb/elasticsearch/2.4.6/elasticsearch-2.4.6.deb
```
Install (elasticsearch.deb)  
```
sudo dpkg -i elasticsearch-2.4.6.deb
```
Startup (start elasticsearch on startup|update elasticsearch.yml as needed) [Optional] 
```
sudo systemctl enable elasticsearch.service
```
Start Elasticsearch (or reboot) 
```
sudo systemctl start elasticsearch.service
```
Initialize Moloch Database 
```
/data/moloch/db/db.pl http://localhost:9200 init
```
Add Admin User to Moloch Viewer 
```
/data/moloch/bin/moloch_add_user.sh admin admin PASSWORDGOESHERE --admin
```
Start molochcapture.service 
```
systemctl start molochcapture.service
```
Start molochviewer.service 
```
systemctl start molochviewer.service
```

Point your browser to http://x.x.x.x:8005 (IP address of Moloch) 
