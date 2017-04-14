#  Note 0306
## 實作步驟
1. su -
> 權限切換
2. init-class `31` 
> 網路設定 <br >
> 10.0.0.X
>> X = no * 5 + 1 ～ 5
>>> no = computerNO <br>
3. reboot

## others 
* 開起虛擬機： 應用程式 > 系統工具 > 虛擬機器管理
* date ： 系統時間
* wc ： 行數
* history ： List command 
* ! `82` ： 重複指令
* HISTSIZE = 0  ： 清除指令
* last ： 最近登入時間
* boot ： 開機目錄
* etc ： 系統設定檔
* home ： 使用者家目錄
* tmp ： 暫存檔
* dev ： 硬碟放置區
* var ： 動態檔案

## VI 指令
* HJKL ： 上下左右
* `:set nu` ： 行號
* `:set nu` ： 行號
* NG : 移到檔案第N行
* 1,$s /`replaceTo`/`replace`/g 
> 替換1個 <br>
> replaceTo ： 被替換<br>
> replace ： 替換<br>