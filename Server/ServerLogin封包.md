Server Login 封包
=========================
0. **登入**
	- CtoLLogin
		- AccountType int
		- Account     string // AccountTypeAccount 使用
		- Password    string // AccountTypeAccount 使用
		- UserID      string // AccountTypeUserID 使用, 空字串表示由 server 自動建立試玩帳號
	- LtoDLogin
		- ClientPeerID uint32
		- AccountType  int
		- Account      string
		- Password     string
		- UserID       string
	- DtoLLogin
		- ClientPeerID uint32
		- Result       int
		- AccountID    uint32
		- UserID       string
		- Token        string
	- LtoCLogin
		- Result             int
		- AccountID          uint32
		- UserID             string
		- Token              string
		- LobbyServerAddress string
0. **登入大廳**
	- CtoLbLoginLobby
		- AccountID uint32
		- Token     string
	- LbtoDLoginLobby
		- ClientPeerID uint32
		- AccountID    uint32
		- Token        string
		- ClientIP     string
	- DtoLbLoginLobby
		- ClientPeerID uint32
		- AccountID    uint32
		- Result       int
		- PlayerInfo   SPlayerInfo
	- LbtoCLoginLobby
		- Result           int
		- UserID           string
		- NickName         string
		- Money            int64
		- FreeMoney        int64
		- ImageTemplateID  int
		- ImageCustomID    string
		- IsUseCustomImage bool
0. **登出**
	- CtoLbLogout
	- LbtoCLogout
		- Result int
	- LbtoDLogout
		- AccountID uint32
	- LbtoGLogout
		- AccountID uint32
0. **註冊帳號**
	- CtoLRegisterAccount
		- Account  string
		- Password string
		- UserID   string // 非空字串, 表示綁定試玩帳號
	- LtoDRegisterAccount
		- ClientPeerID uint32
		- Account      string
		- Password     string
		- UserID       string
	- DtoLRegisterAccount
		- ClientPeerID uint32
		- Result       int
		- Account      string
		- Password     string
		- UserID       string
	- LtoCRegisterAccount
		- Result int
		- Account  string
		- Password string
		- UserID   string