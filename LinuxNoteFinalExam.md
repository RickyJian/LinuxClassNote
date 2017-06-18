# final exam

## 公鑰登入


```vi

vi /etc/ssh/
vi ssh_config 

passwordauthentication no #不能用帳密登入

```
## DNS
### Server 端

```vi



yum  install bind-chroot
yum  install bind-utils

cd /etc/

# 修改 conf

vi named.conf

cd /var/named

cp named.empty db-site1.class.ntub

# 修改 empty

vi db-site1.class.ntub



systemctl enable named-chroot
systemctl start named-chroot



rndc reload

# 檢查 DNS 成功與否

host ns.site01.exam.class.ntub 127.0.0.1



```

### Client 端

```vi

 

host -t ns site01.exam.class.ntub



```

```

# 修改 /var/named/named.empty


```


```

# 修改 /etc/named.conf


```



## samba

### server

```vi

yum install -y  samba
systemctl eable smb


mkdir /share

group staff
useradd -g staff emp01
useradd -g staff emp02

smbpasswd -a emp01
smbpasswd -a emp02

# tail /etc/passwd 

cd /etc/samba

vi smb.conf.example

vi smb.conf

systemctl restart smb

ss -ntulp |grep 445

# share 權限設定
chmod u=rwx, g = rwx , o =--- /share/

chgrp staff /share/

```

```

# smb.conf.example



```

```
# smb.conf
```

### client

```vi

yum install cifs-utils

mount -t cifs -o rw,username=emp01,password=password //128.119.223.152/share /mnt

# 128.199.223.152 smbserverip

cd /mnt
touch a


```

## mail server

### server

```vi

cd /var/named
vi dns
rndc reload

cd /etc/postfix

cp main.cf main.cf_0612

vi main.cf

systemctl restart postfix

# 收信目錄

cd /var/spool/mail 


## 以下可不做
cd /etc/devecont/conf.d 

vi 10-auth.conf

cd /etc/devecot/
vi devecot.conf

```

```

# main.cf


```

### client

```

host -t mx mailroot
yum provides *bin/mail

yum install mailx -y


exho test mail | mail -s emp01@site01.exam.cass.ntub

sendmail -q
```

## DB backup

```vi

yum install mariadb-server
systemctl enable mariadb
systemctl start mariadb

mysql -u root -h localhost

less /var/log/message
## 從message中找出這行
'/usr/bin/mysqladmin' -u root password 'new-password'



yum install mod_ssl php php-mysql php-pdo php-mbstring

cd /var/www/html

curl -O -L  https://files.phpmyadmin.net/phpMyAdmin/4.0.10.20/phpMyAdmin-4.0.10.20-all-languages.tar.gz

tar -zxvf  phpMyAdmin-4.0.10.20-all-languages.tar.gz


mv  phpMyAdmin-4.0.10.20-all-languages mysql

systemctl start httpd

## 網站上 crate database and table



mysqldump --opt -u root -p -h localhost tablename > tablename.sql

mysql -u root -p -h localhost tablename < tablename.sql

```

