Server Common 封包
=========================
0. **Server 註冊**
	- SutoMaRegister
		- ServerType int
		- ServerID   int
		- ServerKey  string
		- ServerUUID string
		- InitInfo   string
	- MatoSuRegister
		- ServerType int
		- ServerID   int
		- Result     int
		- InitInfo   string
0. **通知關機**
	- DtoSShutdown
		- Reason int // 1: DB 斷線, 2: DataServer 斷線