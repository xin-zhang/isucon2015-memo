###instance setup
```
curl https://sdk.cloud.google.com | bash
gcloud auth login
gcloud compute zones list
gcloud compute regions list
gcloud config set compute/zone 指定されたzone
gcloud config set compute/region 指定されたregion
gcloud compute ssh isucon5
```

###vm setup
```
#/bin/bash
wget http://repo.mysql.com/mysql-apt-config_0.2.1-1debian7_all.deb
sudo dpkg -i mysql-apt-config_0.2.1-1debian7_all.deb
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449
echo deb http://dl.hhvm.com/debian wheezy main | sudo tee /etc/apt/sources.list.d/hhvm.list
sudo apt-get update
sudo apt-get dist-upgrade -y
sudo apt-get install mysql-server-5.6 -y
sudo apt-get install nginx -y
sudo apt-get install hhvm -y
sudo /usr/share/hhvm/install_fastcgi.sh
sudo /etc/init.d/nginx start
sudo service hhvm restart
```

