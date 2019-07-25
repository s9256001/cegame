Baccarat3D 封包
=========================
0. **初始資訊**
	- SSeatInfo
		- SeatID          		 int                               // 座位 ID
		- AccountID       		 uint32                            // 帳號 ID
		- NickName        		 string                            // 玩家的暱稱
		- Money           		 int64                             // 玩家的錢
		- FreeMoney       		 int64                             // 玩家的免費錢
		- ImageTemplateID 		 int                               // 樣板圖片 ID
		- ImageCustomID   		 string                            // 自訂圖片 ID
		- ImageLastCustomID      string                            // 上次的自訂圖片 ID
		- Bets            		 [baccaratmathpkg.BetTypeNum]int64 // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
		- PlayerWinBetUpdateTime int64                             // 下注閒家贏的最近 server 時間 (由 1970/1/1 開始算的毫秒數)
		- BankerWinBetUpdateTime int64                             // 下注莊家贏的最近 server 時間 (由 1970/1/1 開始算的毫秒數)
	- GtoCBaccarat3DInit
		- BetRoundCount int // 押注輪次 (1-based)
		- RoundCode string // 局號
		- ShoeLen int // 靴剩餘張數
		- ShoeTailNum int // 靴尾張數 (剩餘張 <= 此張數表示該靴結束)
		- PlayerCardIDs [3]int // 閒家的牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- BankerCardIDs [3]int // 莊家的牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- ViewState int // 顯示用的操作狀態, 0: 無, 1: 洗牌, 2: 押注輪開始, 3: 開始發牌, 4: 閒家發牌咪牌或開牌, 5: 莊家發牌咪牌或開牌, 6: 閒家補牌咪牌或開牌, 7: 莊家補牌咪牌或開牌, 8: 結算
	    - ViewSecs int // 顯示用的 操作秒數
	    - ViewServerTime int64 // 顯示用的 server 時間 (由 1970/1/1 開始算的毫秒數)
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
		- ShoeTailNum int // 靴尾張數 (剩餘張 <= 此張數表示該靴結束)
0. **洗牌**
	- GtoCBaccarat3DShuffle // 廣播
		- ShoeTailNum int // 靴尾張數 (剩餘張 <= 此張數表示該靴結束)
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **押注輪開始**
	- GtoCBaccarat3DBetRoundStart // 廣播
		- BetRoundCount int // 押注輪次 (1-based)
		- RoundCode string // 局號
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
		- ShoeLen int // 靴剩餘張數
		- WaitBetSecs int // 等待押注秒數
0. **發送押注**
	- CtoGBaccarat3DBet
		- Bets [5]int64 // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
	- GtoCBaccarat3DBet // 成功則廣播
		- Bets                   [baccaratmathpkg.BetTypeNum]int64 // 押注, 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
		- PlayerWinBetUpdateTime int64                             // 下注閒家贏的最近 server 時間 (由 1970/1/1 開始算的毫秒數)
		- BankerWinBetUpdateTime int64                             // 下注莊家贏的最近 server 時間 (由 1970/1/1 開始算的毫秒數)
		- SeatID                 int                               // 座位 ID
		- Result                 int                               // 結果
0. **確認押注**
	- CtoGBaccarat3DConfirmBet
0. **開始發牌**
	- GtoCBaccarat3DDeal // 廣播
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **押注結束**
	- GtoCBaccarat3DBetEnd // 廣播
		- PlayerPeekSeatID int // 閒家咪牌的座位 ID, 0: 荷官咪牌
		- BankerPeekSeatID int // 莊家咪牌的座位 ID, 0: 荷官咪牌
0. **咪牌過程**
	- CtoGBaccarat3DPeekProgress
		- Info string // client 自定的夾帶訊息
	- GtoCBaccarat3DPeekProgress // 廣播給其他人
		- Info string // client 自定的夾帶訊息
0. **閒家發牌咪牌或開牌**
	- GtoCBaccarat3DPlayerDealPeek // 廣播
		- CardIDs [2]int // 閒家的兩張牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **閒家發牌咪牌結束**
	- CtoGBaccarat3DPlayerDealPeekEnd
	- GtoCBaccarat3DPlayerDealPeekEnd // 廣播
0. **莊家發牌咪牌或開牌**
	- GtoCBaccarat3DBankerDealPeek // 廣播
		- CardIDs [2]int // 莊家的兩張牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **莊家發牌咪牌結束**
	- CtoGBaccarat3DBankerDealPeekEnd
	- GtoCBaccarat3DBankerDealPeekEnd // 廣播
0. **閒家補牌咪牌或開牌**
	- GtoCBaccarat3DPlayerCallPeek // 廣播
		- CardID int // 閒家的第三牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **閒家補牌咪牌結束**
	- CtoGBaccarat3DPlayerCallPeekEnd
	- GtoCBaccarat3DPlayerCallPeekEnd // 廣播
0. **莊家補牌咪牌或開牌**
	- GtoCBaccarat3DBankerCallPeek // 廣播
		- CardID int // 莊家的第三牌 ID, 1~52, 順序為黑桃 A, 黑桃 2, ..., 黑桃 K, 紅心 A, 紅心 2, ..., 紅心 K, 梅花 A, 梅花 2, ..., 梅花 K, 方塊 A, 方塊 2, ..., 方塊 K
		- PeekSecs int // 咪牌秒數
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **莊家補牌咪牌結束**
	- CtoGBaccarat3DBankerCallPeekEnd
	- GtoCBaccarat3DBankerCallPeekEnd // 廣播
0. **結算**
	- SSeatMoney
		- SeatID    int   // 座位 ID
		- Money     int64 // 玩家的錢
		- FreeMoney int64 // 玩家的免費錢
	- GtoCBaccarat3DSettle // 廣播
		- SeatMoneys []SSeatMoney // 座位的錢列表
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
		- Result uint32 // 各區開獎結果; 各區以 1 bit 表示, 1 代表有開, 0代表沒開; bit 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
0. **此靴的賽果列表**
	- GtoCBaccarat3DGameResults
		- Results []uint32 // 順序依照押注輪次; 各區開獎結果; 各區以 1 bit 表示, 1 代表有開, 0代表沒開; bit 索引分別為 0: 閒, 1: 莊, 2: 和, 3: 閒對, 4: 莊對
0. **一局結束**
	- GtoCBaccarat3DRoundEnd // 廣播
		- ServerTime int64 // server 時間 (由 1970/1/1 開始算的毫秒數)
0. **聊天**
	- CtoGBaccarat3DChat
		- Message string // 訊息
	- GtoCBaccarat3DChat // 廣播
		- SeatID  int    // 座位 ID
		- Message string // 訊息
0. **情緒效果**
	- CtoGBaccarat3DEmotion
		- EmotionID int // 情緒 ID
	- GtoCBaccarat3DEmotion // 廣播
		- SeatID    int // 座位 ID
		- EmotionID int // 情緒 ID