microsoft DB
=========================
0. **註冊**
    - SP_CreateMember
    - 參數
    ~~~
    CardName  VARCHAR(50)     -- 帳號
    Password  VARCHAR(64)     -- 密碼
    NickName  NVARCHAR(20)    -- 暱稱
    Email     NVARCHAR(50)='' -- 電子信箱
    ~~~
    - 回傳
        - 0: 成功, 1: 失敗, 2: 帳號重覆, 3: 暱稱重覆
0. **登入**
    - sp_Login_04_CheckAccountByGame
    - 參數
    ~~~
    sAccount      VARCHAR(128)    -- 帳號
    sPassword     VARCHAR(64)     -- 密碼
    sPLIP         VARCHAR(32)     -- IP
    ~~~
    - 回傳
        - 0: 正常登入, 1: 無此帳號, 2: 密碼錯誤, 3: 本身帳號停用, 4: 密碼錯誤超過次數, 5: 非會員帳號, 99: 登入錯誤
    - 回傳列表
    ~~~
    (點數為真錢 * 100)
    MemberID       int        -- 會員編號
    Exps           int64      -- 經驗值
    MemberLevel    int        -- 等級
    SportsRate     float64    -- 運動類遊戲比值
    RealRate       float64    -- 真人類遊戲比值
    GameRate       float64    -- 電子類遊戲比值
    LotteryRate    float64    -- 彩票類遊戲比值
    NickName       string     -- 暱稱
    PicURL         string     -- 照片連結網址
    AlarmType      int        -- 緊急設定
    WarPoints      int64      -- 戰點
    Points         int64      -- 有價幣幣點數
    Deposits       int64      -- 免費幣點數
    WagerPoints    int64      -- 電子錢包點數
    LottoPoints    int64
    MainPoints     int64
    Bonus          int64      -- 累積紅利
    MemberPassword string
    MemberAccount  string
    ~~~
0. **帶入錢**
    - sp_Game_26_WagerBuyIn
    - 參數
    ~~~
    BuyInPLUniID  INT         -- 玩家唯一識別碼
    PointsType    INT         -- 幣別; 0: 有價幣幣點數, 1: 免費幣點數
    nPoints       BIGINT      -- 買入點數
    ~~~
    - 回傳
        0: 成功, 1: 失敗, 2: Wager 尚有點數, 3: 會員點數資料不存在, 4: buyin 點數大於存簿點數, 5: 會員不存在
    - 回傳列表
    ~~~
    WagerPoints       BIGINT              -- 電子錢包點數
    TopFanShuiRate    DECIMAL(5, 2)       -- 頂層代理遊戲退水比例
    FanShuiRate       DECIMAL(5, 2)       -- 玩家遊戲退水比例
    AllowBet          TINYINT             -- 玩家是否可以下注
    ~~~
0. **回存錢**
    - sp_Game_27_WagerCancel
    - 參數
    ~~~
    PLUniID       INT         -- 玩家唯一識別碼
    PointsType    INT         -- 幣別; 0: 有價幣幣點數, 1: 免費幣點數
    ~~~
    - 回傳
        0: 成功, 1: 失敗, 3: 會員點數資料不存在, 5: 會員不存在
    - 回傳列表
    ~~~
    MemberId          int
    Points            int64
    Deposits          int64
    WagerPoints       int64      -- 電子錢包點數
    ~~~
0. **結算**
    - sp_GameRecord_01_Winlose_Rate
    - 參數
    ~~~
    MemberId          INT                 -- 會員編號
    GameMode          INT                 -- 幣別; 0: 有價幣幣點數, 1: 免費幣點數
    GameId            INT                 -- 遊戲編號
    TableId           INT                 -- 遊戲桌(機台)編號
    RoundId           INT                 -- 局數
    RoundCode         VARCHAR(20) = ''    -- 局號(將號)
    Bet               BIGINT              -- 押注值(計算抽水)(象棋麻將嬴家押注0，輸家為正數)
    GetJPMoney        BIGINT              -- 取得彩金值
    WinLose           BIGINT              -- 輸贏值(加減點數)(象棋麻將嬴家輸嬴值為正數，輸家為負數)
    CommBase          BIGINT              -- 洗碼量(有效投注)(與@Bet重覆)
    CurrentPoints     BIGINT              -- 當局結束後玩家剩餘點數 (改由db自行計算)
    BetState          NVARCHAR(MAX) =''   -- 押注狀態
    WinLoseState      NVARCHAR(MAX) =''   -- 輸贏狀態
    CreateDate        DATETIME            -- 時間
    Score             Int
    Total             Int
    Win               Int
    Loss              Int
    Draw              Int
    Level             Int
    Fame              Int
    Custom1           Int
    Custom2           Int
    Custom3           Int
    Custom4           Int
    Custom5           Int
    Custom6           Int
    Custom7           Int
    Custom8           Int
    Custom9           Int
    Custom10          Int
    ~~~
    - 回傳
        0: 成功, 1: 失敗, 2: 帳號不存在, 4: 遊戲編號不存在