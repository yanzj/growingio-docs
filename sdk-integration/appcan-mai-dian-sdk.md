---
description: GrowingIO 埋点 SDK 仅自动采集设备信息和您埋点内容。
---

# AppCan 埋点 SDK

## 集成

### 添加自定义插件

* 下载 自定义插件

| 插件平台    | 下载地址 |
| :--- | :--- |
| Android | [https://assets.growingio.com/sdk/android/uexGrowingIO-android-2.6.0.zip](https://assets.growingio.com/sdk/android/uexGrowingIO-android-2.6.0.zip) |
| iOS | [https://assets.growingio.com/sdk/ios/uexGrowingIO-iOS-2.6.0.zip](https://assets.growingio.com/sdk/ios/uexGrowingIO-iOS-2.6.0.zip) |

* 在 AppCan IDE 中导航栏中选择 “AppCan” -&gt; “自定义插件“ -&gt; “添加插件”
* 选择对应安装包后，如图所示：

![](../.gitbook/assets/image%20%28115%29.png)



## Android 集成

Android AppCan 集成方式与官网默认的无埋点集成方式不一样， 请按照本文档集成。

### 1. 添加URLScheme和权限

在官网添加 Android 应用，找到黄色高亮中对应的 项目ID 和 URLScheme。

把 URL Scheme 添加到您的项目，以便使用 [MobileDebugger](growingio-debugger/) 时唤醒您的程序。将该产品的URLScheme添加到你的`AndroidManifest.xml`中的`LAUNCHER` `Activity`下。例如：

```markup
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    package="org.zywx.wbpalmstar.widgetone.uexDemo"
    android:versionCode="1"
    android:versionName="3.0"
    tools:overrideLibrary="org.zywx.wbpalmstar.widgetone.uex">    
    <!-- GrowingIO 需要的权限 -->
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW"/>
    <application
        android:label="Plugin Demo">
        <activity
            android:name="org.zywx.wbpalmstar.engine.LoadingActivity"
            android:configChanges="keyboardHidden|orientation"
            android:launchMode="standard"
            android:screenOrientation="portrait"
            android:theme="@style/browser_loading_theme">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
            <!--GrowingIO 请添加这里的整个 intent-filter 区块，并确保其中只有一个 data 字段-->
            <intent-filter>
                <data android:scheme="growing.您的URL Scheme" />
                <action android:name="android.intent.action.VIEW" />

                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
            </intent-filter>
            <!--请添加这里的整个 intent-filter 区块，并确保其中只有一个 data 字段-->
        </activity>
        <activity android:name="com.test.HelloAppCanNativeActivity" />
    </application>
</manifest>
```

### 3. 初始化 SDK

在 `appcan.ready`的时候初始化 GrowingIO，如下：

```javascript
appcan.ready(function() {
    //appcan.initBounce();
    initGio();
})
function initGio() {
    var options = {
        debug : true,
        channel : 'xx应用市场'
    };
    uexGrowingIO.init("您的 ProjectId ", "您的 URL Scheme", options);
}
```



## iOS 集成

### 1. 获取 URL Scheme 和 ProjectId

在官网创建 iOS  应用后，只需关心整个安装文档中的两个黄色高两块， 其为对应的 URL Scheme 和 accoundId。

### 2. 添加 ProjectId 

* 打开项目中的 config.xml 文件
* 选择底部的 “插件AppKey配置”
* 点击 “添加” 并修改对应的插件名称为`uexGrowingIO`
* 点击 “添加param”，输入键为：`$uexGrowingIO_accountId$`，随后填入您的值

![](../.gitbook/assets/image%20%2843%29.png)

### 3. 添加 URL Scheme 

#### \(1\) 获取 URL Scheme

* 添加新产品：登录官网 -&gt; 点击项目选择框  -&gt; 点击“设置”icon -&gt; 点击“新建应用”  -&gt; 选择添加 iOS 应用 -&gt; 填写“应用名称”，点击下一步 -&gt; 在第二段中标黄字体。
* 现有产品：登录官网  -&gt;   点击“设置”icon  -&gt;  点击“应用管理”  -&gt;  找到对应产品的 URL Scheme

![&#x5E94;&#x7528;&#x7BA1;&#x7406;&#x5165;&#x53E3;](../.gitbook/assets/image%20%28134%29.png)

#### \(2\) 添加 URL Scheme

![](../.gitbook/assets/image%20%2888%29.png)



## 自定义事件和变量

对于用户行为，比如搜索、添加到购物车、购买等，我们可以很很容易的通过一行代码采集到这些事件，比如：

```javascript
uexGrowingIO.track("purchase", 456, { item: '123' }, onSucc, onFail)
```



### 采集自定义事件

```javascript
uexGrowingIO.track(eventId, number, eventLevelVariable)
```

采集自定义事件 `eventId`，该事件的属性信息属于事件级变量。

在添加所需要发送的事件代码之前，需要在打点管理用户界面配置事件以及事件级变量`eventLevelVariable`。

**参数说明：**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x53C2;&#x6570;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>eventId</code>
      </td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x6807;&#x8BC6;&#x7B26;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>number</code>
      </td>
      <td style="text-align:left">Number</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">
        <p>&#x4E8B;&#x4EF6;&#x7684;&#x6570;&#x503C;&#xFF0C;&#x6CA1;&#x6709;number&#x53C2;&#x6570;&#x65F6;&#xFF0C;&#x4E8B;&#x4EF6;&#x9ED8;&#x8BA4;&#x52A0;&#x4E00;&#xFF1B;</p>
        <p>&#x5F53;&#x51FA;&#x73B0;number&#x53C2;&#x6570;&#x65F6;&#xFF0C;&#x4E8B;&#x4EF6;&#x81EA;&#x589E;number&#x7684;&#x6570;&#x503C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>eventLevelVariable</code>
      </td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">&#x5426;</td>
      <td style="text-align:left">&#x4E8B;&#x4EF6;&#x53D1;&#x751F;&#x65F6;&#x6240;&#x4F34;&#x968F;&#x7684;&#x7EF4;&#x5EA6;&#x4FE1;&#x606F;</td>
    </tr>
  </tbody>
</table>**参数限制条件：**

参数违反以下条件将不发送数据，调用后请验证数据是否发送，事件类型`t`为`cstm`。

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x9650;&#x5236;&#x6761;&#x4EF6;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>eventId</code>
      </td>
      <td style="text-align:left">&#x975E;&#x7A7A;&#xFF0C;&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF1B;</td>
    </tr>
    <tr>
      <td style="text-align:left"> <code>number</code>
      </td>
      <td style="text-align:left">&#x975E;&#x7A7A;&#x3002;</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>eventLevelVariable</code>
      </td>
      <td style="text-align:left">
        <p>&#x975E;&#x7A7A;&#xFF0C;&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;100&#xFF08;<code>eventLevelVariable.length()&lt;=100</code>&#xFF09;&#xFF1B;</p>
        <p><code>eventLevelVariable</code> &#x5185;&#x90E8;&#x4E0D;&#x5141;&#x8BB8;&#x5D4C;&#x5957;
          Object&#xFF1B;</p>
        <p><code>eventLevelVariable</code>Object &#x4E2D;&#x7684; <code>key</code>&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;<code>value</code>&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x7B49;&#x4E8E;1000&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>**示例代码：**

```java
// track API调用示例一
uexGrowingIO.track("registerSuccess");
// track API调用示例二
uexGrowingIO.track("registerSuccess",{ 'item': '123' });
// track API调用示例三
uexGrowingIO.track("loanAmount", 80000, { "gender":"male","age":"21" });
```

**检验数据发送日志示例：** 

注意 `t` 等于 `cstm` 字段，表示自定义事件发送成功，只需注意 `var`、`n` 、`num`字段，其它字段无需仔细验证**。**

```javascript
//展示 track 接口调用示例三日志内容
{
    "s":"31e3aa14-5241-490c-821c-a741e9bf0f87",
    // t 为事件类型， track 接口调用发送的事件类型为 cstm
    "t":"cstm",
    "tm":1532085495251,
    "d":"com.growingio.android.test",
    // n 为 eventId 参数携带的值
    "n":"loanAmount",
    // var 为 eventLevelVariable 参数携带的值
    "var":{
        "gender":"male",
        "age":"21"
    },
    "ptm":0,
    // num 为 number 参数携带的值
    "num":80000,
    "gesid":18,
    "esid":0,
    "u":"b6247b01-a31a-3bc6-a391-4c456888c1ee"
}
```

{% hint style="info" %}
#### 推荐您使用MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[cstm 事件验证](growingio-debugger/best-practice.md#cstm-shi-jian-yi-ji-guan-lian-de-shi-jian-ji-bian-liang-shi-jian)。
{% endhint %}



### 设置转化变量

```javascript
uexGrowingIO.setEvar(conversionVariables)
```

发送一个转化信息用于高级归因分析，在添加代码之前必须在打点管理界面上声明转化变量。

转化变量是一种非常强大的变量类型，主要是为了归因而用，比如访问渠道、站外搜索关键词、站内搜索关键词等等。在 GrowingIO 里面可以定制变量的归因方式和持久性范围。

**参数说明：**

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| conversionVariables | Object | 是 | 转化级属性 |

**参数限制条件：**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x9650;&#x5236;&#x6761;&#x4EF6;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">conversionVariables</td>
      <td style="text-align:left">
        <p>&#x975E;&#x7A7A;&#xFF0C;&#x952E;&#x503C;&#x5BF9;&#x4E2A;&#x6570;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;100&#xFF1B;</p>
        <p><code>conversionVariables</code> &#x5185;&#x90E8;&#x4E0D;&#x5141;&#x8BB8;&#x542B;&#x6709;<code>Object</code><b> </b>&#x5D4C;&#x5957;&#xFF1B;</p>
        <p><code>conversionVariables</code>Object &#x4E2D;&#x7684; <code>key</code>&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;<code>value</code>&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x7B49;&#x4E8E;1000&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>**示例代码：**

```java
uexGrowingIO.setEvar({ "evarTest":111,"campaignId":"1234567890","campaignOwner":"Li Si" });
```

**检验数据发送日志示例：** 

注意 `t` 等于`evar`字段，表示自定义事件发送成功，只需注意 `var` 字段，其它字段无需仔细验证**。**

```javascript
{
    "s":"e1c48845-dd60-4cf2-b1a5-a8e529d2188d",
    // t 为事件类型， evar 为转化事件
    "t":"evar",
    "tm":1532338526083,
    "d":"com.growingio.android.test",
    "cs1":"GrowingIO",
    // 转化变量
    "var":{
        "evarTest":111,
        "campaignId":"1234567890",
        "campaignOwner":"Li Si"
    },
    "gesid":300,
    "esid":22
}
```

{% hint style="info" %}
#### 推荐您使用 MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[ evar 事件验证](growingio-debugger/best-practice.md#evar-zhuan-hua-bian-liang-shi-jian)
{% endhint %}



### 设置用户级变量

```javascript
uexGrowingIO.setPeopleVariable(peopleVariables)
```

设置用户自身属性相关的属性信息，比如用户姓名、邮件地址、信用等级等。

在添加代码之前必须在打点管理界面上声明用户变量。

**参数说明：**

| 参数名 | 类型 | 是否必填 | 描述 |
| :--- | :--- | :--- | :--- |
| peopleVariables | Object | 是 | 用户属性 |

**参数限制条件：**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x9650;&#x5236;&#x6761;&#x4EF6;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">peopleVariables</td>
      <td style="text-align:left">
        <p>&#x975E;&#x7A7A;&#xFF0C;&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;100&#xFF08;<code>peopleVariables.length()&lt;=100</code>&#xFF09;&#xFF1B;</p>
        <p><code>peopleVariables</code> &#x5185;&#x90E8;&#x4E0D;&#x5141;&#x8BB8;&#x542B;&#x6709;<code>JSONObject</code>&#x6216;&#x8005;&#xFF1B;</p>
        <p><code>peopleVariables</code>Object &#x4E2D;&#x7684; <code>key</code>&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;<code>value</code>&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x7B49;&#x4E8E;1000&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>**示例代码：**

```java
uexGrowingIO.setPeopleVariable({ 'name': '玎玎', 'email': 'dingding@growingio.com' })
```

**检验数据发送日志示例：** 

注意 `t` 等于`ppl`字段，表示用户变量发送成功，只需注意 `var`字段，其它字段无需仔细验证。

```javascript
{
    "s":"a35872af-13df-4479-90bc-25558d12328e",
    // t 为事件类型， pvar 为发送用户变量事件
    "t":"ppl",
    "tm":1532339208991,
    "d":"com.growingio.android.test",
    "cs1":"GrowingIO",
    // 用户变量
    "var":{
        'name': '玎玎', 
        'email': 'dingding@growingio.com'
    },
    "gesid":311,
    "esid":0
}
```

{% hint style="info" %}
#### 推荐您使用 MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[ ppl 事件验证](growingio-debugger/best-practice.md#ppl-yong-hu-bian-liang-shi-jian)
{% endhint %}

### 

### 关联注册用户

```javascript
uexGrowingIO.setUserId(userId);
```

把 GrowingIO 识别的访问用户跟应用自身的注册用户做关联，用以登录用户行为分析。

**参数说明：**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x53C2;&#x6570;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">userId</td>
      <td style="text-align:left">String</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x767B;&#x5F55;&#x7528;&#x6237;Id&#xFF0C;&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;1000&#xFF1B;</p>
        <p>&#x5982;&#x679C;&#x503C;&#x4E3A;&#x7A7A;&#x5219;&#x6E05;&#x7A7A;&#x4E86;&#x767B;&#x5F55;&#x7528;&#x6237;&#x53D8;&#x91CF;&#xFF0C;&#x4E0D;&#x5EFA;&#x8BAE;&#x8FD9;&#x4E48;&#x7528;&#xFF0C;</p>
        <p>&#x8BF7;&#x4F7F;&#x7528; clearUserId &#x6E05;&#x9664;&#x767B;&#x5F55;&#x7528;&#x6237;&#x53D8;&#x91CF;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>**示例代码：**

```java
uexGrowingIO.setUserId('xiaoming');
```

注：您的 App 每次用户升级版本时无需重新登录的话，建议在用户每次升级App 版本后初次访问时重新调用上述 setUserId 方法。

{% hint style="info" %}
#### 推荐您使用 MobileDebugger，我们为您列举了应用场景和验证示例，请移步查看：[ 用户变量](growingio-debugger/best-practice.md#chang-jing-yi-yong-hu-bian-liang-zhi-deng-lu-yong-hu-id)
{% endhint %}



### 解除关联注册用户

```javascript
uexGrowingIO.clearUserId();
```

当访问用户跟注册用户关联后，之后触发的行为会绑定到该注册用户上。如果有需要解除绑定，比如用户退出登录后，可以通过该函数解决绑定。

**示例**

```javascript
uexGrowingIO.clearUserId();
```



### 设置访问用户变量

当用户未登录时，定义用户属性变量，也可用于A/B测试上传标签。

```java
uexGrowingIO.setVisitor(visitorVar)
```

**参数说明：**

<table>
  <thead>
    <tr>
      <th style="text-align:left">&#x53C2;&#x6570;&#x540D;&#x79F0;</th>
      <th style="text-align:left">&#x53C2;&#x6570;&#x7C7B;&#x578B;</th>
      <th style="text-align:left">&#x5FC5;&#x586B;</th>
      <th style="text-align:left">&#x8BF4;&#x660E;</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>visitorVar</code>
      </td>
      <td style="text-align:left">Object</td>
      <td style="text-align:left">&#x662F;</td>
      <td style="text-align:left">
        <p>&#x4E0D;&#x53EF;&#x4F7F;&#x7528;&#x5D4C;&#x5957;&#x7684;<code>JSONObject</code>&#x5BF9;&#x8C61;&#xFF0C;&#x5373;&#x4E3A;JSONObject&#x4E2D;&#x4E0D;&#x53EF;&#x4EE5;&#x653E;&#x5165;<code>JSONObject</code>&#x6216;&#x8005;<code>JSONArray</code>&#xFF1B;</p>
        <p>key &#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x4E8E;&#x7B49;&#x4E8E;50&#xFF0C;value&#x957F;&#x5EA6;&#x9650;&#x5236;&#x5C0F;&#x7B49;&#x4E8E;1000&#xFF0C;&#x503C;&#x4E0D;&#x80FD;&#x4E3A;&#x7A7A;&#x4E32;&#xFF0C;&#x4E5F;&#x5C31;&#x662F;&quot;&quot;&#x3002;</p>
      </td>
    </tr>
  </tbody>
</table>**示例代码：**

```java
uexGrowingIO.setVisitor({"gender":"male","age":21});
```

**检验数据发送日志示例：** 

注意 `t` 等于`vstr`字段，表示访问用户变量发送成功，其它字段无需仔细验证。

```javascript
{
    "s":"d334b4a1-57eb-4bf4-b426-64c1cce5a5c0",
    // t 为事件类型， vstr 为发送访问用户变量事件
    "t":"vstr",
    "tm":1532341259134,
    "d":"com.growingio.android.test",
    "cs1":"GrowingIO",
    //访问用户变量
    "var":{
        "gender":"male",
        "age":21
    },
    "gesid":322,
    "esid":0
}
```



## 验证 SDK 是否正常采集

#### 验证内容：

1. 验证打点事件是否发送

#### 验证工具：

1. [Mobile Debugger](growingio-debugger/)
2. Android [查看日志：](android-sdk/android-sdk.md#she-zhi-debug-mo-shi)初始化GrowingIO时打开测试模式

```java
var options = {
        //打开测试模式
        debug : true,
        channel : 'xx应用市场'
    };
uexGrowingIO.init("您的 ProjectId ", "您的 URL Scheme", options);
```

    





