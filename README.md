# 金贝数字货币交易所系统Rest API接口清单v2.2

金贝为用户提供了一个简单的而又强大的API，旨在帮助用户快速高效的将金贝数字货币交易所功能整合到自己应用当中。如果在使用过程中有任何问题，请电话咨询，我们将为您做出及时的解答，请求参数post方式提交需要进行参数签名。

# **1.** ***行情API***

## **1.1** ***获取最新市场行情数据***

 

1.接口路径：/exapi/api/klinevtwo/message
2.请求方式：POST
3.请求参数：无

4,返回参数：

| ***名称***   | ***必填*** | ***类型***                      | ***说明*** |
| ------------ | ---------- | ------------------------------- | ---------- |
| marketDetail | 是         | Map<String, List<MarketDetail>> | 市场细节   |
| productList  | 是         | List<String>                    | 产品清单   |

 

示例：

 

 

| ***接口***                                                   | ***描述***                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ***示例***                                                   | //# Response marketDetail:{,…}, productList:["BTC_LTC", "BTC_USDT", "LTC_USDT", "BTC_USD", "LTC_USD", "BCC_BTC", "ETH_BTC", "QTUM_USDT",…] lastKLine{}, |
| ***参数说明***                                               | marketDetail:市场细节productList：产品清单lastKLine:k线数据  |
| marketDetail：{BCC_BTC具体产品:[｛idCur:时间戳idPrev:  id前缀msgType: 消息类型payload:{...} 交易信息[单独说明见下一栏]symbolId:交易对version:版本_id:时间戳｝]} |                                                              |
| ***Payload 说明***amount:0 amp:null  待定。。asks:{price: 成交价格, amount: 成交量, level: 待定}  委托卖amount:null level:null 与最新成交价相等price:nullbids:{price: 成交价格, amount: 成交量, level: 待定。。}  委托买commissionRatio:0 innerDisc:0level:0outerDisc:0poor:0priceAverage:0priceHigh:0 最高价priceLast:0priceLow:0  最低价priceNew:0 最新成交价priceOpen:0 开盘价symbolId:"btccny"totalAmount:0  弃用totalVolume:  成交量trades:{price: 成交价格, amount: 成交量l, direction: 成交内盘外盘, time: 成交时间} 成交数据turnVolume:0turnoverRate:0updownRatio:0updownVolume:0volumeRatio:0yestdayPriceLast: priceLastsymbolId:"BCC_BTC"version:1_id:1516340689 |                                                              |

 

/exapi/api/klinevtwo/data

# **2.** ***交易API***

用于通过接口快速进行交易

## ***2.1委托下单***

 

1.接口路径：exapi/api/trade/order
2.请求方式：POST
3.***请求参数***：

| 名称         | 必填 | 类型   | 说明                                                    |
| ------------ | ---- | ------ | ------------------------------------------------------- |
| entrustPrice | 是   | String | 价格                                                    |
| type         | 是   | String | 1，买，2，卖                                            |
| coinCode     | 是   | String | 交易对                                                  |
| entrustCount | 是   | String | 数量                                                    |
| accesskey    | 是   | String | 签名公钥（后台用户管理申请的可以id公钥）                |
| sign1        | 是   | String | 签名值（顺序：entrustPrice+type+coinCode+entrustCount） |

***返回参数:***

| 名称    | 必填 | 类型   | 说明                           |
| ------- | ---- | ------ | ------------------------------ |
| Success | 是   | String | Ture,false                     |
| Msg     | 是   | String | 返回说明                       |
| Object  | 是   | 无     | 此方法无返回对象               |
| code    | 是   | String | 成功：8888（具体参考返回编码） |

## ***2.2取消全部委托***

1.接口路径：exapi/api/trade/cancelOrder
2.请求方式：POST
3.***请求参数***：

| 名称      | 必填 | 类型   | 说明                                     |
| --------- | ---- | ------ | ---------------------------------------- |
| coinCode  | 是   | String | 交易对                                   |
| accesskey | 是   | String | 签名公钥（后台用户管理申请的可以id公钥） |
| sign1     | 是   | String | 签名值（顺序： coinCode）                |

***返回参数:***

| 名称    | 必填 | 类型   | 说明                           |
| ------- | ---- | ------ | ------------------------------ |
| Success | 是   | String | Ture,false                     |
| Msg     | 是   | String | 返回说明                       |
| Object  | 是   | 无     | 此方法无返回对象               |
| code    | 是   | String | 成功：8888（具体参考返回编码） |

 

## ***2.3获取我的委托***

接口路径：exapi/api/user/singleExEntrust
2.请求方式：POST


3.***请求参数***：

| 名称      | 必填 | 类型   | 说明                                           |
| --------- | ---- | ------ | ---------------------------------------------- |
| limit     | 是   | String | 显示条数                                       |
| offset    | 是   | String | 从第几条开始                                   |
| sortOrder | 是   | String | 排序（asc，dec）                               |
| querypath | 是   | String | current                                        |
| accesskey | 是   | String | 签名公钥（后台用户管理申请的可以id公钥）       |
| sign1     | 是   | String | 签名值（顺序limit+offset+sortOrder+querypath） |

 

***返回参数:***

 

| 名称    | 必填 | 类型      | 说明                           |
| ------- | ---- | --------- | ------------------------------ |
| Success | 是   | String    | Ture,false                     |
| Msg     | 是   | String    | 返回说明                       |
| Object  | 是   | FrontPage | 分页对象                       |
| code    | 是   | String    | 成功：8888（具体参考返回编码） |

 

返回类型说明:

| ***示例*** | //# RequestAccesskey：供钥limit:显示的条数offset: 从第几条开始显示sortOrder: 显示的顺序querypath: 查询数据的类型sign1:数签//# Response{FrontPage： {  Integer page;// 要查找第几页	 Integer pageSize;// 每页显示多少条	 Long totalPage = 0L;// 总页数	 Long recordsTotal;// 总记录数	 Long recordsFiltered;// 过滤后记录数	 List rows;// 结果集	 Long  total;//总记录数 }<List<Entrust>> Rows：{Entrust：{//委托	 String entrustNum;	//委托时间	 Date entrustTime;	//时间戳	 Long entrustTime_long;  // 委托的来源 (1. 表示人工pc 2. 表示 机器人3.表示人工移动端 4.强制平仓系统生成,5计划委托，6，止盈平仓系统生成，7止损平仓系统生成)	 ***int*** source;	// 委托价格	 BigDecimal entrustPrice;	// 委托数量	 BigDecimal entrustCount;	// TYPE 类型 1 ： 买 2 ： 卖	 ***int*** type;	// 委托剩余数量	 BigDecimal surplusEntrustCount;	// STATUS 状态 ---> 0未成交　1部分成交　2已完成　 3部分成交已撤销 4已撤销 	 ***int*** status;	//成交金额	 BigDecimal transactionSum;	//委托金额	 BigDecimal entrustSum;	//成交平台价格	 BigDecimal processedPrice;	//币代码	 String coinCode;	//定价币	 String fixPriceCoinCode;}} |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

## ***2.4获取用户信息***

1.接口路径：exapi/api/user/getAccountInfo
2.请求方式：POST
3.***请求参数***：

| 名称      | 必填 | 类型   | 说明                                     |
| --------- | ---- | ------ | ---------------------------------------- |
| accesskey | 是   | String | 签名公钥（后台用户管理申请的可以id公钥） |
| sign1     | 是   | String | 签名值（顺序：accesskey）                |

***返回参数:***

| 名称    | 必填 | 类型                | 说明                           |
| ------- | ---- | ------------------- | ------------------------------ |
| Success | 是   | String              | Ture,false                     |
| Msg     | 是   | String              | 返回说明                       |
| Object  | 是   | Map<String, Object> |                                |
| code    | 是   | String              | 成功：8888（具体参考返回编码） |

 

| ***示例*** | //# Responseobj {  isChongbi：是否开启充币需要实名认证 （0 开 1关）isTrade:是否开启交易需要实名认证（ 0开 1关）isTibi：是否开启提币需要实名认证（0开1关）   witfee:提现手续费率   maxWithdrawMoneyOneTime:一次最大提现   languageCode:定价币   maxWithdrawMoney:一天最大提现   List<CoinAccount> coinAccount: {  CoinAccount：{    // 币的id 在wap端使用 	   Long id;	  //币代码	   String coinCode;	  // 可用总额	   BigDecimal hotMoney;	 // 冻结总额	   BigDecimal coldMoney;	 //币的名字	  String name;	 //币的类型	  String currencyType;	 //虚拟账号	  String accountNum;	 //为手机端使用	  String tokenId;	 //币的保留几位小数	  Integer keepDecimalForCoin;	 //api使用0为法币1为虚拟货币	 Integer moneyAndCoin;  }       user: {     //用户名/手机号	     String username;		    //密码	     String password;		    //用户唯一标识	     String userCode;		    //是否实名0没有实名，1实名	      ***int*** isReal;  	     //是否能交易  0可以交易  1不能交易	      ***int*** isChange;  	     //是否禁用  0没有禁用 1禁用	     ***int*** isDelete; 		     //是否锁定  0没锁定  1锁定	     ***int*** isLock;		     //邮箱认证 0否 1是	     ***int*** isEmail;		    //交易密码	     String accountPassWord;		//前台用户id	     Long customerId;			    //用户邮箱	     String mobile;		    //真实名	     String truename;	    //真实姓	     String surname;	//`customerType` int(5) DEFAULT '1' COMMENT '客户类型customerType甲类账户1(普通的，默认)，乙类账号2，丙类账户3'	     ***int*** customerType;		   //盐	     String salt;		   //身份证	     String cardcode;		    //邮箱	     String email;		    //性别	     Integer sex;		    //详细地址	     String postalAddress;	   //谷歌认证状态(0否，1是)	     Integer googleState;		    //申请ip	     String messIp;		    //手机号	     String phone;	  //手机认证状态(0否，1是)	     Integer phoneState;		//0 未实名 1 待审核 2 已实名 3 已拒绝	     Integer states;	    //用户登录uuid	     String uuid;	     //是否管理员	     Integer isAdmin;	     //是否禁言	     Integer isGag;	    },    info: {      //真实名	     String trueName;	    //国家	     String country;	    //证件类型	     String cardType;	    //证件号	     String cardId;	    //姓	     String surname;	    //证件名称	     String papersType;	    //证件类型      (2护照 1身份证)	     String type;     },} |
| ---------- | ------------------------------------------------------------ |
|            |                                                              |

## ***2．9取消指定委托***

\1. 接口路径：exapi/api/user/singleRevocation
2.请求方式：POST


3.***请求参数***：

| 名称       | 必填 | 类型   | 说明                                     |
| ---------- | ---- | ------ | ---------------------------------------- |
| entrustNum | 是   | String | 单号                                     |
| accesskey  | 是   | String | 签名公钥（后台用户管理申请的可以id公钥） |
| sign1      | 是   | String | 签名值顺序（entrustNum）                 |

 

***返回参数:***

 

| 名称    | 必填 | 类型   | 说明                           |
| ------- | ---- | ------ | ------------------------------ |
| Success | 是   | String | Ture,false                     |
| Msg     | 是   | String | 返回说明                       |
| code    | 是   | String | 成功：8888（具体参考返回编码） |

 

## ***3.0 获取K线数据接口***

接口路径：klineApi/getkline/{交易对} /{period}

period取值**1min,5min,15min,30min,60min,1day,1week,1mon**

返回值说明

amout成交量

lowPrice 最低价

highPrice 最高价

openPrice 开盘价

closePrice 收盘价

time 时间戳

 

## ***3.1 获取所有交易行情***

1.接口路径：/exapi/api/v1/allTicker
2.请求方式：POST/GET
3.请求参数：无

4,返回参数：

date: 返回数据时服务器时间 格式yyyy-MM-dd HH:mm:ss

Ticker[{

symbol: 交易对（交易对1简称_交易对2简称） 

buy: 买一价 

high: 最高价 

last: 最新成交价 

low: 最低价 

sell: 卖一价 

vol: 成交量(最近的24小时) 

change:涨跌幅 

}..]

 

 

 

 

公钥，私钥值获取

![img](file:///C:\Users\burgl\AppData\Local\Temp\ksohtml281412\wps1.jpg) 

# **3.** ***请求参数加密说明***

Accesskey的值为公钥

***aValue的获取***

![img](file:///C:\Users\burgl\AppData\Local\Temp\ksohtml281412\wps2.jpg) 

***String akey=申请是获得到私钥;***

***例：***

***String sign1 =EncryptUtil.hmacSign(aValue, aKey)***

校验值的参数为 ***sign1  这个1不是多写的。***

 

错误代码

所有API方法调用在请求失败或遇到未知错误时会返回JSON错误对象。

| ***代码*** | ***描述***                 |
| ---------- | -------------------------- |
| 8888       | 成功                       |
| 0000       | 失败编码                   |
| 1000       | 一般错误提示               |
| 1001       | 内部错误                   |
| 1002       | 用户不存在                 |
| 1003       | 人民币账户不存在           |
| 1004       | 币账户不存在               |
| 1005       | 无效的参数                 |
| 5000       | 无效的IP或与绑定的IP不一致 |
| 5001       | 方法调错                   |
| 5002       | 访问公钥已失效             |
| 5003       | 验签失败                   |
| 5004       | API接口被锁定或未启用      |
| 6000       | 请求过于频繁               |
| 6001       | 人民币账户余额不足         |
| 2000       | 币账户余额不足             |
| 2001       | 委托单没有找到             |
| 2002       | 币种账号不存在             |
| 2003       | 无效的数量                 |
| 2004       | 人民币账户不存在           |
| 2005       | 提币地址不存在             |
| 2006       | 提现地址不存在             |
|            |                            |

访问限制

1单个用户限制每秒钟1次访问，一秒钟200次以上的请求，将会视作无效。

 

 