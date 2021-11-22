#### 1 事先准备

##### 1.1 下载并安装Android Studio

https://developer.android.google.cn/studio

##### 1.2 创建一个Empty Activity

##### 1.3 创建AVD安卓虚拟机

#### 2 使用WebView

##### 2.1 打开URL

在AndroidManifest.xml中，把`<TextView>`删了，并写上`<WebVeiw>`

```xml
    <WebView
        android:id="@+id/webview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
    />
```

在MainActivity.java中，`onCreate`函数里写入

```java
    WebView myWebView = (WebView) findViewById(R.id.webview);
    myWebView.loadUrl("http://www.example.com");
```

或在MainActivity.kt中，`onCreate`函数里写入

```kotlin
    val myWebView: WebView = findViewById(R.id.webview)
    myWebView.loadUrl("http://www.example.com")
```

注：二者都需要导入`android.webkit.WebView`这个包



若出现`ERR_CLEARTEXT_NOT_PERMITTED`，是因为Google针对Android P版本以后的应用程序，将要求默认使用加密连接，也就是不允许使用http协议访问，解决办法之一是修改清单文件允许APP使用HTTP协议

故在AndroidManifest.xml中，写入

```xml
 <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:usesCleartextTraffic="true"
        android:theme="@style/Theme.WebView">
        <activity
            android:name=".MainActivity"
```

主要是`android:usesCleartextTraffic="true"`这一行



若出现`ERR_CACHE_MISS`，是因为APP无权链接网络。解决方法：在AndroidManifest.xml文件中加入联网的权限 `<uses-permission android:name="android.permission.INTERNET"></uses-permission>`即可

故在AndroidManifest.xml中，写入

```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.example.webview">
    <uses-permission android:name="android.permission.INTERNET"/>
    <application
```

主要是`<uses-permission android:name="android.permission.INTERNET"/>`这一行

##### 2.2 解析HTML

在MainActivity.java中，`onCreate`函数里写入

```java
	WebView myWebView = (WebView) findViewById(R.id.webview);
    // myWebView.loadUrl("http://www.example.com");
	StringBuilder sb = new StringBuilder();
	sb.append("<h1>Hello Andriod</h1>");
	myWebView.loadDataWithBaseURL(null, sb.toString(), "text/html", "utf-8", null);
```

或在MainActivity.kt中，`onCreate`函数里写入

```kotlin
	val myWebView: WebView = findViewById(R.id.webview)
    // myWebView.loadUrl("http://www.example.com")
	val unencodedHtml = "<h1>Hello Andriod</h1>"
    val encodedHtml = Base64.encodeToString(unencodedHtml.toByteArray(), Base64.NO_PADDING)
    myWebView.loadData(encodedHtml, "text/html", "base64")
```

##### 2.3 导入HTML文件并使用 JavaScript

在MainActivity.java中，`onCreate`函数里写入

```java
    WebView myWebView = (WebView) findViewById(R.id.webview);
    // myWebView.loadUrl("http://www.example.com");
	// StringBuilder sb = new StringBuilder();
	// sb.append("<h1>Hello Andriod</h1>");
	// myWebView.loadDataWithBaseURL(null, sb.toString(), "text/html", "utf-8", null);
    // 支持Javascript
    myWebView.getSettings().setJavaScriptEnabled(true);
    // 不会打开选择浏览器
    myWebView.setWebChromeClient(new WebChromeClient());
    // 加载app/assets/index.html
    myWebView.loadUrl("file:///android_asset/index.html");
```

或在MainActivity.kt中，`onCreate`函数里写入 （TODO）

```kotlin
    val myWebView: WebView = findViewById(R.id.webview)
    // myWebView.loadUrl("http://www.example.com")
    // val unencodedHtml = "<h1>Hello Andriod</h1>"
    // val encodedHtml = Base64.encodeToString(unencodedHtml.toByteArray(), Base64.NO_PADDING)
    // myWebView.loadData(encodedHtml, "text/html", "base64")
	// 支持Javascript	
	myWebView.settings.javaScriptEnabled = true
```

