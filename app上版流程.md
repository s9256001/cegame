app 上版流程
=========================
0. **版號驗證規則**
	- 連線時取得後端紀錄的 app 版號
	- 若 app 版號的大、中版號一致，則驗證通過
	- 否則跳出最新版 app 下載網頁
0. **改版號**
	- 修改後端紀錄的 app 版號，並提交
		- 檔案位置在 D:\WorkPlace\cegame\env\server\backend\server\client_version.json
		- 如 "Version": "0.12.0"
	- 修改 app 端的版號，並提交
		- 檔案位置在 D:\WorkPlace\cegame\src\client\Baccarat3D\Assets\Script\GameServer.cs
		- 如 Version = "0.12.0";
0. **產出 app**
	- android
		- unity 專案 > cegame > build > Android，編完後 commit
	- IOS
		- unity 專案 > cegame > build > IOS
		- 編完開啟 .xcodeproj 檔，Archive 產出 ipa
		- 將 ipa 搬到類似 D:\WorkPlace\cegame\env\client\ios 路徑，並提交
0. **後端 app 資源更新**
	- 執行 D:\WorkPlace\cegame\env\cmd\linux_control\remote_server_operation.bat
	- 執行 "13. pull server env"