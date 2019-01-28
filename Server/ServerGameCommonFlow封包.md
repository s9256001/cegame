Baccarat3D 封包
=========================
0. **押注**
	- SServerBetRequest
		- ClientPeerID uint32
		- AccountID    uint32
		- Bet          int64
		- Detail       string
	- GtoDBet
		- GameID    int
		- GameLevel int
		- RoundCode string
		- Bets      []SServerBetRequest
	- SServerBetResult
		- ClientPeerID uint32
		- AccountID    uint32
		- Result       int
		- BetID        uint64
		- Money        int64
	- DtoGBet
		- GameID    int
		- GameLevel int
		- RoundCode string
		- Bets      []SServerBetResult
0. **結算**
	- SServerSettleRequest
		- ClientPeerID uint32
		- AccountID    uint32
		- BetID        uint64
		- Win          int64
		- Detail       string
	- GtoDSettle
		- GameID    int
		- GameLevel int
		- RoundCode string
		- Settles   []SServerSettleRequest
	- SServerSettleResult
		- ClientPeerID uint32
		- AccountID    uint32
		- Result       int
		- Money        int64
	- DtoGSettle
		- GameID                    int
		- GameLevel                 int
		- RoundCode                 string
		- Settles                   []SServerSettleResult
		- TotalWin                  int64
		- TotalMonthlyWin           int64
		- TotalMonthlyWinCreateTime time.Time
0. **賽果**
	- GtoDGameResult
		- GameID    int
		- GameLevel int
		- RoundCode string
		- Result    string
		- Detail    string
0. **更新 Server 總輸贏**
	- DtoGUpdateServerTotalWin
		- TotalWin                  int64
		- TotalMonthlyWin           int64
		- TotalMonthlyWinCreateTime time.Time
0. **更新遊戲賽果歷史**
	- GtoLbUpdateGameResults
		- GameID      int
		- GameLevel   int
		- RoomID      int
		- GameResults string
0. **儲存房間資料**
	- GtoDSaveRoomData
		- GameID    int
		- GameLevel int
		- RoomID    int
		- Data      string