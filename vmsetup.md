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

###tools install
```
sudo apt-get install git vim
```

###analysis tools install
```
gpg --keyserver  hkp://keys.gnupg.net --recv-keys 1C4CBDCDCD2EFD2A
gpg -a --export CD2EFD2A | sudo apt-key add -
echo "deb http://repo.percona.com/apt `lsb_release -cs` main" >> sudo /etc/apt/sources.list.d/percona.list
echo "deb-src http://repo.percona.com/apt `lsb_release -cs` main" >> sudo /etc/apt/sources.list.d/percona.list
sudo apt-get install percona-toolkit
echo "deb http://deb.goaccess.io $(lsb_release -cs) main" | sudo tee -a /etc/apt/sources.list
wget -O - http://deb.goaccess.io/gnugpg.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install goaccess
```

###DB
```
pt-query-digest slow.log
or
tcpdump -s 65535 -x -nn -q -tttt -i any -c 1000 port 3306 > mysql.tcp.txt
pt-query-digest --type tcpdump mysql.tcp.txt
```


###ngnix
```
ricetuan@instance-2:~$ cat /etc/goaccess/ltsv.nginx
color_scheme 2
date_format %d/%b/%Y
time_format %H:%M:%S
log_format host:%h\tuser:%^\ttime:%d:%t %^\treq:%r\tstatus:%s\tsize:%b\treferer:%R\tua:%u\tforwardedfor:%^\treqtime:%T\tapptime:%^

log_format ltsv "host:$remote_addr"
"\tuser:$remote_user"
"\ttime:$time_local"
"\treq:$request"
"\tstatus:$status"
"\tsize:$body_bytes_sent"
"\treferer:$http_referer"
"\tua:$http_user_agent"
"\tforwardedfor:$http_x_forwarded_for"
"\treqtime:$request_time"
"\tapptime:$upstream_response_time";
access_log /var/log/nginx/ap.access.log ltsv;
error_log /var/log/nginx/error.log;

goaccess -f /var/log/nginx/ap.access.log -p /etc/goaccess/ltsv.nginx
```
