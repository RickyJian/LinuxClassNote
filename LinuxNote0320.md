#  Note 0320
## 實作步驟

1. wget http://140.131.114.2/class/vm-init.sh
    > 下載 `http://140.131.114.2/class/vm-init.sh` 資料

2. sh vm-init.sh r6 
3. create_vm.sh `server1`
    > server1 ： server name

4. viewvm `server1`
    > viewvm ： 開啟虛擬機 <br>
    > server1 ： server name

5. GW:10.1.1.254
6. vi /etc/hostname

    ```
    serverA 改成 server1
    ```
    > 修改 hostname

7. nmcli con show 
    > 看連線資訊

8. nmcli con del `name`
    >刪除不必要連線

9. nmcli con add type ethernet ifname `eth0` con-name `eth0` ipv4.address ` "10.1.1.157/24" `  ipv4.gateway `10.1.1.254` ipv4.dns `8.8.8.8 ` ipv4.method manual
    > ifname ： 指定連接 <br>
    > ipv4.address ： ip address <br>
    > ipv4.gateway ： GateWay <br>
    > ipv4.dns ： DNS <br>
    > [nmcli 指令全集](https://access.redhat.com/documentation/zh-CN/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/sec-Using_the_NetworkManager_Command_Line_Tool_nmcli.html)

10. systemctl stop sshd 
    > 停止遠端連線

11. sshd `root`@`ipaddress`
    > root ： 遠端連線權限 <br>
    > ipaddress ： ip位置

12. systemctl disable sshd 
    > 關閉遠端連線
    
13. reset_vm `server1`
14. fdisk -l /dev/vda
    > 磁碟分割管理

15. blkid /dev/vdb
    > 看磁碟詳細資料

16. fdisk -l /dev/vdb <br>
    n → p → l → `按ENTER` → +400M → w

17. ls /dev/vdb*
18. blkid /dev/vdb1
19. mkfs.`ext4` /dev/vdb1
    > ext4 ： 磁碟型態 <br>
    > 磁碟格式化