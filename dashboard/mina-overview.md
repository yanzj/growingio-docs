# 小程序预置看板

当成功添加了小程序追踪代码以后，在 GrowingIO 的首页里面会自动出现一个小程序概况看板，能直接得到日常分析报告，持续监测基础数据来获得洞察。

目前，小程序概况看板提供默认6个场景的数据：

1. [增长指标](mina-overview.md#zeng-chang-zhi-biao)
2. [获客场景](mina-overview.md#huo-ke-chang-jing)
3. [分享场景](mina-overview.md#fen-xiang-chang-jing)
4. [页面分析](mina-overview.md#ye-mian-fen-xi)
5. [用户画像](mina-overview.md#yong-hu-hua-xiang)
6. [错误分析](mina-overview.md#cuo-wu-fen-xi)

对于进阶分析需求，比如转化分析、自定义事件、更多维度拆分等，可以使用 GrowingIO 的高级分析功能，自行制作单图和看板来分析，并且可以添加到首页做日常监测。

整体描述你的小程序的访问、分享和留存指标。总共有 8 张单图，主要分成三块信息：

1. 获客：预置图中展示**过去7天**小程序的打开次数、去重访问用户数、去重新访问用户数
2. 分享：预置图中展示**过去7天**小程序的调用微信小程序卡片分享事件次数、分享的访问用户数、以及由分享链接首次进入小程序的新访问用户数。
3. 留存：预置图中展示过去30天全部用户和新用户的主要留存率指标趋势。

**右上角“自定义”可以支持选择自定义的时间。当选择“今日”时，趋势图会自动切换为今日小时颗粒度的数据。**

## 增长指标

### 获客 <a id="huo-ke"></a>

预置图中展示**过去7天**小程序的打开次数、去重访问用户数、去重新访问用户数。趋势线展示过去7天每一天的各指标的数据情况。同时会默认计算上周同期对比数据。切换概览右上角时间控件，可以自动切换统计时间。

\*上周期：即选择统计时间的上一个相同时间周期。例如如果统计周期选择过去7天，上周期就是过去第14天到过去第8天；统计周期默认选择昨天，则上周期为前天。

#### 打开次数 <a id="da-kai-ci-shu"></a>

用户从打开小程序到主动关闭小程序或超时退出记为一次访问，即被统计为打开一次。

\*注：在单图、分群等功能中，预定义指标“访问量”即对应小程序的打开次数

#### 访问用户数 <a id="fang-wen-yong-hu-shu"></a>

在不设置openid的情况下，GrowingIO默认使用cookie作为识别访问用户的标识；访问用户数即为去重的独立cookie数量。

#### 新访问用户数 <a id="xin-fang-wen-yong-hu-shu"></a>

新访问用户数是指在同一个项目ID中接入GrowingIO 小程序SDK后，第一次使用你的小程序的访问用户

### **分享** <a id="fen-xiang"></a>

预置图中展示**过去7天**小程序中调用微信分享事件次数、分享的访问用户数、以及由好友转发分享进入小程序的新访问用户数。趋势线展示过去7天每一天的各指标的数据情况。同时会默认计算上周同期对比数据。

\*上周期：即选择统计时间的上一个相同时间周期。例如如果统计周期选择过去7天，上周期就是过去第14天到过去第8天；统计周期默认选择昨天，则上周期为前天。

#### 分享次数 <a id="fen-xiang-ci-shu"></a>

GrowingIO 小程序 SDK 会默认监测用户在页面点击转发按钮，调用微信转发接口转发小程序卡片给好友的分享事件_。_

\*注：_注意这个事件仅代表用户触发了分享事件，但是不代表真正的转发成功。例如：用户点击了分享，但是没有选择分享对象。_

#### 分享人数 <a id="fen-xiang-ren-shu"></a>

触达分享事件的去重访问用户数。

#### 分享新增人数 <a id="fen-xiang-xin-zeng-ren-shu"></a>

通过好友转发分享带来的新访问用户数。

### 留存 <a id="liu-cun"></a>

访问用户周留存：预置图中展示过去30天内，每周的活跃用户在次周、2周后、3周后、4周后的留存率趋势变化。观察小程序周活跃用户的留存变化，方便以周为单位，洞察整体产品的留存核心指标是否有提升。

新访问用户日留存：预置图中展示30天内，每天的日活跃用户在次日、7日、14日后的留存趋势变化。新用户需要关注激活（产生留存意愿）的情况，所以需要关注短期内的留存趋势。

## 获客场景

微信中开放了非常多进入小程序的入口，每次打开小程序时，GrowingIO会获取到进入小程序时的入口信息。

### 入口分布与趋势 <a id="ru-kou-fen-bu-yu-qu-shi"></a>

预置图中展示**过去7天**小程序打开次数、获取访问用户数、获取新访问用户Top10的场景及每日趋势。右上角“自定义”可以支持选择自定义的时间。当选择“今日”时，趋势图会自动切换为今日小时颗粒度的数据。

通过打开次数、访问用户数、新访问用户数的入口分布和趋势，可以较为直观的得到用户进入小程序场景的洞察。

### 推广获客

推广获客按照GrowingIO预置的广告来源维度统计，预置图中展示**过去7天**中访问用户和新访问用户Top10的广告来源。切换概览右上角时间控件，可以自动切换统计时间。

小程序目前支持公众号图文链接、二维码、广告等投放方式；GrowingIO可以通过识别在投放的落地链接中加入UTM参数的方式，来自动跟踪推广数据。具体可以参考渠道跟踪内容。[渠道跟踪/data-analytics/channel-tracking](/miniprogram/data-analytics/channel-tracking)

**注**：目前微信支持的小程序入口值如下：

| 1001 | 发现栏小程序主入口 |
| :--- | :--- |
| 1005 | 顶部搜索框的搜索结果页 |
| 1006 | 发现栏小程序主入口搜索框的搜索结果页 |
| 1007 | 单人聊天会话中的小程序消息卡片 |
| 1008 | 群聊会话中的小程序消息卡片 |
| 1011 | 扫描二维码 |
| 1012 | 长按图片识别二维码 |
| 1013 | 手机相册选取二维码 |
| 1014 | 小程序模版消息 |
| 1017 | 前往体验版的入口页 |
| 1019 | 微信钱包 |
| 1020 | 公众号 profile 页相关小程序列表 |
| 1022 | 聊天顶部置顶小程序入口 |
| 1023 | 安卓系统桌面图标 |
| 1024 | 小程序 profile 页 |
| 1025 | 扫描一维码 |
| 1026 | 附近小程序列表 |
| 1027 | 顶部搜索框搜索结果页“使用过的小程序”列表 |
| 1028 | 我的卡包 |
| 1029 | 卡券详情页 |
| 1030 | 自动化测试下打开小程序 |
| 1031 | 长按图片识别一维码 |
| 1032 | 手机相册选取一维码 |
| 1034 | 微信支付完成页 |
| 1035 | 公众号自定义菜单 |
| 1036 | App 分享消息卡片 |
| 1037 | 小程序打开小程序 |
| 1038 | 从另一个小程序返回 |
| 1039 | 摇电视 |
| 1042 | 添加好友搜索框的搜索结果页 |
| 1043 | 公众号模板消息 |
| 1044 | 带 shareTicket 的小程序消息卡片 |
| 1045 | 朋友圈广告 |
| 1047 | 扫描小程序码 |
| 1048 | 长按图片识别小程序码 |
| 1049 | 手机相册选取小程序码 |
| 1052 | 卡券的适用门店列表 |
| 1053 | 搜一搜的结果页 |
| 1054 | 顶部搜索框小程序快捷入口 |
| 1056 | 音乐播放器菜单 |
| 1057 | 钱包中的银行卡详情页 |
| 1058 | 公众号文章 |
| 1059 | 体验版小程序绑定邀请页 |
| 1064 | 微信连Wi-Fi状态栏 |
| 1067 | 公众号文章广告 |
| 1068 | 附近小程序列表广告 |
| 1069 | 移动应用 |
| 1071 | 钱包中的银行卡列表页 |
| 1072 | 二维码收款页面 |
| 1073 | 客服消息列表下发的小程序消息卡片 |
| 1074 | 公众号会话下发的小程序消息卡片 |
| 1077 | 摇周边 |
| 1078 | 连Wi-Fi成功页 |
| 1079 | 微信游戏中心 |
| 1081 | 客服消息下发的文字链 |
| 1082 | 公众号会话下发的文字链 |
| 1089 | 微信聊天主界面下拉 |
| 1090 | 长按小程序右上角菜单唤出最近使用历史 |
| 1091 | 公众号文章商品卡片 |
| 1092 | 城市服务入口 |
| 1095 | 小程序广告组件 |
| 1096 | 聊天记录 |
| 1097 | 微信支付签约页 |
| 1102 | 服务号 profile 页服务预览 |

\*Tip：由于Android系统限制，目前微信还无法获取到按 Home 键退出到桌面，然后从桌面再次进小程序的场景值，对于这种情况，会保留上一次的场景值。

微信文档链接：[https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/scene.html](https://developers.weixin.qq.com/miniprogram/dev/framework/app-service/scene.html)​

## 分享场景

默认分享事件统计分享到好友对话框和微信群的触发事件。分别从页面、页面标题和详细页面路径三个角度，展示Top10的分享触发场景。预置图中展示**过去7天**的数据**，**切换概览右上角时间控件，可以自动切换统计时间。

### 页面 <a id="ye-mian"></a>

抓取分享发生的页面（没有参数），一般用来确定用户触发分享的基本功能场景或者触发机制，例如是红包，还是具体的内容，或者具体的商品。

`例如：红包页（pages/regbag)，商品详情页(pages/productdetails)。`

### 页面标题 <a id="ye-mian-biao-ti"></a>

页面标题是GrowingIO自动抓取的内容；如果页面设置了较为详细的名称，是可以非常清晰的知道具体页面内容的转发情况。常用在具体内容类或者详细商品类的场景上。例如：![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LD4kKkCTHNxUGbu1QWO%2F-LGy-_l_bITP1Zjy66Bd%2F-LGy0Iv97k-GjNJIBnAg%2Fimage.png?alt=media&token=1765c63d-1729-4d91-88e7-dced708d9bb8)

### 页面路径 <a id="ye-mian-lu-jing"></a>

这个维度是最详细的页面路径（有参数），帮助定位非常具体的页面值。

## 页面分析

### 进入页 <a id="jin-ru-ye"></a>

用户进入小程序访问的第一个页面，例如用户从页面A进入小程序，跳转到页面B，A为进入页，而B不是（目前不支持带页面参数的情况）。

### 浏览页 <a id="lan-ye"></a>

用户进入小程序浏览过的所有页面，例如用户从页面A进入小程序，跳转到页面B，A，B均为浏览页。

### 进入页面质量分析 <a id="jin-ru-ye-mian-zhi-liang-fen-xi"></a>

预置图中展示**过去7天**的数据**，**切换概览右上角时间控件，可以自动切换统计时间。

通过页面的进入量、跳出次数、每次进入页面浏览量、访问用户人均进入次数、平均进入时长（分钟）、和总进入时长，来衡量用户进入小程序的第一个页面。主要判断页面较为有效的满足了用户需求，或者吸引了用户，从而更好的引导用户在哪些页面和场景下进行分享。

**进入量**：即打开次数，按照进入页面拆分，即统计了打开小程序次数最多的第一个页面（落地页）。

**跳出次数**：用户打开一次小程序，仅有一个页面的浏览，就关闭或退出了小程序。这样会记一次跳出。跳出次数越高，说明用户对落地到达小程序看到的内容兴趣越低。

**每次进入页面浏览量**：按照进入页拆分后，指从A页面打开小程序，到关闭小程序，平均每次访问会浏览多少个页面。

**访问用户人均进入次数**：按照进入页拆分，指通过A页面打开小程序的次数/通过A页面进入小程序的访问用户量。

**总进入时长**：按照进入页拆分，指通过A页面打开小程序的访问时长的总和。

**平均进入时长**：按照进入页拆分，指通过A页面打开小程序的访问时长的总和/通过A页面打开小程序的次数。

### 浏览页关键质量指标分析 <a id="lan-ye-guan-jian-zhi-liang-zhi-biao-fen-xi"></a>

预置图中展示**过去7天**的数据**，**切换概览右上角时间控件，可以自动切换统计时间。

页面浏览，即指在小程序打开期间，被浏览过的页面。其中，页面浏览可以按照页面浏览量、访问用户量、退出率、页面停留时长、转发次数几个方面来进行评价。

**退出率**：退出率按照不同的页面去查看的时候，即描述的是A页面作为_退出页_的访问量/浏览过A页面的访问量。

\*退出页：用户在一次访问中访问的最后一个页面，是这次访问的退出页，也就是用户的这次访问是在这里结束的

**总页面停留时长（分钟）：**代表着在当前页面上用户停留的总时长。

**平均页面停留时长（秒）**：代表着在每次打开小程序，当前页面上用户停留的平均时长。

**转发分享按钮\_点击次数**：表示在这个页面上触发了多少次好友/群聊对话框的分享事件。

## 用户画像

整体描述小程序访问用户的画像特征数据，主要分成两块信息：

1. 使用时长和使用频率
2. 用户特征数据，包括性别、用户城市、用户使用设备品牌

### **使用时长和使用频率** <a id="shi-yong-shi-chang-he-shi-yong-pin-lv"></a>

#### 用户使用时长分布 <a id="yong-hu-shi-yong-shi-chang-fen-bu"></a>

单位为秒，预置图中展示**过去7天**活跃用户访问小程序的使用时长的人数分布。目前分布有 \(0-5\]s、\(5-10\]s、\(10-20\]s、\(20-30\]s、\(30-50\]s、\(50-100\]s、\(100-300\]s、&gt;300s。每个时间区段，不包含区段的最小值，包含区段的最大值。切换概览右上角时间控件，可以自动切换统计时间。

#### 用户使用频次分布 <a id="yong-hu-shi-yong-pin-ci-fen-bu"></a>

单位为次，预置图中展示**过去7天**活跃用户访问小程序的使用次数的人数分布。目前分布有 1次、\(1-3\]次、\(3-6\]次、\(6-10\]次、&gt;10次。每个频次区段，不包含区段的最小值，包含区段的最大值。切换概览右上角时间控件，可以自动切换统计时间。

### **用户性别** <a id="yong-hu-xing-bie"></a>

#### 访问用户性别分布、打开次数性别分布 <a id="fang-wen-yong-hu-xing-bie-fen-bu-da-kai-ci-shu-xing-bie-fen-bu"></a>

预置图中显示过去7天微信属性中不同性别的访问用户量和打开次数。切换概览右上角时间控件，可以自动切换统计时间。

如果在 SDK 集成的时候设置了微信用户变量，那么可以在图中得到过去 7 天的使用用户的性别分布；微信用户变量中，常见的值为：男性、女性、未知（表示用户没有设置性别值）。

如果出现大量的N/A，表示GrowingIO没有获取到用户设置的微信性别属性。常见的情况有这么几种：1没有设置用户；请[参考SDK微信用户属性设置](https://growingio.gitbook.io/miniprogram/~/edit/drafts/-LH1kFvlqMstbSQRa8Ql/tag-management/sdk-logic/sdk-gao-ji-she-zhi-11)，来设置微信用户的变量；2小程序不强制读取微信用户设置的信息，用户未授权小程序读自己的内容设置。

### 用户城市 <a id="yong-hu-cheng-shi"></a>

预置图中显示小程序在**过去 7 天**的 Top10 用户城市分布图。切换概览右上角时间控件，可以自动切换统计时间。用户城市从两个角度统计了城市分布：

**微信所属城市**：即用户设置的微信用户信息中标记的地理位置所属的城市。不按照实际地点变化进行变化。

如果出现大量的N/A，表示GrowingIO没有获取到用户设置的微信性别属性。常见的情况有这么几种：1没有设置用户；请[参考SDK采集数据逻辑](/miniprogram/~/drafts/-LGyI067mAICT2LPDqZQ/primary/tag-management/sdk-logic#she-zhi-wei-xin-yong-hu-xin-xi)，来设置微信用户的变量；2小程序不强制读取微信用户设置的信息，用户未授权小程序读自己的内容设置。

**实际访问城市：**GrowingIO会获取用户访问时的实际IP，根据实际IP，对照商业IP库，来识别用户所在地区。如果标记为未知，即为商业IP库未收录，多常见于移动网络IP、较为偏远的地区、或网络代理。

### 设备品牌 <a id="she-bei-pin-pai"></a>

预置图中展示小程序在**过去 7 天**的 Top10 用户访问设备分布图。切换概览右上角时间控件，可以自动切换统计时间。

如果想得到更为详细的设备型号等信息，可以在新建单图功能，维度选择预置的设备型号，指标选择想查看的指标（例如：访问用户量），来查看具体的设备型号。设备品牌中存在“不适用”的情况，主要由于访问信息中没有设备品牌信息。

## 错误分析

### 错误信息 <a id="cuo-wu-xin-xi"></a>

统计小程序中报错的数量和被影响的用户数。默认展示过去7天的Top10报错信息，帮助及时改善用户体验。

GrowingIO采集小程序中错误发生事件，报错所在的页面、错误信息、错误对应的函数，以及错误码。

