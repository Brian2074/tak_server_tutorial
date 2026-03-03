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