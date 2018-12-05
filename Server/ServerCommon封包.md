Server Common 封包
=========================
0. **Server 註冊**
	- SutoMaRegister
		- ServerType int
		- ServerID   int
		- ServerName string
		- ServerIP   string
		- ServerPort int
		- Info       string
		- ServerKey  string
		- ServerUUID string
	- MatoSuRegister
		- ServerType int
		- ServerID   int
		- Result     int
		- Info       string
0. **通知關機**
	- DtoSShutdown
		- Reason int