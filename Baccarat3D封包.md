Baccarat3D 封包
=========================
0. **測試直連遊戲**
	- C2GTestJoinGame
	- G2CTestJoinGame
		- GameID int // 遊戲 ID
		- RoomID int // 房間 ID
		- SeatID int // 座位 ID
		- Result int // 結果
		- Money int // 玩家的錢
0. **一局開始**
	- G2CBaccarat3DRoundStart // 廣播
		- RoundCode string // 局號
0. **押注輪開始**
	- G2CBaccarat3DBetRoundStart // 廣播
		- RoundCode string // 局號
0. **發送押注**
	- C2GBaccarat3DBet
		- Bets [5]int // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
	- G2CBaccarat3DBet // 成功則廣播
		- Bets [5]int // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
		- SeatID int // 座位 ID
		- Result int // 結果
0. **確認押注**
	- C2GBaccarat3DConfirmBet
0. **開始發牌**
	- G2CBaccarat3DDeal // 廣播
0. **更新押注後的錢**
	- G2CBaccarat3DUpdateMoneyForBet // 廣播/押注 Lag 時更新該玩家的錢
		- Money int // 玩家的錢
0. **閒家發牌咪牌或開牌**
	- G2CBaccarat3DPlayerDealPeek // 廣播
		- PeekSeatID int // 咪牌的座位 ID, 0: 荷官咪牌
		- CardKind [2]int // 閒家的兩張牌的花色, 0: 黑桃, 1: 紅心, 2: 梅花, 3: 方塊
		- CardValue [2]int // 閒家的兩張牌的牌值, 1: A, 2: 2, ..., 10: T, ..., 13: K
		- PeekSecs int // 咪牌秒數
0. **閒家發牌咪牌過程**
	- C2GBaccarat3DPlayerDealPeekProgress
		- Info string // client 自定的夾帶訊息
	- G2CBaccarat3DPlayerDealPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **閒家發牌咪牌結束**
	- C2GBaccarat3DPlayerDealPeekEnd
	- G2CBaccarat3DPlayerDealPeekEnd // 廣播
0. **莊家發牌咪牌或開牌**
	- G2CBaccarat3DBankerDealPeek // 廣播
		- PeekSeatID int // 咪牌的座位 ID, 0: 荷官咪牌
		- CardKind [2]int // 閒家的兩張牌的花色, 0: 黑桃, 1: 紅心, 2: 梅花, 3: 方塊
		- CardValue [2]int // 閒家的兩張牌的牌值, 1: A, 2: 2, ..., 10: T, ..., 13: K
		- PeekSecs int // 咪牌秒數
0. **莊家發牌咪牌過程**
	- C2GBaccarat3DBankerDealPeekProgress
		- Info string // client 自定的夾帶訊息
	- G2CBaccarat3DBankerDealPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **莊家發牌咪牌結束**
	- C2GBaccarat3DBankerDealPeekEnd
	- G2CBaccarat3DBankerDealPeekEnd // 廣播
0. **閒家補牌咪牌或開牌**
	- G2CBaccarat3DPlayerCallPeek // 廣播
		- PeekSeatID int // 咪牌的座位 ID, 0: 荷官咪牌
		- CardID [2]int // 閒家的第三牌的 ID
		- PeekSecs int // 咪牌秒數
0. **閒家補牌咪牌過程**
	- C2GBaccarat3DPlayerCallPeekProgress
		- Info string // client 自定的夾帶訊息
	- G2CBaccarat3DPlayerCallPeekProgress // 廣播給其他人
		- PeekSeatID int // 咪牌的座位 ID
		- Info string // client 自定的夾帶訊息
0. **閒家補牌咪牌結束**
	- C2GBaccarat3DPlayerCallPeekEnd
	- G2CBaccarat3DPlayerCallPeekEnd // 廣播
0. **莊家補牌咪牌或開牌**
	- G2CBaccarat3DBankerCallPeek // 廣播
		- PeekSeatID int // 咪牌的座位 ID, 0: 荷官咪牌
		- CardID [2]int // 莊家的第三牌的 ID
		- PeekSecs int // 咪牌秒數
0. **莊家補牌咪牌過程**
	- C2GBaccarat3DBankerCallPeekProgress
		- Info string // client 自定的夾帶訊息
	- G2CBaccarat3DBankerCallPeekProgress // 廣播給其他人
		- PeekSeatID int // 咪牌的座位 ID
		- Info string // client 自定的夾帶訊息
0. **莊家補牌咪牌結束**
	- C2GBaccarat3DBankerCallPeekEnd
	- G2CBaccarat3DBankerCallPeekEnd // 廣播
0. **結算**
	- G2CBaccarat3DSettle // 廣播
		- PlayerPairWin int // 閒對贏錢
		- BankerPairWin int // 莊對贏錢
		- TotalWin int // 總贏錢
		- Money int // 玩家的錢