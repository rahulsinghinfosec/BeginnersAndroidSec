<h1>Day 9</h1>
<small>Reference: developer.android.com & blog.oversecured.com</small>
<p><b>Web View</b></p>
<p>If you want to deliver a web application (or just a web page) as a part of a client application, you can do it using WebView. The WebView class is an extension of Android's View class that allows you to display web pages as a part of your activity layout. It does not include any features of a fully developed web browser, such as navigation controls or an address bar. All that WebView does, by default, is show a web page.</p>
<p>A common scenario in which using WebView is helpful is when you want to provide information in your app that you might need to update, such as an end-user agreement or a user guide. Within your Android app, you can create an Activity that contains a WebView, then use that to display your document that's hosted online.</p>
<p>It is a fancy web browser that allows developers, among other things, to bypass standard browser security. Any misuse of these features by a malicious actor can lead to vulnerabilities in mobile apps.</p>
<p>One of these features is that a WebView allows you to intercept app requests and return arbitrary content, which is implemented via the <code>WebResourceResponse</code> class.</p>
<p><b>WebResrouceResponse</b></b>
<p>Encapsulates a resource response. Constructs a resource response with the given MIME type, character encoding, and input stream. Applications can return an instance of this class from <code>WebViewClient#shouldInterceptRequest</code> to provide a custom response when the WebView requests a particular resource.</p>
<p>In other words: The implementation of WebResourceResponse which is a WebView class that allows an Android app to emulate the server by returning a response (including a status code, content type, content encoding, headers and the response body) from the app’s code itself without making any actual requests to the server.</p>
<p><code>
WebView webView = findViewById(R.id.webView); <br>
webView.setWebViewClient(new WebViewClient() { <br>
   public WebResourceResponse shouldInterceptRequest(WebView view, WebResourceRequest request) { <br>
       Uri uri = request.getUrl(); ,br>
       if (uri.getPath().startsWith("/local_cache/")) { <br>
           File cacheFile = new File(getCacheDir(), uri.getLastPathSegment()); <br>
           if (cacheFile.exists()) { <br>
               InputStream inputStream; <br>
               try { <br>
                   inputStream = new FileInputStream(cacheFile); <br>
               } catch (IOException e) { <br>
                   return null; <br>
               } <br>
               Map<String, String> headers = new HashMap<>(); <br>
               headers.put("Access-Control-Allow-Origin", "*"); <br>
               return new WebResourceResponse("text/html", "utf-8", 200, "OK", headers, inputStream); <br>
           } <br>
       }<br>
       return super.shouldInterceptRequest(view, request); <br>
   } <br>
}); <br>
</code>
</p>
<small>Code taken from : blog.oversecured.com</small>
<p>If the request URI matches the given pattern, it fetches the response from the local storag</p>
<p>The problem arises when an attacker can manipulate the path of the returned file and, through XHR requests, gain access to arbitrary files.</p>
