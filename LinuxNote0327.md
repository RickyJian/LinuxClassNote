#  Note 0327
## 實作步驟

1. ssh root@10.1.1.157
2. blkid /dev/db1
3. mount /dev/vdb1 /mnt
    > 將 /dev/vdb1 掛載到 /mnt
    > umount /mnt 刪除掛載

4. df -h
    > 看 partition 並且以 G/M 等容量格式顯示出來

5. for `u` in `{1..100}` do useradd `user${u}` done
    > 新增1～100個使用者，名字為 `user1` 、 `user2` ...

6. echo `user1` | passwd --stdin `user1`
    > 找 user1 並輸入 user1 這個密碼
    > stdin ： 標準輸入

7. vi `create_user`.sh
    > 新增名為 create_user 的 shellscript

    ```
    for u in {1..50}
        do 
            useradd autouser${u}
            echo user${u} | passwd --stdin autouser${u}
        done
    ```

    >  useradd autouser${u} ： 新增使用者 autouser1 ...
    > echo user${u} ： 密碼
    > passwd --stdin autouser${u} ： 更改的帳戶，例如：找出 autouser1 並將密碼更改為 user1

8. chmod +x
9. ./create_user.sh 
    > 執行 create_user 的 shellscript

10. ls -ld user1