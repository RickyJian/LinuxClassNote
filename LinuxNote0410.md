#  Note 0410
## 實作步驟

1. nmcli con show
2. nmcli con mod eth0 `ipv4.dns` "10.1.1.254" 
    > 修改DNS

3. nmcli con up eth0
    > 開啟 eth0 的網路連線

4. ping s31.class.ntub
    > 網路連線傳輸
    >  
    >> 查DNS Route
    >> Cat /etc/hosts
    >> DNS

5. yum install bind-utils
    > 安裝 host  ， dig ， nslookup

6. yum provides */host
    > 查詢特定檔案存在於什麼套件之中 
    > host ： 檔案名稱

7. host classroom.class.ntub `168.95.1.1`
    > 用別人 DNS 查詢

8. nslookup x1.class.ntub
9. curl http://s1.class.ntub
    > curl 和 wget 一樣，是 linux 中檔案下載的指令

10. yum install httpd
11. systemctl start httpd
12. systemctl enable httpd
13. firewall-cmd --permanent --add-service=http
    firewall-cmd --permanent --add-service=https
    > 防火牆設定

14. firewall-cmd --reload
    > 重啟 防火牆

15. iptables -nvL
16. yum install mod_ssl
    > APACHE Server 安裝

17. mount /dev/vdb1 /var/www/html
18. df 
19. cat /etc/fstab
20. vi /etc/fstab
    ```
    /dev/vdb1 /var/www/html ext4 defaults 0 0
    ```
    > fstab：開機自動掛載

21. mount -a
    > 檢查掛載是否有誤

22. restorecon -R -v /var/www/html
    > 恢復成預設的 SELinux type <br>
    > 10.1.1.157/index.html <br>
    > s31.class.ntub

----
* classroom.class.ntub/class/
* GW：10.1.1.254
* /etc/resolv.conf
* ps aux | grep yum  <br>
  kill -p PID