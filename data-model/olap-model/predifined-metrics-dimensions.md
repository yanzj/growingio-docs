# 预定义的指标和维度

## 预定义指标

### 第一部分：用户级指标

> **用户级指标：项目级别的用户总量统计**

#### 访问用户量（web/app/小程序） <a id="17"></a>

访问用户的数量。

#### 新访问用户量（web/app/小程序） <a id="18&#x65B0;&#x8BBF;&#x95EE;&#x7528;&#x6237;&#x91CF;&#xFF08;webapp&#xFF09;"></a>

（接入 GrowingIO 后）365 天内第一次访问网站/小程序；打开App的访问用户数量。

#### 登录用户量（web/app/小程序） <a id="19"></a>

登录用户的数量，需要上传登录用户 ID 。

#### 新登录用户量（web/app/小程序） <a id="20"></a>

（接入 GrowingIO 后）第一次登录网站的用户数量。

> 访问用户的技术说明 ：
>
> Web：根据 cookie 。
>
>  APP：根据用户唯一 Id 区分访问用户（Android 用户的唯一 ID 为：Android\_ID 或 IMEI；iOS 的唯一 ID 为：IDFV 或 IDFA）。即使用户删除应用再安装，用户 ID 仍然不变。
>
> 小程序：默认按照cookie判断访问用户；如果不取关小程序，则cookie不会发生变化；当设置forceLogin后，则会默认按照openid来判断访问用户，且不采用365的限制。

### 第二部分：访问级指标 <a id="di-yi-bu-fen-fang-wen-ji-zhi-biao"></a>

> **衡量网站总体访问情况**

#### 访问量（web/app/小程序） <a id="1fang-wen-liang"></a>

访问的数量。被页面级变量分解时，代表着包含该页面的访问的次数。

#### 每次访问页面浏览量（web/app/小程序） \[ 页面浏览量 / 访问量 \] <a id="3"></a>

平均每次访问浏览的页面的数量。

#### 人均访问页数（web/app/小程序） \[ 页面浏览量 / 用户量 \] <a id="2"></a>

平均每个用户实际浏览过的网页数量，由 \[ 页面浏览量 / 用户量 \] 得来。

#### 人均访问次数（web/app/小程序） \[ 访问量 / 用户量 \] <a id="2"></a>

平均每个用户访问网站（打开 App）的次数。

#### 总访问时长（web/app/小程序） <a id="4"></a>

所有访问的总时长，以分钟作为单位展示。不能使用页面级维度（域名、页面、自定义页面级变量）分解。

#### 平均访问时长（web/app/小程序） \[ 总访问时长 / 访问量 \] <a id="5"></a>

平均每次访问时长，以分钟作为单位展示。不能使用页面级维度（域名、页面、自定义页面级变量）分解。

#### 人均访问时长（web/app/小程序） \[ 总访问时长 / 用户量 \] <a id="5"></a>

平均每个用户的访问时长，由 \[ 总访问时长 / 用户量 \] 计算得来。

#### 退出次数（web/app/小程序） <a id="6"></a>

用户退出网站的数量，通常需要在一定范围内，因为所有的用户最终都会退出网站。 与页面级变量一起使用时，统计的是该页面作为用户一次访问中的最后一个页面的访问的次数。

#### 退出率（web/app/小程序） \[ 退出次数 / 访问量 \] <a id="7"></a>

如果与页面级变量一起使用，统计的是该页面作为退出页的次数，占这个页面被访问的总体数量的比例。 每个页面都有可能成为退出页，因为用户总要离开网站，但是如果关键流程中的页面退出率高，就说明页面出现了问题，用户本应该继续完成操作，但是中途退出了。 \*退出页：用户在一次访问中访问的最后一个页面，是这次访问的退出页，也就是用户的这次访问是在这里结束的。

#### 总页面停留时长（web/小程序/app） <a id="8"></a>

总页面停留时长（分钟）指标只能被页面级维度（域名、页面、自定义页面级变量）分解，代表着用户在当前页面上停留的总时长，即访问结束的时间点减去访问开始的时间点。

#### 平均页面停留时长（web/小程序/app）\[ 总页面停留时长/（页面浏览量 - 退出次数）\] <a id="9"></a>

平均页面停留时长（分钟）指标只能被页面级维度（域名、页面、自定义页面级变量）分解，代表着用户在当前页面上停留的平均时长。

#### 进入量（web/app/小程序） <a id="10"></a>

访问用户进入网站/小程序进行访问的数量。

#### 访问用户人均进入次数（web/app/小程序） \[ 进入量 / 访问用户量 \] <a id="11"></a>

平均每个访问用户进入网站/小程序进行访问的数量。

#### 总进入时长（web/app/小程序） <a id="12"></a>

用户进入网站/小程序进行访问的总时长，以分钟作为单位展示。 与页面级变量一起使用时，统计的是该页面作为用户一次访问中的第一个页面的访问的时长。

#### 平均进入时长（web/app/小程序） \[ 总进入时长 / 进入量 \] <a id="13"></a>

用户平均每次进入网站/小程序进行访问的平均时长，以分钟作为单位展示。

#### 每次进入页面浏览量（web/app/小程序） \[ 进入总页面浏览量 / 进入量 \] <a id="14"></a>

平均每次进入带来的页面浏览的数量。

#### 跳出次数（web/小程序） <a id="15"></a>

访问一个页面就离开的次数。即一次访问中只访问了一个页面。

#### 跳出率（web/小程序） \[ 跳出次数 / 进入量 \] <a id="16"></a>

只有一个页面浏览的访问占所有访问的比率。

> 高跳出率表示访问者对到达站内时访问的第一个页面不感兴趣，没有继续访问更深入的页面，或者是登录页面设计

### 第三部分：页面级指标 <a id="di-san-bu-fen-ye-mian-ji-zhi-biao"></a>

> **衡量页面的访问情况**

#### 页面浏览量（web/app/小程序） <a id="21"></a>

用户实际浏览过的网页数量。

#### 通过圈选定义的页面浏览量（web/app/小程序） <a id="22"></a>

可以定义一个页面，也可以定义一组页面，统计定义页面的浏览量。

### 第四部分：事件级指标 <a id="di-si-bu-fen-shi-jian-ji-zhi-biao"></a>

> **可以通过圈选和创建自定义事件来实现**

#### 通过圈选定义的元素指标化后（web/app/小程序） <a id="23"></a>

通过圈选定义的元素，在使用的时候，会指标化为「该元素点击 / 浏览的人数或次数」。

#### 自定义事件（web/app/小程序） <a id="24"></a>

通过打点实施创建自定义事件。

## 预定义维度

### 第一部分：用户来源维度 <a id="01"></a>

> **通过用户来源了解用户是怎样来到你的网站上的。**

#### 1.访问来源（web/app） <a id="11"></a>

网站的流量来源，可以是百度，谷歌，优酷等站外渠道，也可能是直接访问\*该网站。可以通过设置 UTM 参数来确定流量具体是哪个广告带来的。

访问来源中微信类来源: 微信目前是一个非常重要的流量来源。一般不考虑广点通等付费推广的话，微信渠道上很多H5\WEB等有非常成熟的使用和分享、获客场景，根据微信环境中打开的数据参数，GrowingIO 识别了几种微信环境访问 H5/PC 的分类，常见的用例有这样几种：

| 场景 | 访问来源 | 解释 |
| :--- | :--- | :--- |
| 扫描二维码在微信中打开H5页面查看 | 微信-其他 | 如果不使用GrowingIO生成具体的追踪链接，仅可以识别微信环境打开；如果想要识别具体的二维码的信息，例如那篇文章的，哪个公众号等，详情可以了解广告监测链接的相关功能。 |
| 公众号中查看图文消息-点击“阅读原文” | 微信-公众号 | GroiwngIO会识别到微信的环境，微信会返回“公众号”访问来源链接（例如mp.weixinbridge.com\)，即可以判断出公众号的来源。 |
| 公众号直接给文字/图片链接，用户打开 | 微信-其他 | 如果不使用GrowingIO生成具体的追踪链接，仅可以识别微信环境打开；如果想要识别具体的二维码的信息，例如那篇文章的，哪个公众号等，详情可以了解广告监测链接的相关功能。 |
| 朋友圈里查看分享的页面类链接 | 微信-朋友圈 | GroiwngIO会识别到微信的环境，同时微信会给出相应的技术参数，即可以判断为朋友圈打开。 |
| 查看分享给群组的页面链接 | 微信-群聊 | GroiwngIO会识别到微信的环境，同时微信会给出相应的技术参数，即可以判断为群组信息中打开。 |
| 查看分享给单个好友的页面链接 | 微信-单聊 | GroiwngIO会识别到微信的环境，同时微信会给出相应的技术参数，即可以判断为好友信息中打开。 |
| 打开分享到朋友圈、群聊、单聊消息中的URL链接 | 微信-其他 | 如果仅是URL，只会追踪具体的URL，但可以识别在微信环境中打开。 |

#### 2.一级访问来源（web/app） <a id="12"></a>

为了便于分析，我们将访问来源进行了归类：直接访问，搜索引擎，社交媒体，外部链接四大部分。

为便于分析使用，我们将访问来源进行了以下归类：直接访问、搜索引擎、社交媒体、视频媒体、新闻媒体、外部链接，六大分类。

**直接访问**

a.用户直接在浏览器中输入了一个域名或使用书签进行访问；

b.从邮件中点击链接访问网站取决于电子邮件的提供商/程序）；

c.从 Microsoft Office 或 PDF 文件中点击链接访问网站；

d.通过点击由原 url 生成的短链接访问网站； 

e.通过 App 点击链接访问网站（比如今日头条、微博中的链接）（对微信做过识别，故此场景不适用微信）； 

f.通过点击一个 https 类型的 url 访问一个 http 类型的 url（比如如果点击 https://example.com/1 转到 http://example.com/2, 对于 example.com/2 的分析会认为是直接访问）；

 g.部分浏览器（特别是移动端浏览器）会把搜索跳转当成直接访问。

**搜索引擎**

| **域名** | 来源方 |
| :--- | :--- |
| google.xx.xx | Google |
| yahoo.com | 雅虎 |
| bing.com | 必应 |
|  www.baidu.com、m.baidu.com、bzclk.baidu.com | 百度 |
| so.com | 360 搜索 |
| sogou.com | 搜狗 |
| sm.cn | 神马 |
| youdao.com | 有道 |
| zhongsou.com | 中搜 |

**社交媒体** 

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x57DF;&#x540D;</th>
      <th style="text-align:left">&#x6765;&#x6E90;&#x65B9;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">facebook.com</td>
      <td style="text-align:left">Facebook</td>
    </tr>
    <tr>
      <td style="text-align:left">twitter.com&#x3001;t.co</td>
      <td style="text-align:left">Twitter</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>web.telegram.org&#x3001;org.telegram.plus&#x3001;org.telegram.multi&#x3001;</p>
        <p>org.telegram.messenger</p>
      </td>
      <td style="text-align:left">Telegram</td>
    </tr>
    <tr>
      <td style="text-align:left">linkedin.com</td>
      <td style="text-align:left">Linkedin</td>
    </tr>
    <tr>
      <td style="text-align:left">instagram.com</td>
      <td style="text-align:left">Instagram</td>
    </tr>
    <tr>
      <td style="text-align:left">weibo.com&#x3001;t.cn&#x3001;weibo.cn</td>
      <td style="text-align:left">&#x5FAE;&#x535A;</td>
    </tr>
    <tr>
      <td style="text-align:left">zhihu.com</td>
      <td style="text-align:left">&#x77E5;&#x4E4E;</td>
    </tr>
    <tr>
      <td style="text-align:left">renren.com</td>
      <td style="text-align:left">&#x4EBA;&#x4EBA;&#x7F51;</td>
    </tr>
    <tr>
      <td style="text-align:left">mp.weixin.qq.com</td>
      <td style="text-align:left">&#x5FAE;&#x4FE1;</td>
    </tr>
  </tbody>
</table>由于目前微信已经作为一个较重要的访问来源，所以 GrowingIO 目前专门针对微信环境做了判定：如果 PC 网页或 H5 的访问是发生在 wechat 环境中，也会被归入社交媒体，而根据不同的微信后置参数，进一步区分访问来源，详情请看访问来源中微信来源的维度解释。

**视频媒体**

| **域名** | 来源方 |
| :--- | :--- |
| www.youtube.com、m.youtube.com | Youtube |
| www.iqiyi.com | 爱奇艺 |
| v.qq.com | 腾讯视频 |
| v.youku.com | 优酷 |
| www.douyu.com | 斗鱼TV |
| www.bilibili.com | Bilibili |

**新闻媒体**

| **域名** | 来源方 |
| :--- | :--- |
| open.toutiao.com、ad.toutiao.com | 今日头条 |
| xw.qq.com | 腾讯新闻 |
| news.sohu.com | 搜狐新闻 |

**外部链接**

除直接访问及以上来源分类之外，其余全部算做外部链接。

#### 3.搜索词（web） <a id="13"></a>

用户从搜索引擎进入网站所使用的搜索词，一般情况下付费搜索的搜索词可以被解析，百度、谷歌、搜狗和360渠道只有付费搜索词，其他渠道既有付费搜索词也有自然搜索词。

如果在值中出现 N/A ，意为这部分流量不是通过搜索词访问的。

#### 4.App 版本（app/小程序） <a id="14"></a>

App 和小程序 的版本号

#### 5.自定义 App 渠道（app/小程序） <a id="15"></a>

自定义 App 渠道：

在APP集成SDK的时候，针对安卓用户，设置分包渠道。

在小程序中，则自动获取小程序打开的来源。目前支持微信中60多种统计场景，例如：二维码扫码，群聊中点击分享的小程序卡片等。详情请见[小程序概览-获客场景](https://growingio.gitbook.io/docs/dashboard/mina-overview#huo-ke-chang-jing)。

**案例：**在「事件分析」横向柱图中添加不同的「维度」，可以查看不同访问来源下的页面浏览量情况。

​![](http://growing.cn-bj.ufileos.com/ccc10.png)

> **通过「广告监测」设置 App 推广的维度值**

通过顶部导航栏进入「广告监测」功能，设置 App 推广的字段：![](http://growing.cn-bj.ufileos.com/ccc11.png)

> **通过「广告监测」设置网站推广的维度值**

通过顶部导航栏进入「广告监测」功能，设置网站推广的字段：

![](http://growing.cn-bj.ufileos.com/ccc12.png)

> **支持自定义 UTM 参数**

| UTM 参数 | 使用方式 | 示意 |
| :--- | :--- | :--- |
| 广告来源 utm\_source | 标识投放的网站，例如：google、baidu、toutiao | utm\_source=Google |
| 广告媒介 utm\_medium | 广告媒介或营销媒介，例如：CPC、Banner 和 EDM | utm\_medium=cpc |
| 广告名称 utm\_campaign | 产品的具体广告系列名称、标语、促销代码等 | utm\_campaign=spring\_sale |
| 广告关键词 utm\_term | 标识付费搜索关键字 | utm\_term=running+shoes |
| 广告内容 utm\_content | 用于区分相似内容或同一广告内的链接。如果在同一封 EDM 中使用了两个不同的链接，就可以使用 utm\_content 设置不同的值，以便判断哪个版本的效果更好 | utm\_content=logolink or utm\_content=textlink |

UTM 渠道归因模式为非直接访问的最后一次访问。

**案例：**可以通过设置 utm 参数，选择相应的维度「广告来源」、「广告内容」、「广告名称」、「广告关键词」、「广告媒介」等，来监控投放的推广内容效果。

![](http://growing.cn-bj.ufileos.com/ccc13.png)

### 第二部分：地域信息维度 <a id="02"></a>

> **了解用户在哪里访问你的网站**

#### 1.城市名称（web/app/小程序） <a id="21"></a>

web 基于 IP 地址，以城市作为维度值，目前只支持国内城市。 app 和小程序 基于 IP 地址和 GPS 。优先判断GPS值，GPS值缺失时，使用IP地址。

#### 2.地区名称（web/app/小程序） <a id="2-di-qu-ming-cheng-webapp-xiao-cheng-xu"></a>

web 基于IP地址，该维度包含国内省级以上行政区，以及国外地区。 app 和小程序 基于 IP 地址和 GPS 。优先判断GPS值，GPS值缺失时，使用IP地址。

#### 3.国家代码（web/app/小程序） <a id="23"></a>

用户所在的国家的英文缩写，常见的维度值有：CN，US，JP，SG等。

#### 4.国家名称（web/app/小程序） <a id="24"></a>

用户所在的国家的名称，常见的有：中国，美国，英国，新加坡等。

> 技术说明：维度指为「未知」的原因：可能是用户使用的是移动网络，或开了代理。

#### 5.微信用户所在城市（小程序） <a id="5-wei-xin-yong-hu-suo-zai-cheng-shi-xiao-cheng-xu"></a>

小程序特有维度。表示用户在微信端设置的所在城市。使用前提是小程序SDK获取到微信访问用户属性。详情请见 [小程序SDK-微信用户属性设置](https://growingio.gitbook.io/docs/sdk-integration/mina-sdk#sdk-wei-xin-yong-hu-shu-xing-she-zhi)。

#### 6.微信用户所在省（小程序） <a id="6-wei-xin-yong-hu-suo-zai-sheng-xiao-cheng-xu"></a>

小程序特有维度。表示用户在微信端设置的所在省。使用前提是小程序SDK获取到微信访问用户属性。详情请见 [小程序SDK-微信用户属性设置](https://growingio.gitbook.io/docs/sdk-integration/mina-sdk#sdk-wei-xin-yong-hu-shu-xing-she-zhi)。

#### 7.微信用户所在国家（小程序） <a id="7-wei-xin-yong-hu-suo-zai-guo-jia-xiao-cheng-xu"></a>

小程序特有维度。表示用户在微信端设置的所在国家。使用前提是小程序SDK获取到微信访问用户属性。详情请见 [小程序SDK-微信用户属性设置](https://growingio.gitbook.io/docs/sdk-integration/mina-sdk#sdk-wei-xin-yong-hu-shu-xing-she-zhi)。

### 第三部分：设备信息维度 <a id="03"></a>

> **了解用户使用什么设备访问你的网站**

#### 1.网站/手机应用（web/app/小程序） <a id="31"></a>

用于区分该设备是接入了 GrowingIO 的 JS SDK 还是 iOS SDK、Android SDK 等。

#### 2.屏幕大小（web/app/小程序） <a id="32"></a>

web 端是窗口大小，移动端是屏幕大小。

#### 3.操作系统（web/app/小程序） <a id="33"></a>

用户所使用的操作系统，比如 Windows 8 ，Windows 7 ，Mac OS X ，Android，weixin-iOS，weixin-Android。

#### 4.操作系统版本（web/app/小程序） <a id="34"></a>

同「浏览器」，但是会按照不同的版本进行区分，比如 Android 4.0 等。

#### 5.操作系统语言（web/app/小程序） <a id="35"></a>

统计不同的操作系统语言的使用情况，比如简体中文等。

#### 6.浏览器（web） <a id="36"></a>

用户所用浏览器的类型，比如 Chrome，Chrome Mobile，Safari，IE 等。

#### 7.浏览器版本（web） <a id="37"></a>

同「浏览器」，但是会按照不同的版本进行区分，比如 Chrome 47.0.2526 等。

#### 8.设备品牌（app/小程序） <a id="38"></a>

将不同设备的品牌作为维度值。

#### 9.设备型号（web/app/小程序） <a id="39"></a>

用于区分具体的机型。

#### 10.设备类型（web/app/小程序） <a id="310"></a>

设备的类型，平板和手机。

### 第四部分：其他维度 <a id="04"></a>

> **页面级维度**

对于 web 端可以这样理解： 用户先访问了 https://www.growingio.com/ 再访问了 https://www.growingio.com/circle

#### 1.域名（web/小程序） <a id="41"></a>

www.growingio.com 是这两个页面的域名。

小程序为appID.

#### 2.页面（web/app/小程序） <a id="42"></a>

对于 web 端可以这样理解： / 是 https://www.growingio.com**/** 的页面。 /circle 是 https://www.growingio.com**/circle** 的页面。

对于 app 端可以这样理解： android : activity + fragment iOS : UIViewController

小程序：页面URL（不包括query）

#### 3.页面来源（web/app/小程序） <a id="43"></a>

这次访问中 https://www.growingio.com/circle 这个页面的页面来源是 https://www.growingio.com/ 。

> **事件级维度：当次事件发生时，对应的维度**

#### 4.设备方向（app） <a id="44"></a>

可以理解为用户的手机时横屏还是竖屏。

#### 5.元素内容（web/app/小程序） <a id="45"></a>

通过圈选可定义的维度包括“元素内容“ 和 “元素位置“。

圈选某个元素时，如果该元素本身有 "内容"信息，即可用 "元素内容" 来统计该元素对应的指标。

#### 6.元素位置（web/app/小程序） <a id="46"></a>

如果该元素本身有 "位置"信息，即可用 "元素位置"来统计该元素对应的指标。

**案例：**我们在圈选时只能看到一种元素，但是可能用户看到的网站内容不一样，元素的内容也不一样，因此，当我们在定义一个元素时，要思考我们想要统计的是「现在这个位置的按钮点击情况」还是「这个位置上这个内容的按钮的点击情况」。常见于商品位、AB测试等使用场景。

在下图中，有一部分用户看到的按钮是「立即注册」，还有一部分用户看到的按钮是「免费试用」，因此，如果我想定义这个按钮的点击情况，不管是什么内容，那么就只「限定顺序」，不限定其他条件：![](https://docs.growingio.com/.gitbook/assets/21_32_36__04_25_2018%20%281%29.jpg)

如果想看这个位置上不同内容的点击情况，可以在「事件分析」中，选择「柱图」，用「元素内容」作为维度，来进行分析。使用「元素位置」作为维度来分析时，可以看到「元素位置」的值都是 2（因为在圈选时限定了元素的位置）。

#### 7.时间（web/app/小程序） <a id="47"></a>

以「小时」粒度切分时，代表当前小时的开始到结束； 以「天」粒度切分时，代表北京时间的 0:00-24:00。

### 第五部分：用户性别 <a id="di-wu-bu-fen-yong-hu-xing-bie"></a>

#### 1. 微信用户性别 （小程序） <a id="1-wei-xin-yong-hu-xing-bie-xiao-cheng-xu"></a>

小程序特有维度。表示用户在微信端设置的性别。通常为男、女、未知（表示未设置性别信息）。使用前提是小程序SDK获取到微信访问用户属性。详情请见 [小程序SDK-微信用户属性设置](https://growingio.gitbook.io/docs/sdk-integration/mina-sdk#sdk-wei-xin-yong-hu-shu-xing-she-zhi)。

