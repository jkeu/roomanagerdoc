# 房卡管理

## 会员

### 注册

会员可以通过网页注册，也可以通过接口注册，若通过接口注册，游戏客户端需要实现注册界面

1. 网页注册: https://mydomain.com/user/signup.html
2. 接口: https://mydomain.com/api/user/signup
3. 输入: (http get method) user, password (使用 RSA 加密)
4. 输出: {"result" : "ok"}
5. 错误: {"result" : "some error"}
6. 加密公钥:
````
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDlOJu6TyygqxfWT7eLtGDwajtN
FOb9I5XRb6khyfD1Yt3YiCgQWMNW649887VGJiGr/L5i2osbl8C9+WJTeucF+S76
xFxdU6jE0NQ+Z+zEdhUTooNRaY5nZiu5PgDB0ED/ZKBUSLKL7eibMxZtMlUDHjm4
gwQco1KRMDSmXSMkDwIDAQAB
-----END PUBLIC KEY-----
````

### 登录

游戏客户端需要实现登录界面，通过接口登录后，保存返回的 TOKEN，后面的接口都需要使用 TOKEN 进行鉴权

1. 调试界面: https://mydomain.com/user/signin.html
2. 接口: https://mydomain.com/api/user/login
3. 输入: (http get method) user, password (使用 RSA 加密)
4. 输出: {"token" : "TOKEN", "user" : "username"}
5. 错误: {"result" : "some error"}
6. 加密公钥:
````
-----BEGIN PUBLIC KEY-----
MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQDlOJu6TyygqxfWT7eLtGDwajtN
FOb9I5XRb6khyfD1Yt3YiCgQWMNW649887VGJiGr/L5i2osbl8C9+WJTeucF+S76
xFxdU6jE0NQ+Z+zEdhUTooNRaY5nZiu5PgDB0ED/ZKBUSLKL7eibMxZtMlUDHjm4
gwQco1KRMDSmXSMkDwIDAQAB
-----END PUBLIC KEY-----
````

### 积分

用户通过房主进行加减积分，实际交收线下完成，房主可通过网页管理旗下会员的积分

- 网页: https://mydomain.com/room/index.html


## 游戏

### 进入房间

游戏客户端需要实现房间号码输入界面，通过接口访问确定用户有权限可以进入房间

1. 接口: https://mydomain.com/api/user/accountGet
2. 输入: (http get method) TOKEN, user, room
3. 输出: 帐户对象
4. 错误: {"result" : "some error"}
5. 帐户对象:
````
type AccountInfo struct {
	AID       int    `json:"aid"`
	UID       int    `json:"uid"`
	Username  string `json:"username"`
	RID       int    `json:"rid"`
	RoomNo    string `json:"roomno"`
	Balance   int    `json:"balance"`
	AmountIn  int    `json:"amountin"`
	AmountOut int    `json:"amountout"`
	Status    int    `json:"status"`
	Created   int64  `json:"created"`
}
````

### 获取游戏结果

用户点击下注或转动轮盘时，通过接口获取本局结果，游戏客户端根据结果显示动画

服务器在提供结果时已经计算盈利并保存用户积分的变化

每次获取游戏结果需要消耗房间的积分，房间积分由区域代理管理

1. 接口: https://mydomain.com/api/user/gameRun
2. 输入: (http get method) TOKEN, user, room, amount
3. 输出: 根据游戏类型返回不同对象
4. 错误: {"result" : "some error"}
5. 游戏结果对象:
````
type GameResultInfo struct {
	GID       int    `json:"gid"`
	AID       int    `json:"aid"`
	...
	Amount    int    `json:"amount"`
	Created   int64  `json:"created"`
}
````


## 房主

coming soon

### 邀请会员

发展会员是房主最主要的工作

### 踢出会员

### 增加积分

等于充值，为会员增加积分是房主持续发展的推动力

### 减少积分

等于提款

### 查询会员积分记录

### 查询会员盈利记录

### 查看房间内会员报表

### 查询房间积分


## 区域代理

coming soon

### 邀请房主

发展房主是区域代理最主要的工作

### 增加积分

房间充值，为房主增加积分是区域代理持续发展的推动力

### 查看区域内房间报表




