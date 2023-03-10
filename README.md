# ![](https://drive.google.com/uc?id=10INx5_pkhMcYRdx_OO4rXNXxcsvPtBYq) Tmux 入門筆記
> ##### 這篇的操作是以macOS為主，以及常用指令記錄
---
<br>

<!--ts-->
## 目錄
* [安裝](#安裝)
* [基本說明](#基本說明)
* [基本操作](#基本操作)
  * [會話 session](#session)
  * [視窗 window](#window)
  * [切割 pane](#pane)
<!--te-->

---
<br>

## 安裝
- 安裝[Homebrew](https://brew.sh/index_zh-tw.html) <br>
- 裝完後，執行以下命令，安裝`tmux`
```bash
# 安裝tmux套件
brew install tmux
```

```bash
# 查詢tmux版本
tmux -V
```
> tmux 3.0.a

---
<br>

## 基本操作
tmux 除了是一個很方便的終端機畫面管理套件之外，最重要的是，他可以在將session放在機器背景運作，而不會像一般的終端機一樣，視窗關閉後，原本在運行的程序就會關閉. 

`所以最常被用在ssh連線至雲端機器，並且希望關閉ssh之後還可以持續運行在雲端機器的背景上.`

當切換到tmux的環境下，會看到最下方有一條綠色的狀態列
![](https://drive.google.com/uc?id=1Xd-nW0K7Dhug43eD9okNhV6If7V8xPL8)

在tmux的所有快捷操作上，都會有一個預先動作，預設就是按下`control`加上`b`鍵後,會進入等待輸入快捷的狀態，此時在接著按下對應的快捷鍵才會有作用.
> ##### 備註： 快捷鍵的操作，僅限於在切換進入到tmux的環境下使用！

---
<br>

## session
每一個session，可以看做是一個執行緒的終端機，而每個session是各自獨立的.

```bash
# 新增 session
tmux
```

```bash
# 新增 session 並且命名
tmux new -s <new_session_name>
```

```bash
# 重新命名 session
# 可更換現有的session名稱
# 可替只有編號沒有名稱的session命名
tmux rename-session -t <session_name> <new_session_name>
tmux rename-session -t <session_num> <new_session_name>
```

```bash
# 列出所有 session (列表上的第一個數字就是session_num)
tmux ls
```
> 0: 5 windows (created Wed Dec  4 10:02:22 2019) <br>
1: 1 windows (created Wed Dec  4 10:12:14 2019)

<br>

```bash
# 重新連線 session (下列幾種方式都可以)
# session_num 可以從列表中查到
# session_name 新增session時所命名的名稱
# attach 可用縮寫 a 或 at 代替
tmux attach -t <session_num>
tmux attach -t <session_name>
tmux a -t <session_num>
tmux at -t <session_num>
```

```bash
# 刪除 session (下列幾種方式都可以)
# session_num 可以從列表中查到
# session_name 新增session時所命名的名稱
tmux kill-session -t <session_num>
tmux kill-session -t <session_name>

# 保留最後新增的 session 其他session全部刪掉 (session_num 不會歸 0)
tmux kill-session -a

# 刪除全部的 session (session_num 會歸 0)
tmux kill-server
```

<br>

在tmux環境下的快捷組合操作：
|     組合鍵     |  說明  |
| :------------ | :---------- |
| <ctrl+b> + $  | 重新命名目前的 session） |
| <ctrl+b> + d  | 分離目前的 session（detach），暫時退出tmux環境 |
| <ctrl+b> + s  | 以視覺化選單切換 session（select）|
| <ctrl+b> + L  | 切換至上一個使用過的 session|
| <ctrl+b> + (  | 切換至上一個 session |
| <ctrl+b> + )  | 切換至下一個 session |

---
<br>

## window
window就是指整個終端機的畫面，而一個session可以有多個window.

|     組合鍵     |  說明  |
| :------------ | :---------- |
| <ctrl+b> + c  | 建立新 window 視窗（create） |
| <ctrl+b> + w  | 以視覺化選單切換 window 視窗 |
| <ctrl+b> + n  | 切換至下一個 window 視窗（next）|
| <ctrl+b> + p  | 切換至上一個 window 視窗（previous）|
| <ctrl+b> + 數字鍵  | 切換至指定的 window 視窗 <br>備註：對應下方數字 |
| <ctrl+b> + &  | 關閉目前的 window 視窗 |

---
<br>

## pane
每一個window都可以切成多個小區塊，而每個區塊都是一個pane.

|     組合鍵     |  說明  |
| :------------ | :---------- |
| <ctrl+b> + %  | 垂直分割視窗 |
| <ctrl+b> + "  | 水平分割視窗 |
| <ctrl+b> + o  | 以輪流方式輪流切換 pane <br>備註：是英文的o|
| <ctrl+b> + 方向鍵  | 切換至指定方向的 pane <br>備註：↑↓←→|
| <ctrl+b> + 空白鍵  | 切換目前pane的切割佈局 |
| <ctrl+b> + !  | 將目前的 pane 抽出來，獨立建立一個 window 視窗 |
| <ctrl+b> + x  | 關閉目前的 pane <br>備註：下方會跳出確認提示|

---
<br>

## 參考資料
* [官方文件](https://man.openbsd.org/OpenBSD-current/man1/tmux.1)
https://dywang.csie.cyut.edu.tw/dywang/security/node98.html
https://blog.gtwang.org/linux/linux-tmux-terminal-multiplexer-tutorial/

---
<br>

<!--ts-->
## [返回目錄](#目錄)
<!--te-->
