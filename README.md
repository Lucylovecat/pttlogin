# pttlogin  (批踢踢每日自動登入)
 批踢踢登入的主程式碼很簡單，就是ptt_login.expect，但後續自動排程初始設定很複雜，所以主要這篇主要介紹初始設定
 - 使用 Linux系統 ( Ubuntu)
   1. 先安裝 Linux (最簡單安裝方法)
      * 用系統管理員權限開啟 終端機cmd ，鍵入 `wsl --install`  安裝子系統  Ubuntu (安裝時間約10分鐘，期間需要設定帳號密碼)
      * 更新 Ubuntu  `sudo apt-get update`
   2. 安裝特定特套件
      * `sudo apt install expect`  (安裝更新expect)
      * ，執行  `expect`，查看是否已成功執行
   4. 切換到放置ptt_login.expect程式碼的資料夾，例如 `cd/mnt/d/pttlogin/`  
   5. 測試執行  `./ptt_login.expect  ptt帳號 ptt密碼` 是否成功登入，若成功登入執行下一階段 自動排程
   6. 如果測試不成功，可能是腳本從 Windows環境轉入Ubuntu，相容性不好造成，解決辦法改將ptt_login.expect腳本內容，逐行複製到 expect 解釋器中，再按 Enter 鍵執行，反覆到最後一行
   7. 再重新測試執行  `./ptt_login.expect  ptt帳號 ptt密碼` 是否成功登入，若成功登入執行下一步
   8. 使用 crontab 進行自動排程 `crontab -e`, 第一次編輯 crontab，系統可能會要求你選擇一個編輯器。你可以選擇自己熟悉的編輯器
   9. 假設每天清晨 02:30 執行你的腳本，在 crontab 中新增下列語法，存檔後退出
      *  `30 2 * * * /usr/bin/expect /mnt/d/ptt_login.expect ptt帳號 ptt密碼 && pkill ssh`
      *  (PS 請確保將路徑修改為你的 ptt_login.expect 的正確路徑)
   10. 未來手動執行
        Ubuntu 執行   `/mnt/特定資料夾/ptt_login.expect ptt帳號 ptt密碼`     
   

 - 使用 Windows系統 (還沒測試成功)
   * 1.先至 tclsh官網安裝  tclsh  (文獻有提及，但網路找不到，可能年代久遠已下架)
   * 2.建立bat批次檔，檔名可取名為 run_ptt_login.bat 
     ```Bash
        @echo off
        cd /d "path\to\script\directory"
        tclsh ptt_login_unix.expect ptt帳號 ptt密碼
     ```
   * 3.設定工作排程器
    1. 打開 Windows 的工作排程器。依照以下步驟來建立一個新的計劃任務：
    2. 點擊 "建立基本工作"。
    3. 選擇 "每天"，然後點擊 "下一步"。
    4. 選擇一個開始時間，然後點擊 "下一步"。
    5. 選擇 "啟動程式"，然後點擊 "下一步"。
    6. 在 "程式/指令碼" 欄位中，瀏覽並選擇你剛剛建立的 .bat 檔案。
    7. 在 "起始於" 欄位中，指定 .bat 檔案所在的目錄。
    8. 點擊 "下一步"，然後點擊 "完成" 來建立計劃任務   

## 參考資料
 1. https://uwaylu.github.io/blog/2021/03/04/ptt%E6%AF%8F%E6%97%A5%E8%87%AA%E5%8B%95%E7%99%BB%E5%85%A5/

