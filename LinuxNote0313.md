#  Note 0313
## 實作步驟

1. find /etc -type d network-scripts
2. find /etc -type f -name 'ifcfg-lo'
3. rm -rf d-*
    > find ./d-x | xargs rm -rf <br>
    > find ./iname 'd-*' | xargs rm -rf <br>
    >
    >>  找到東西 丟 後面 <br>
    >
    >以上兩種接等於第三步驟

4. for i in `{1..500}` ; do touch $i ; done
    > 新增資料夾由 1 ～ 500

5. find  `|d|` -iname '*' -type f | xargs rm -rf
    > `|d|` ： file location

6. find ./ -name '[0~9]*' -type -f

7. tail -n 5 /etc/passwd 
    > passwd ： 帳號放置處
    > 看作後5筆資料

8.  tail -n 5 /etc/shadow 
    > shadow ： 密碼放置處
    > 看作後5筆資料

9.  ls -l /etc/{passwd,shadow}
10. useradd `user1`
    > 新增使用者

11. userdel -r `user1`
    > 刪除帳號


12. tail `-n 1` /etc/passwd > /tmp/test.txt
    > n 1 ： 行數
    > 將passwd最後一行貼到 tmp 裡的 test.txt

13. vi /tmp/test.txt
    ```
    autouser1:centos 
    .
    .
    .
    .
    autouser5...
    ```
14. chpasswd < /tmp/test.txt
    > chpasswd ： 大量修改密碼


----
### passwd 檔案

* `User Name:Password:UID:GID:Remark:Home Directory:Shell`

    > User Name ： owner 的帳號 <br>
    > Password ： 原來密碼放置處，現放在 shadow 裡 <br>
    > UID ： 這個就是使用者識別碼 <br>
    >>  UID 為 0 是 root 
    >
    > GID ： 使用這群組 <br>
    > Remark ： 註解 <br>
    > Home Directory ： 定義使用者的家目錄 <br>
    > Shell ： 使用者登入系統後就會取得一個 Shell 來與系統的核心溝通以進行使用者的操作任務

