# TAK Server Tutorial

本教學是在Ubuntu系統上建立TAK Server，使用前需要有TAK的帳號密碼

## Server建立

首先進到[TAK官網](tak.gov)，登入自己的帳號密碼 ![TAK Website Image](/imgs/IMG_0756.jpg)

選擇上方Products > TAK Server Developer Environment Wizard ![Products](/imgs/IMG_0755.jpg)

按照指示完成設定 ![Environment Wizard](/imgs/IMG_0757.jpg)

帳號密碼可以自訂 ![AccPwd](/imgs/IMG_0758.jpg)

Server Details這裡可以Skip ![Server Details Skip](/imgs/IMG_0759.jpg)

完成後會自動下載`tak_server_configurator.zip`，解壓縮後內容如圖所示 ![Configurator](/imgs/IMG_0760.jpg)

執行紅框處`linux-mac-start-here.sh`，跳出的選項都選擇Yes就可以了

之後需要新增一個docker_join.sh在同個資料夾，內容如下：
```bash
sudo docker exec -it -w /opt/tak takserver /bin/bash
```
`linux-mac-start-here.sh`完成後會跳出一個網頁，就是WebTAK (TAK的網頁版本)，到這裡TAK Server就架設完成！

## 金鑰建立

執行剛剛建立的`docker_join.sh`，然後
```bash
cd cert/
```
接著建立金鑰
```bash
source makeCerts.sh client <client_name>
```
完成後會跳到下一層`files/`，裡面就會包含剛建立好的client金鑰

## 匯入金鑰

確保你已經從伺服器的 /opt/tak/certs/files/ 取得了：
1. 用戶名.p12 (身分金鑰)
2. truststore-root.p12 (信任憑證，官方版連線必備)
* 密碼皆預設為： atakatak

### iPhone / iPad (iTAK)

iOS 的安全性較高，建議按以下順序手動操作：
1. 開啟 iTAK，點擊右上角 「齒輪 (Settings)」。
2. 進入 Network -> Servers。
3. 點擊右下角 「+」，選擇 Add Server。
4. 填寫連線資訊：
* Name: 隨意取名（例如 MyTAK）。
* Address: 伺服器的 IP 位址。
* Port: 8089。
* Protocol: 選擇 SSL。
5. 匯入金鑰 (Client Certificate)：
* 在下方找到 Client Certificate 選項。
* 點擊 Import，從「檔案」App 選取你的 [你的名稱].p12。
* 系統會要求密碼，輸入官方預設的 atakatak。
6. 匯入信任憑證 (Trust Store)：
* 找到 Trust Store 選項。
* 點擊 Import，選取 truststore-root.p12。
* 密碼同樣輸入 atakatak。
7. 儲存並連線：
* 點擊右上角 Save。
* 回到 Servers 清單，將該伺服器開關切換為 On。

### Windows (WinTAK)

1. 開啟設定：點擊右側 Settings -> Network -> Server Connections。
2. 新增連線：點擊 Add。
* Address: 輸入伺服器 IP。
* Port: 8089。
* Protocol: 務必選 SSL。
3. 掛載金鑰：
* Client Certificate: 點擊 ... 選取 用戶名.p12，輸入密碼 atakatak。
4. 掛載信任證書（官方版關鍵）：
* Trust Store: 點擊 ... 選取 truststore-root.p12，輸入密碼 atakatak。
5. 啟動：點擊 Apply 並將該伺服器勾選為 Connect。

### Android (ATAK)

Android 建議先匯入憑證，再設定伺服器：
1. 匯入身分金鑰：
* Settings -> Network -> Client Certificate Check。
* 點擊 Import Certificate -> 選取 用戶名.p12 -> 輸入密碼 atakatak。
2. 匯入信任憑證：
* 在同一個頁面點擊 CA Certificate Check 或 Trust Store。
* 匯入 truststore-root.p12。
3. 設定伺服器連線：
* Settings -> Network -> Connection Management -> Add。
* Address: 輸入 IP，Port: 8089。
* Server Type: 選 TAK Server。
* Use SSL/TLS: 切換為 ON。
* Certificate: 點進去選擇剛才匯入的那個 用戶名 憑證。
4. 儲存：點擊 OK，回到清單確認變為綠色。
