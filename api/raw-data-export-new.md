# 原始数据导出 2.0 API

* [1.原始数据导出 2.0 API 功能概要](raw-data-export-new.md#summary)
* [2.原始数据导出 2.0 API 接口定义](raw-data-export-new.md#definition)
  * [GET 按类型导出原始数据](raw-data-export-new.md#an-lei-xing-dao-chu-yuan-shi-shu-ju)
  * [GET 导出全部类型原始数据](raw-data-export-new.md#dao-chu-quan-bu-lei-xing-yuan-shi-shu-ju)
* [3.原始数据导出版本和GrowingIO数据主版本（SDK 版本）关系](raw-data-export-new.md#sdk-explaination)
* [4.原始数据导出 2.0 和原始数据导出 1.0 主要区别](raw-data-export-new.md#changelog)
* [5.原始数据导出 2.0 导出数据字段说明](raw-data-export-new.md#metadata)
  * [visit](raw-data-export-new.md#metadata_visit)
  * [page](raw-data-export-new.md#metadata_page)
  * [action](raw-data-export-new.md#metadata_action)
  * [action\_tag](raw-data-export-new.md#metadata_action_tag) /  [rules](raw-data-export-new.md#metadata_rule)
  * [custom\_event](raw-data-export-new.md#metadata_custom_event)
  * [pvar](raw-data-export-new.md#metadata_pvar)
  * [evar](raw-data-export-new.md#metadata_evar)
  * [ads\_track\_click](raw-data-export-new.md#metadata_ads_click)
  * [ads\_track\_activation](raw-data-export-new.md#metadata_ads_activation)
* [6.关于接口版本1.0升级到2.0注意事项](raw-data-export-new.md#upgrade)

原始数据导出为付费功能，且只能导出从开通之日起的原始数据，原始数据仅保留15天，请定期下载。数据导出一般延迟为 30 分钟，比如早上 8 点到 9 点之间的数据，一般 9:30 会准备好。每天凌晨因为需要运行天级别的统计任务，所以导出任务会延迟 1-2 小时，在导出数据时请判断  `status` 字段 。

导出时数据以每 64M 为单位分包发送，导出数据默认采用 gzip 压缩。原始数据中所有时间字段均为 [UTC](http://baike.baidu.com/link?url=T9ER87o8wd_ABq-oRrn839-Q2hxrV5WvIeQX2bJCOAWgne8C8BCw8yRWrISceZJEoR83GuIhdu0vSZFwzl4ngFrD7vUITsrlcY6U3Fj6lWCx7x0xWRTNDFOHkhJmnUW05hrb5df7vvz12EayMr_4b5QJZ1UcTs17ffae3wI18LNeF8j_4WpMZ_srcJHSXhpk) 时间，并非中国时间；此处导出的压缩包名也是由 UTC 时间命名。

在进行原始数据导出之前，请务必参考 [“GrowingIO接口认证”文档](https://docs.growingio.com/api/authentication.html)，完成接口认证获取 token 。

### 1.原始数据导出 2.0 API 功能概要 {#summary}

1. “2.0版”提供了小时级别的原始数据导出。

   例如，下午1点到2点的原始数据，在一般情况下可以在3点准备好。

2. “2.0版”在包含所有“1.0版”具有的数据表和字段的基础上添加了数据主版本2.0（SDK 2.x）版本具有的自定义事件和变量的数据表和字段，并对包括广告监测数据导出在内的所有数据导出表的字段做了统一处理。
3. “2.0版”兼容并包含了"1.0版"的所有数据字段。

### 2.原始数据导出 2.0 API 接口定 {#definition}

### 3.原始数据导出版本和GrowingIO数据主版本（SDK 版本）关系 {#sdk-explaination}

![](https://docs.growingio.com/.gitbook/assets/datafeed.png)

在“原始数据导出 2.0 API” 上线之前，使用数据主版本2的客户也在使用“原始数据导出 1.0 API”。在“原始数据导出 1.0 API”版本中并没有包括如：页面级变量、转化变量这样的原始数据。在“原始数据导出 2.0 API”中提供了这部分原始数据的导出功能。

### 4.原始数据导出 2.0 和原始数据导出 1.0 主要区别 {#changelog}

#### 接口请求 URL {#接口请求-url}

原始数据导出 1.0 接口格式：

`https://www.growingio.com/insights/:ai/:date.json`

原始数据导出 2.0 接口格式：

`https://www.growingio.com/v2/insights/{export_type}/{data_type}/{ai}/{export_date}.json`

#### 接口响应数据格式 {#接口响应数据格式}

原始数据导出 1.0 接口返回数据格式：

```text
{
  "status":"FINISHED",
  "downlinks":[
    "link1",
    "link2"
  ]
}
```

原始数据导出 2.0 接口返回数据格式：

```text
{
  "status”:"FINISHED",
  "downloadLinks":[
    "link1",
    "link2"
  ],
  "exportType":"",
  "dataType":"",
  "exportDate":"",
  "exportVersion":"",
  "requestTime":"",
  "errorMsg":""
}
```

#### 数据文件的获取方式和组织 {#数据文件的获取方式和组织}

原始数据导出 1.0

1. 按天和小时的维度区分获取数据，一次获取所有类型的数据
2. 天数据一次返回所有7种类型当天的7个数据文件
3. 小时数据一次返回所有7种类型当天特定小时的7个数据文件

原始数据导出 2.0

1. 按导出类型（天或小时）和数据类型（v2共9种）区分获取数据，一次获取一种类型特定时间的数据
2. 天数据返回特定日期所有小时的数据文件
3. 小时数据根据确定的数据类型和时间获取确定类型确定小时的1个数据文件

#### 原始数据导出提供的数据类型 {#原始数据导出提供的数据类型}

原始数据导出 1.0 提供的数据类型：

visit、page、action、action\_tag、custom\_attr、ads\_track\_click、ads\_track\_activation一共7种类型的数据

原始数据导出 2.0 提供的数据类型：

visit、page、action、action\_tag、custom\_event（原custom\_attr）、ads\_track\_click、ads\_track\_activation、pvar（新增）、evar（新增）一共9种类型的数据

#### 数据格式变化 {#数据格式变化}

visit：新增字段，部分字段名称变化

page：新增字段，部分字段名称变化

action：部分字段名称变化

action\_tag：字段名称变化

ads\_track\_activation：部分字段名称变化

custom\_event：原custom\_attr，新增字段，部分字段名称变化

pvar：新增类型

evar：新增类型

### 5.原始数据导出 2.0 导出数据字段说明 {#metadata}

#### page请求导出字段 {#metadata_page}

| 原始数据导出 2.0 字段名称 | 原始数据导出 1.0 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| visitUserId | userId | string\(36\) | 访问用户ID（visit user id） | 2f94c582-bd29-427d-8e4d-ae2cd0287ae1 | 匿名的访问用户ID，由GrowingIO自动生成。 |
| sessionId | sessionId | string\(36\) | 访问ID（session id） | 45bcb40d-2963-4ef9-85d6-6583cd69d7b4 | 访问ID |
| platform | platform | string\(10\) | 平台（platform） | web | 访问所属平台，可能值为 iOS / Android / Web 等 |
| domain | domain | string\(100\) | 域名（domain） | growingio.com | 访问的域名，当为 iOS / Android 时，为 app 包名 |
| page | path | string\(512\) | 页面（page） | pages/index | 用户访问的当前页面 |
| queryParameters | query | string\(512\) | 查询参数（query arameters） | cid=1234567 | 当前网站页面URL中的查询参数 |
| referrer | refer | string\(1024\) | 页面来源（referrer） | [http://www.growingio.com?cid=1234567](http://www.growingio.com/?cid=1234567) | 当前页面浏览的引荐来源 |
| referrerPage | （新加） | string\(512\) | 页面来源页面（referrer page） | myViewController | 移动应用的来源页面 |
| title | title | string\(1024\) | 页面Title（title） | GrowingIO | 页面的Title |
| time | eventTime | bigint | 时间戳（time） | 1506069592985 | 请求在用户端发生的时间戳 |
| sendTime | sendTime | bigint | 发送时间（send time） | 1507897826891 | 请求在SDK发送的时间戳 |
| deviceOrientation | （新加） | string\(10\) | 设备方向（device orientation） | PORTRAIT |  |
| loginUserId | cs1（新旧不同） | string\(200\) | 登录用户ID（login user id） | user12345 | 登录用户ID，推荐使用那些不能定位到个人的ID信息，通常为企业内部使用的CRM ID |
| pageGroup | pageGroup\(新旧不同\) | string\(200\) | 页面组（page group） | myPG | SDK 1.x版本的页面组维度（Deprecated） |
| appVariable | （新加） | map&lt;string, string&gt; | 应用级变量（app variable） | {"version": "1.1"} | SDK 1.x版本的应用级变量（Deprecated） |
| customerAttributes2 | cs2（新旧不同） | string\(200\) | 用户属性2（customer attributes2） |  | SDK 1.x版本的CS2字段（Deprecated） |
| customerAttributes3 | cs3（新旧不同） | string\(200\) | 用户属性3（customer attributes3） |  | SDK 1.x版本的CS3字段（Deprecated） |
| customerAttributes4 | cs4（新旧不同） | string\(200\) | 用户属性4（customer attributes4） |  | SDK 1.x版本的CS4字段（Deprecated） |
| customerAttributes5 | cs5（新旧不同） | string\(200\) | 用户属性5（customer attributes5） |  | SDK 1.x版本的CS5字段（Deprecated） |
| customerAttributes6 | cs6（新旧不同） | string\(200\) | 用户属性6（customer attributes6） |  | SDK 1.x版本的CS6字段（Deprecated） |
| customerAttributes7 | cs7（新旧不同） | string\(200\) | 用户属性7（customer attributes7） |  | SDK 1.x版本的CS7字段（Deprecated） |
| customerAttributes8 | cs8（新旧不同） | string\(200\) | 用户属性8（customer attributes8） |  | SDK 1.x版本的CS8字段（Deprecated） |
| customerAttributes9 | cs9（新旧不同） | string\(200\) | 用户属性9（customer attributes9） |  | SDK 1.x版本的CS9字段（Deprecated） |
| customerAttributes10 | cs10（新旧不同） | string\(200\) | 用户属性10（customer attributes10） |  | SDK 1.x版本的CS10字段（Deprecated） |
| pageAttributes1 | ps1（新旧不同） | string\(200\) | 页面属性1（pageattributes1） |  | SDK 1.x版本的PS1字段（Deprecated） |
| pageAttributes2 | ps2（新旧不同） | string\(200\) | 页面属性2（pageattributes2） |  | SDK 1.x版本的PS2字段（Deprecated） |
| pageAttributes3 | ps3（新旧不同） | string\(200\) | 页面属性3（pageattributes3） |  | SDK 1.x版本的PS3字段（Deprecated） |
| pageAttributes4 | ps4（新旧不同） | string\(200\) | 页面属性4（pageattributes 4） |  | SDK 1.x版本的PS4字段（Deprecated） |
| pageAttributes5 | ps5（新旧不同） | string\(200\) | 页面属性5（pageattributes5） |  | SDK 1.x版本的PS5字段（Deprecated） |
| pageAttributes6 | ps6（新旧不同） | string\(200\) | 页面属性6（pageattributes6） |  | SDK 1.x版本的PS6字段（Deprecated） |
| pageAttributes7 | ps7（新旧不同） | string\(200\) | 页面属性7（pageattributes7） |  | SDK 1.x版本的PS7字段（Deprecated） |
| pageAttributes8 | ps8（新旧不同） | string\(200\) | 页面属性8（pageattributes8） |  | SDK 1.x版本的PS8字段（Deprecated） |
| pageAttributes9 | ps9（新旧不同） | string\(200\) | 页面属性9（pageattributes9） |  | SDK 1.x版本的PS9字段（Deprecated） |
| pageAttributes10 | ps10（新旧不同） | string\(200\) | 页面属性10（pageattributes10） |  | SDK 1.x版本的PS10字段（Deprecated） |
| pageRequestId | id | string\(23\) | 页面请求ID（page request id） | 1521010820647fa5a9314e6 | GrowingIO系统内部用于标识一个唯一的页面请求的ID |
| vstRequestId | visit\_id | string\(16\) | 访问请求ID（visit request id） | c7db72a5841506bd | GrowingIO系统内部用于标识一个访问请求的ID |

#### vst请求导出字段 {#metadata_visit}

| 原始数据导出 2.0 字段名称 | 原始数据导出 1.0 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| visitUserId | userId | string\(36\) | 访问用户ID（visit user id） | fc55728b-41ab-42ff-8b1f-714e44c65fd6 | 匿名的访问用户ID，由GrowingIO自动生成。 |
| sessionId | sessionId | string\(36\) | 访问ID（session id） | 6b5099c7-6006-422d-92ac-4f3bf4ddd37c | 访问ID |
| accountVersion | （新加） | string\(20\) | SDK版本（account version） | 2.3.0 | SDK版本信息 |
| platform | platform | string\(20\) | 平台（platform） | Web | 访问所属平台，可能值为 iOS / Android / Web 等 |
| domain | domain | string\(100\) | 域名（domain） | growingio.com | 访问的域名，当为 iOS / Android 时，为 app 包名 |
| page | path（新旧不同） | string\(512\) | 页面（page） | pages/index | 用户访问的当前页面 |
| queryParameters | query（新旧不同） | string\(512\) | 查询参数（query arameters） | cid=1234567 | 当前网站页面URL中的查询参数 |
| referrer | refer（新旧不同） | string\(1024\) | 页面来源（referrer） | [http://www.growingio.com?cid=1234567](http://www.growingio.com/?cid=1234567) | 当前页面浏览的引荐来源 |
| language | language | string\(10\) | 语言（language） | zh-cn | 系统使用的语言 |
| screenHeight | （新加） | string\(10\) | 屏幕高度（screen height） | 1242 | 屏幕高度 |
| screenWidth | （新加） | string\(10\) | 屏幕宽度（screen width） | 2016 | 屏幕宽度 |
| time | eventTime\(新旧不同\) | bigint | 时间戳（time） | 1520899220665 | 请求在用户端发生的时间戳 |
| sendTime | sendTime | bigint | 发送时间（send time） | 1520899221211 | 请求在SDK发送的时间戳 |
| ip | ip | string\(15\) | IP地址（ip address） | 127.0.0.1 | IP地址（ip address） |
| userAgent | userAgent | string\(512\) | User Agent，例如浏览器信息或者移动设备信息 | Mozilla/5.0 \(Linux; Android 6.0; V9 Build/MRA58K; wv\) AppleWebKit/537.36 \(KHTML |  |
| operatingSystem | （新加） | string\(3\) | 操作系统（operating system） | iOS / Android |  |
| operatingSystemVersion | osVersion\(新旧不同\) | string\(50\) | 操作系统版本（operating system version） | iOS 11.0.1 /Android 6.0.1 |  |
| clientVersion | appVersion\(新旧不同\) | string\(20\) | 客户的产品版本，仅限移动端 | 1.0 |  |
| channel | channel | string\(40\) | app的下载渠道，仅限移动端 | App Store |  |
| deviceBrand | manufacturer\(新旧不同\) | string\(20\) | 设备品牌（device brand） | google |  |
| deviceModel | model\(新旧不同\) | string\(50\) | 设备型号（device model） | Nexus 5 |  |
| deviceType | （新加） | string\(50\) | 设备类型（device type） | 1 | 设备类型：1为手机，2为平板 |
| deviceOrientation | （新加） | string\(10\) | 设备方向（device orientation） | PORTRAIT | 请求产生时设备方向 |
| latitude | lat\(新旧不同\) | double | 地理位置维度（latitude） | 29.43982 | 精确到小数点后5位 |
| longitude | lng\(新旧不同\) | double | 地理位置经度（longitude） | 29.43982 | 精确到小数点后5位 |
| vstRequestId | visit\_id | string\(16\) | GrowingIO系统访问请求内部ID（internal visit id） | c7db72a5841506bd | GrowingIO系统内部用于标识一个访问请求的ID |
| idfa | （新加） | string\(16\) | idfa\(identifier for advertising\) | A075A0F9-32D2-4671-A78D-144B6B7D2920 | 苹果系统用于监测广告的ID |
| androidId | （新加） | string\(16\) | androidId | 6284760c2926bcd5 | 安卓系统的一个ID |
| IMEI | （新加） | string\(16\) | IMEI（International Mobile Equipment Identity） | 867459000000000 | 国际移动设备识别码 |

> **visit数据注意事项**

API1.0接口中的**`countryName、region、city`**三个字段，在API2.0接口中已经删除。原因是这三个字段实际由GrowingIO内部库通过**`解析IP、地理位置`**得到的结果，可能与客户自己解析出来的结果存在差异，这样会造成客户识别的困扰。

#### action请求导出字段 {#metadata_action}

| 原始数据导出 2.0 字段名称 | 原始数据导出 1.0 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| visitUserId | userId | string\(36\) | 访问用户ID（visit user id） | fc55728b-41ab-42ff-8b1f-714e44c65fd6 | 匿名的访问用户ID，由GrowingIO自动生成。 |
| sessionId | sessionId | string\(36\) | 访问ID（session id） | 6b5099c7-6006-422d-92ac-4f3bf4ddd37c | 访问ID |
| requestType | eventType | string\(10\) | 请求类型（request type） | clck | 根据请求的类型不同，可能值为：clck\(click\), chng\(change\)，sbmt\(submit\)以及imp\(impression\)，change |
| domain | domain | string\(100\) | 域名（domain） | www.growingio.com | 访问的域名，当为 iOS / Android 时，为 app 包名 |
| page | path | string\(512\) | 页面（page） | /login | 网站页面 |
| sendTime | sendTime | bigint | 发送时间（send time） | 1507897826891 | 请求在SDK发送的时间戳戳 |
| time | eventTime | bigint | 时间戳（time） | 1506069592985 | 请求在用户端发生的时间戳 |
| href | href | string\(1024\) | 标签内的跳转链接（如果没有则为null） | help.growingio.com | 标签内的跳转链接（如果没有则为null） |
| requestValue | eventValue | string\(1024\) | 请求值（request value） | “确定” | 该消息的值，例如标签的value |
| index | index | bigint | 标签序号（tag index） | 用于标记列表内的第几项，分析列表中最常被点击的内容或者首项推广效果等等 | 列表类型标签的序号 |
| info | info | string\(200\) |  | 用户自定义事件信息 | 对应growingAttributesInfo设置的字段信息 |
| pageRequestId | page\_id | string\(23\) | GrowingIO系统页面请求内部ID | 1521010820647fa5a9314e6 | 页面唯一的id，用于与page数据join |
| actionRequestId | action\_id | string\(30\) | GrowingIO系统Action请求内部ID | web的action\_id以wa开头，mobile以ma开头 | 标签事件的唯一id |

#### cstm请求导出字段 {#metadata_custom_event}

| 原始数据导出 2.0 字段名称 | 原始数据导出 1.0 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| visitUserId | \_userId（新旧不同） | string\(36\) | 访问用户ID（visituser id） | fc55728b-41ab-42ff-8b1f-714e44c65fd6 | 访问用户 ID 唯一标识 |
| sessionId | \_sessionId（新旧不同） | string\(36\) | 访问ID（session id） | 6b5099c7-6006-422d-92ac-4f3bf4ddd37c | 当前访问唯一标识 |
| time | \_eventTime（新旧不同） | bigint | 时间戳（time） | 1506069592985 | 请求在用户端发生的时间戳 |
| sendTime | （新加） | bigint | 发送时间（send time） | 1507897826891 | 请求在SDK发送的时间戳 |
| pageTime | （新加） | bigint | 页面时间（page time） | 1516349263375 | pvar对应的页面请求的产生时间 |
| domain | （新加） | string\(100\) | 域名（domain） | www.growingio.com | 访问的域名，当为 iOS / Android 时，为 app 包名 |
| page | path（新旧不同） | string\(512\) | 页面（page） | pages/index | 用户访问的当前页面 |
| queryParameters | （新加） | string\(512\) | 查询参数（query arameters） | [http://www](http://www/).[growingio.com?cid=1234567](http://growingio.com/?cid=1234567) | 当前网站页面URL中的查询参数 |
| eventName | （新加） | string\(50\) | 事件名称（event name） | revenue | 自定义事件的标识符 |
| eventNumber | （新加） | double | 事件数值（event number） | 99.99 | 自定义事件的值 |
| eventVariable | （新加） | map&lt;string, string&gt; | 事件级变量（event variable） | {"price": "50.0", "item": "101"} | 自定义事件级变量 |
| loginUserId | \_cs1（新旧不同） | string\(200\) | 登录用户ID（customer attributes 1） | user12345 | 登录用户ID，推荐使用那些不能定位到个人的ID信息，通常为企业内部使用的CRM ID |
| pageRequestId | （新加） | string\(23\) | GrowingIO系统页面请求内部ID | 15208995970115f7e2c153f | 该自定义事件所归属的 page 事件 id |

#### pvar请求导出字段 {#metadata_pvar}

| 原始数据导出 2.0 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| visitUserId | string\(36\) | 访问用户ID（visit user id） | 1ba42333-87f2-3cc4-bb42-ac4176526796 | 访问用户 ID 唯一标识 |
| sessionId | string\(36\) | 访问ID（session id） | c6575ef5-5c06-443e-bf6e-b12e1e37a3f8 | 当前访问唯一标识 |
| time | bigint | 时间戳（time） | 1520899220665 | 请求在用户端发生的时间戳 |
| sendTime | bigint | 发送时间（send time） | 1520899221211 | 请求在SDK发送的时间戳 |
| pageTime | bigint | 页面时间（page time） | 1520899221209 | pvar对应的页面请求的产生时间 |
| domain | string\(100\) | 域名（domain） | www.growingio.com | 访问的域名，当为 iOS / Android 时，为 app 包名 |
| page | string\(512\) | 页面（page） | /funnel | 用户访问的当前页面 |
| pageVariable | map&lt;string, string&gt; | 页面级变量（page variable） | {"category": "funnel"} | 页面级变量键值对 |
| pageRequestId | string\(23\) | GrowingIO系统页面请求内部ID | 15208995970115f7e2c153f | 该页面级变量所归属的 page 事件 id |

#### evar请求导出字段 {#metadata_evar}

| 原始数据导出 2.0 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| visitUserId | string\(36\) | 访问用户ID（visit user id） | c6dc7078-19a8-43c8-a728-d7f78f38bc7b | 访问用户 ID 唯一标识 |
| sessionId | string\(36\) | 访问ID（session id） | 372f87d0-c743-4b6b-a4c3-3833b90ce5e2 | 当前访问唯一标识 |
| time | bigint | 时间戳（time） | 1521331185777 | 请求在用户端发生的时间戳 |
| sendTime | bigint | 发送时间（send time） | 1521331204282 | 请求在SDK发送的时间戳 |
| domain | string\(100\) | 域名（domain） | www.growingio.com | 访问的域名，当为 iOS / Android 时，为 app 包名 |
| conversionVariable | map&lt;string, string&gt; | 转化变量（conversion variable） | {"keyword":"retention"} |  |

#### action\_tag导出字段 {#metadata_action_tag}

| 原始数据导出2.0字段名称 | 原始数据导出1.0字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| sendTime | sendtime | bigint | 数据发送时间（send time） | 1521331200412 | 请求在SDK发送的时间戳 |
| actionRequestId | action\_id | string\(30\) | GrowingIO系统Action内部ID | wa:0:24:1356477892:0 | 用于标识一个action请求的ID，`web的以wa开头`，`mobile的以ma开头` |
| ruleId | rule\_id | string\(8\) | GrowingIO系统Rule内部ID | 99ae0dec | 用于标识圈选标签的唯一ID，由字母和数字组成 |

#### rules（从[统计数据的规则逻辑API](https://docs.growingio.com/docs/api/reporting-api#rule-api)获取） {#metadata_rule}

| 字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| rule\_id | string\(8\) | GrowingIO系统Rule内部ID | 99ae0dec | 用于标识圈选标签的唯一ID，有字母和数字组成 |
| name | string\(200\) | Rule的名称 | xxx | 圈选标签的名称，该名称不可以作为区分Rule唯一的标识 |
| ruleType | string\(10\) | Rule的类型，如按钮的点击或曝光 | clck | 值包括page、imp、clck、chng、sbmt |

> 备注

1. 在基础部分数据导出（visit，page，action）之外，提供圈选数据与action级别数据的映射部分。
2.  **rules**表示客户在GrowingIO平台上圈选的标签，rule\_id是其唯一标识。
3.  通过**action**中的`action_id`与**action\_tag**中的`action_id`聚合，然后绑定**action\_tag**中的`rule_id`到**rules**中对应的`rule_id、name`到action的数据上。这样就可以通过规则名称进行数据分析，识别导出数据中圈选部分的数据情况。
4. 建议规则建立时保持名称的唯一性，GrowingIO平台不保证规则名称的唯一。
5. 相同的名称下可能有多个规则类型，`规则名称+规则类型`才能区分开，此处类型与基础数据**action**中的`请求事件类型`保持一致。

#### ads\_track\_activation 请求导出字段 {#metadata_ads_activation}

| 原始数据导出2.0字段名称 | 原始数据导出1.0字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| visitUserId | userId | string\(36\) | 访问用户ID（visit user id） | fc55728b-41ab-42ff-8b1f-714e44c65fd6 | 匿名的访问用户ID，由GrowingIO自动生成。 |
| idfa | idfa | string\(40\) | IDFA（id for advertiser） | F7A29C20-FD0D-4B68-BF4D-39EFC5C9A9C2 | iOS平台用于广告监测的ID：IDFA（id for advertiser） |
| imei | imei | string\(40\) | IMEI | 100500636E9AA9 | Android平台用于广告监测的ID |
| uuid | uuid | string\(40\) | UUID | 00000000-37fc-f5ob-1e8d-484b190312e1 | 用于广告监测的ID的UUID格式 |
| androidId | androidid | string\(40\) | Android ID | 2cab90e2a3b489ed | SSAID，又称为Android ID |
| ip | ip | string\(15\) | IP地址（ip address） | 127.0.0.1 |  |
| userAgent | useragent | string\(512\) | User Agent，例如浏览器信息或者移动设备信息 | Mozilla/5.0 \(iPhone; CPU iPhone OS 11\_2\_6 like Mac OS X\) AppleWebKit/604.5.6 \(KHTML, like Gecko\) Mobile/15D100 |  |
| platform | platform | string\(20\) | 平台（platform） | iOS |  |
| operatingSystemVersion | osversion | string\(50\) | 操作系统版本（operating system version） | iOS 11.2.6 |  |
| sendTime | sendtime | bigint | 发送时间（send time） | 1521315962327 | 请求在SDK发送的时间戳 |
| linkId | link\_id | string\(20\) | 链接ID（link id） | Yo1KJXRl | 监测链接ID |
| campaignId | campaign\_id | string\(20\) | 活动ID（campaign id） | GPndl79Y | 活动ID |
| channelId | channel\_id | string\(20\) | 渠道ID（channel id） | inmobi | 渠道ID |
| linkName | link\_name | string\(60\) | 链接名称 | 测试链接 | 2018/5/8 开始生效 |
| campaignName | campaign\_name | string\(60\) | 活动名称 | 双十一推广 | 2018/5/8 开始生效 |
| channelName | channel\_name | string\(60\) | 渠道名称 | 今日头条 | 2018/5/8 开始生效 |

#### ads\_track\_click 请求导出字段 {#metadata_ads_click}

| 原始数据导出2.0字段名称 | 原始数据导出1.0字段名称 | 字段格式 | 字段说明 | 示例值 | 备注 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| idfa | idfa | string\(40\) | IDFA（id for advertiser） | F9AFF106-3C41-4B78-B20B-D3BB166DA620 | iOS平台用于广告监测的ID：IDFA（id for advertiser） |
| imei | imei | string\(40\) | IMEI | 100500636E9AA9 | Android平台用于广告监测的ID |
| uuid | uuid | string\(40\) | UUID | 00000000-37fc-f5ob-1e8d-484b190312e1 | 用于广告监测的ID的UUID格式 |
| androidId | androidId | string\(40\) | Android ID | 2cab90e2a3b489ed | SSAID，又称为Android ID |
| ip | ip | string\(15\) | IP地址（ip address） | 127.0.0.1 | IP地址（ip address） |
| userAgent | useragent | string\(512\) | User Agent，例如浏览器信息或者移动设备信息 | Mozilla/5.0 \(Linux; Android 4.0.4; A31 Build/A31\) AppleWebKit/537.36 \(KHTML, like Gecko\) Version/4.0 Chrome/30.0.0.0 Mobile Safari/537.36 |  |
| platform | platform | string\(20\) | 平台（platform） | iOS | 访问所属平台，可能值为 iOS / Android / Web 等 |
| operatingSystemVersion | osversion | string\(50\) | 操作系统版本（operating system version） | iOS 11.2.6 |  |
| eventTime | eventtime | bigint | 点击请求时间（click request time） | 1521315962320 | 请求在SDK发送的时间戳 |
| linkId | link\_id | string | 链接ID（link id） | Yo1KJXRl | 监测链接ID |
| campaignId | campaign\_id | string\(20\) | 活动ID（campaign id） | GPndl79Y | 活动ID |
| channelId | channel\_id | string\(20\) | 渠道ID（channel id） | inmobi | 渠道ID |
| linkName | link\_name | string\(60\) | 链接名称 | 测试链接 | 2018/5/8 开始生效 |
| campaignName | campaign\_name | string\(60\) | 活动名称 | 双十一推广 | 2018/5/8 开始生效 |
| channelName | channel\_name | string\(60\) | 渠道名称 | 今日头条 | 2018/5/8 开始生效 |

### 6.关于接口版本1.0升级到2.0注意事项 {#upgrade}

如果您目前使用的API版本是1.0，想要升级为2.0，请联系客户成功经理。如果您已经从1.0升级到了2.0，请注意如下事项：

* 从API2.0接口开通那一刻起，API1.0接口依旧可以继续使用，但是**`一个月`**之后就会失效，请您在过渡期内尽快升级您的使用代码。
* API2.0接口从开通的那一刻起就开始生效，比如您于`2018-08-01 10:30:00`升级到了API2.0接口，那么API2.0接口就可以下载`2018-08-01 11:00:00`之后的数据了，但是之前的数据还需要通过API1.0去获取。



