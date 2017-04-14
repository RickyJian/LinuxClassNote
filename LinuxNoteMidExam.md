# 期中考筆記
## 考題

* DNS網路設定 ([LinuxNote0410](https://github.com/RickyJian/LinuxClassNote/blob/master/LinuxNote0410.md))
* 使用者建立及群組修改  ([LinuxNote0313](https://github.com/RickyJian/LinuxClassNote/blob/master/LinuxNote0313.md) ，
[LinuxNote0327](https://github.com/RickyJian/LinuxClassNote/blob/master/LinuxNote0327.md))
* Apache、HTTPs 建立及設定 ([LinuxNote0410](https://github.com/RickyJian/LinuxClassNote/blob/master/LinuxNote0410.md))
* 切硬碟掛載  ([LinuxNote0320](https://github.com/RickyJian/LinuxClassNote/blob/master/LinuxNote0320.md) ，
[LinuxNote0327](https://github.com/RickyJian/LinuxClassNote/blob/master/LinuxNote0327.md))

---
## 注意事項
1. __<font color ="red">不能用SSH</font>__ 。為了怕使用到，建議先關掉它吧!!<br>
    > systemctl stop sshd

2. 考題部分可以跳著做，只要記得先灌server在做網路設定，其餘部分看個人習慣。

----
## 實作步驟
### Step 1  網路連線
1. init-class `No` // 號碼
    > ip = no * 5  +1 ～ +5 
    >
    >> no = 31<br>
    >> ip = 31*5 +1 ～ +5 = 156 ～ 160

2. reboot

### Step 2  Server 創建
1. wget http://140.131.114.2/class/vm-init.sh
    > 下載server 安裝檔

2. sh vm_init.sh r6 
3. create_vm.sh `serverName`
    > serverName 替換

4. yum provides */remote-viewer
5. yum install -y virt-viewer
6. viewvm `serverName`
    > serverName 替換
    > 開啟VM

### Step 3 Server1 環境建置
1. nmcli con show 
    > 網路連線資訊

2. nmcli con del `networkName`
    > 刪除連線 留eth0 其餘刪除

3. nmcli con add type ethernet ifname eth0 con-name eth0 ipv4.address “10.1.1.157/24” ipv4.gateway 10.1.1.254 __ipv4.dns `DNS`__ ipv4.method manual
    > <font color ="red"> DNS網路設定 </font><br>
    > DNS ： 改成考試用DNS，例如：8.8.8.8

4. nmcli con up eth0 
5. yum install bind-utils
6. yum provides * /host
7. yum install httpd
    > <font color ="red"> HTTPs 安裝 </font>

8. yum install mod_ssl
    > <font color ="red"> Apache Server 安裝 </font>

8. systemctl start httpd
9. systemctl enable httpd
10. firewall-cmd --permanent --add-service=http
11. firewall-cmd --permanent --add-service=https
12. firewall-cmd --reload
13. fdisk -l /dev/vdb <br>
    n → p → l → `按ENTER` → +400M → w
    > +400M ： 硬碟容量，請參照考試指定分割大小

14. mkfs.`ext4` /dev/vdb1
    > ext4 ： 格式化硬碟格式，請參照考試指定格式

15. mount /dev/vdb1 /var/www/html
16. df -h
17. mount -a
18. vi /etc/fstab
    ```
    /dev/vdb1 /var/www/html ext4 defaults 0 0
    ```
    > ext4 ： 格式化硬碟格式，請參照考試指定格式

19. restorecon -R -v /var/www/html 
20. touch /var/www/html index.html

### Step 4 使用者新增及群組設定
1. vi create_users.sh
    ```
    for u in {1..50}
        do 
            useradd autouser${u}
            echo user${u} | passwd --stdin autouser${u}
        done
    ```

    >  useradd autouser${u} ： 新增使用者 autouser1 ... <br>
    > echo user${u} ： 密碼 <br>
    > passwd --stdin autouser${u} ： 更改的帳戶，例如：找出 autouser1 並將密碼更改為 user1 <br>
    > {1..50}：請參照考試新增數量

2. . create_users.sh
3. cd /home
4. ls -li
5. tail -n 5 /etc/passwd > /tmp/test.txt
6. cd /tmp 
7. vi /tmp/test.txt
    ```
    autouser1:centos 
    .
    .
    .
    .
    autouser5...
    ```
8. chpasswd < /tmp/test.txt
    > chpasswd ： 大量修改密碼

