ios build
=========================
0. **apple developer**
	- 登入
		- https://developer.apple.com
		- 選擇 Certificates, Identifiers & Profiles
	- 證書
		- Certificates > All，創建證書
		- 此處使用現有的 chimera enterment Co., LTD、iOS Distribution、Sep 19, 2021
		- Download 到 Mac 電腦，雙擊安裝
		- 啟動台 > 其他 > 鑰匙圈存取，確認安裝證書成功
	- App ID
		- Identifiers > App IDs，創建 App ID
		- App ID Description > Name，填 App 名稱，如 Baccarat3D
		- App ID Suffix > Explicit App ID > Bundle ID，填 Bundle ID，如 com.Chimera.Baccarat3D
	- 供應配置文件
		- Provisioning Profiles > All，創建供應配置文件
		- Distribution 選擇 In House
		- App ID 選擇剛建立的 App ID，如 Baccarat3D
		- 證書選擇使用的證書，如 chimera enterment Co., LTD、iOS Distribution、Sep 19, 2021
		- Profile Name，填供應配置文件名稱，如 Baccarat3D
		- Download 到 Mac 電腦，雙擊安裝
	- 安裝 cer.p12
		- 若為使用現有的證書，須從產出方的電腦取出 cer.p12，放到 Mac，雙擊安裝
0. **xcode apple ID 設定**
	- Xcode > preferences，新增 apple ID
0. **unity build**
	- Unity > Preferences > External Tools > Signing Team Id，填使用的 Team ID (可在 apple developer 網頁 Account > Membership 查到)
	- File > Build Settings，選擇 iOS
	- Other Settings > Bundle Identifier，填剛建立的 Bundle ID，如 com.Chimera.Baccarat3D
	- Other Settings > Signing Team Id，填使用的 Team ID (可在 apple developer 網頁 Account > Membership 查到)
	- 選擇 Build
0. **xcode 專案設定**
	- 雙擊 .xcodeproj 開啟
	- 專案設定
		- 點選 Unity-iPhone > General，確定 Identity 資訊正確
		- 確定 Signing > Automatically manage signing 有被勾選
		- 確定 Signing > Team 為使用的 Team，如 chimera enterment Co., LTD
	- 組態設定
		- Unity-iPhone > Edit Scheme
		- Archive > Archive Name: 填 ipa 名稱
0. **手機執行**
	- 連接手機，確定 iTunes 有跳出裝置，如 Chimera 的 iPhone，與 xcode 有抓到裝置
	- 按下執行鈕
0. **ipa 上版**
	- Archive
		- Product > Archive
		- 完成後，按下 Distribute App，選擇 Enterprise distribution method
		- 取消選取 Rebuild from Bitcode
		- 選擇 Export，與 Export 路徑
	- 自備下載連結，配置 plist，參考下述網址
		- https://support.magplus.com/hc/en-us/articles/203808598-iOS-Creating-an-Installation-Link-for-Your-Enterprise-App
		- https://medium.com/@zhongwei0717/ipa-%E7%9A%84-ota-%E4%B9%8B%E6%97%85-%E8%AE%93%E4%BD%A0%E7%9A%84-app-%E4%B8%8D%E9%80%8F%E9%81%8E%E5%85%B6%E4%BB%96%E6%96%B9%E5%BC%8F%E7%9B%B4%E6%8E%A5%E5%AE%89%E8%A3%9D%E5%88%B0%E6%89%8B%E6%A9%9F-749b02f061d7
		- http://clver026.pixnet.net/blog/post/384547450-[ios-xcode]%E5%88%A9%E7%94%A8ad-hoc%E7%99%BC%E4%BD%88app
	- iphone 啟動 app
		- 下載 ipa
		- 設定 > 一般 > 裝置管理 > 信任企業級開發者
		- 開啟 app