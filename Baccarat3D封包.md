Baccarat3D 封包
=========================
0. **測試直連遊戲**
	- CtoGTestJoinGame
		- UserID string // 使用者唯一碼
	- GtoCTestJoinGame
		- GameID int // 遊戲 ID
		- RoomID int // 房間 ID
		- SeatID int // 座位 ID
		- Result int // 結果
		- MaxPlayerBet int64 // 個人限紅
		- ValidBets []int64 // 可押注選項
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **測試離開遊戲**
	- CtoGTestLeaveGame
	- GtoCTestLeaveGame
		- Result int // 結果
0. **初始資訊**
	- SSeatInfo
		- SeatID int // 座位 ID
		- AccountID int // 帳號 ID
		- Account string // 玩家的帳號
		- NickName string // 玩家的暱稱
		- Money int64 // 玩家的錢
	- GtoCBaccarat3DInit
		- RoundCode string // 局號
		- ShoeTailNum int // 靴尾張數 (剩餘張 <= 此張數表示該靴結束)
		- PlayerCardIDs [3]int // 閒家的牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- BankerCardIDs [3]int // 莊家的牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- SeatInfos []SSeatInfo // 座位資訊列表
0. **玩家進入**
	- GtoCBaccarat3DPlayerJoin
		- SeatInfo SSeatInfo // 座位資訊
0. **玩家離開**
	- GtoCBaccarat3DPlayerLeave
		- SeatID int // 座位 ID
0. **一局開始**
	- GtoCBaccarat3DRoundStart // 廣播
		- RoundCode string // 局號
0. **洗牌**
	- GtoCBaccarat3DShuffle // 廣播
		- ShoeTailNum int // 靴尾張數 (剩餘張 <= 此張數表示該靴結束)
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **押注輪開始**
	- GtoCBaccarat3DBetRoundStart // 廣播
		- RoundCode string // 局號
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **發送押注**
	- CtoGBaccarat3DBet
		- Bets [5]int64 // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
	- GtoCBaccarat3DBet // 成功則廣播
		- Bets [5]int64 // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
		- SeatID int // 座位 ID
		- Result int // 結果
0. **確認押注**
	- CtoGBaccarat3DConfirmBet
0. **開始發牌**
	- GtoCBaccarat3DDeal // 廣播
	- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **押注結束**
	- GtoCBaccarat3DBetEnd // 廣播
		- PlayerPeekSeatID int // 閒家咪牌的座位 ID, 0: 荷官咪牌
		- BankerPeekSeatID int // 莊家咪牌的座位 ID, 0: 荷官咪牌
0. **閒家發牌咪牌或開牌**
	- GtoCBaccarat3DPlayerDealPeek // 廣播
		- CardIDs [2]int // 閒家的兩張牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **閒家發牌咪牌過程**
	- CtoGBaccarat3DPlayerDealPeekProgress
		- Info string // client 自定的夾帶訊息
	- GtoCBaccarat3DPlayerDealPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **閒家發牌咪牌結束**
	- CtoGBaccarat3DPlayerDealPeekEnd
	- GtoCBaccarat3DPlayerDealPeekEnd // 廣播
0. **莊家發牌咪牌或開牌**
	- GtoCBaccarat3DBankerDealPeek // 廣播
		- CardIDs [2]int // 莊家的兩張牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **莊家發牌咪牌過程**
	- CtoGBaccarat3DBankerDealPeekProgress
		- Info string // client 自定的夾帶訊息
	- GtoCBaccarat3DBankerDealPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **莊家發牌咪牌結束**
	- CtoGBaccarat3DBankerDealPeekEnd
	- GtoCBaccarat3DBankerDealPeekEnd // 廣播
0. **閒家補牌咪牌或開牌**
	- GtoCBaccarat3DPlayerCallPeek // 廣播
		- CardID int // 閒家的第三牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **閒家補牌咪牌過程**
	- CtoGBaccarat3DPlayerCallPeekProgress
		- Info string // client 自定的夾帶訊息
	- GtoCBaccarat3DPlayerCallPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **閒家補牌咪牌結束**
	- CtoGBaccarat3DPlayerCallPeekEnd
	- GtoCBaccarat3DPlayerCallPeekEnd // 廣播
0. **莊家補牌咪牌或開牌**
	- GtoCBaccarat3DBankerCallPeek // 廣播
		- CardID int // 莊家的第三牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **莊家補牌咪牌過程**
	- CtoGBaccarat3DBankerCallPeekProgress
		- Info string // client 自定的夾帶訊息
	- GtoCBaccarat3DBankerCallPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **莊家補牌咪牌結束**
	- CtoGBaccarat3DBankerCallPeekEnd
	- GtoCBaccarat3DBankerCallPeekEnd // 廣播
0. **結算**
	- SSeatMoney
		- SeatID int // 座位 ID
		- Money int64 // 玩家的錢
	- GtoCBaccarat3DSettle // 廣播
		- SeatMoneys []SSeatMoney // 座位的錢列表
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)