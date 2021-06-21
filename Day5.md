<h1>Day5</h1>
<p><b>Supplementary Authentication</b></p>
<p>This includes additinal info gathered by the server. This is completely transparent to the user.This is generally used to detect anomaly.This can include:</p>
<ul>
  <li>Geolocation</li>
  <li>IP address</li>
  <li>Time of the day</li>
  <li>Device being used.</li>
</ul>
<p>Perform the following steps when testing authentication and authorization</p>
<ul>
  <li>Identify all the additional authentication factors implemented by the application.</li>
  <li>Check for the endpoints that provide critical functionality.</li>
  <li>Verify additional features implemented on the server-side.<li>
</ul>

<p>Authentication vuln. exists when the authentication state is not enforced on the server and when the client can tamper with the state</p>
<p>For example, let the client make the following GET request to the server</p>
<a href="#">http://www.site.com/auth/user/1/authenticated=no</a>
<p>You could change it to "yes" thus bypassing the authentication completely.Modern applications might not use this, but implement the same functionality using the cookies. You can try to tamper with the cookies.</p>
<p>To prevent tampering with the client side tokens, the tokens could be signed with cryptographic signatuers.Like JSON Web Tokens.However there are a few workarounds in a few cases to this as well.</p>

<p><b>Login Throttling</b></p>
<p>You need to check the source code for the throttling procedure. It is when the counter increases its value each time a user types in a wrong password.If it exceeds a particular value, it must log you out for a day.The counter should reset to 0 once the user has logged in successfully.</p>
<p>You can check this functionality using Burp and OWASP ZAP. Try to login and use a proxy for the traffic. You can learn more about it <a href='https://portswigger.net/support/configuring-an-android-device-to-work-with-burp'>Here</a>
<p><b>Session Cookie/ID reuse</b></p>
<p>After the user logs out, the session cookie must be destroyed on the server side. Try to use the same session cookie/id. If it works, then it is vulnerable to session resue</p>
<p>Many apps use pre-built frameworks for implementing session id generation and termination. Check the docs of the framework used, to see if they are configured properly</p>
<ul>
  <li>Spring(Java)</li>
  <li>Struts(Java)</li>
  <li>Larval(PHP)</li>
  <li>Ruby on Rails</li>
</ul>

<p><b>Testing Session Timeouts</b></p>
<p>Many frameworks give the option of automatically timeout of the session cookies. Check the source code<b>(Static analysis)</b> to check whether it is implemented. Session should timeout to prevent account hijacking</p>
<p><b>Dynamic Analysis</b> : Log into the application and then try to send requests at intervals (using burp/owasp). Example : 10 min, 20, 1hr, etc.</p>

<h2>Tesging Network Connection</h2>
<p>Generally apps use HTTP over TLS/SSL. But not always.</p>
<p><b>Intercepting HTTP(s) Traffic</b></p>
<p>You can intercept the traffic and then pass it through a network proxy.You can even tinker with the data fields to see how the server reponds to it <br> The most common proxies are : <b>BurpSuite, OWASP ZAP, Charles Proxy</b></p>
<p><b>NOTE:</b>If the app uses TLS, using proxy can break it and therefore you might have problem initiating connections. You'll have to install a CA certificate as a workaround. Further in many cases, they are unable to decode the non-HTTP traffic, so you might need to install extensions(which is a bit tough to setup). They are : <b>Burp non-HTTP-Extension and Mitm Realy</b></p>

<p><b>Intercepting Traffic on the Network Layer</b></p>
<p>You can use tools like wireshark,tcpdump, and even use tools like bettercap to redirect the traffic to your computer (MiTM attack)</p>

<p><b>Testing Code Quality</b></p>
<ul>
  <li>Injection Flaws</li>
  <ul>
    <li>Sql Injection</li>
    <li>XXE Injection</li>
    <li>You might not find CSRF or XSS in native apps. But webViews could be a viable attack vector. </li>
  </ul>
</ul>
<p><b>Examples of XSS in WebView</b></p>
<p>Java: webView.loadUrl("javascript:initialize(" + myNumber + ");"); </p>
<p>Kotlin : webView.loadUrl("javascript:initialize($myNumber);") </p>

<p><b>Android Users and Groups</b></p>
<p>Even though Andorid is based on Linux, it doesn't implement users accounts as the way Linux would do. As we know each app runs in its own sandbox and has its own set of resources allocated to it by the system. The same goes for apps. It is  as if <b>each app runs under a sparate user</b>, which is separate from other apps and the operating system.</p>

<p>For example, Android Nougat defines the following system users: <br>
#define AID_ROOT  0  /* traditional unix root user */ <br>
#define AID_SYSTEM 1000 /* system server */ <br>
#...<br>
#define AID_SHELL  2000 /* adb and debug shell user */<br>
#...<br>
#define AID_APP 10000 /* first app user */</p>


<p><b>Android Device Encryption</b></p>
<ol>
  <li>Full Disk Encryption</li>
  <p>Andoird 5.0 supports this type of encryption. A single key is used to encrypt the entire disk (the key is protected by the user's password). This scheme has a few drawbacks. You can't access abything,be it calls or alarms after the device is rebooted as you'll need a password to first open the device, which will then decrypt them, for use </p>
  <li>File Based Encryption</li>
  <p>Android 7.0 supports this type of encryption. Each file is encrypted with a different key. The advantage of this scheme is that it suppors Direct Boot. Which means that users can have access to emergency calls and alarms, etc. even if the device is locked and needs a password to unlock.</p>
  <li>Adiantum</li>
  <p>AES is a common encryption scheme preferred by almost everyone. It is so widely used that many new processors have new instruction sets to provide hardware accelerate when AES is being implemented. But many low end processors can't handle this. So, Adiantum was developed. It can be considered secure as long as ChaCha12 and SHA-256 are secure. It is 4x faster while encryting and 5x faster while decrypting as compared to AES.It is available in Android versions > 9,but adroid does not provide you with an API to use it for any other purpose.</p>
</ol>
<p><b>Communication with the OS</b></p>
<p>Android Apps interact with the system services via the Android Framework. It is an abstraction layer that provides higher level Java API's. Apps make use of these API calls to do their tasks</p>
<p>Some examples of System services include: </p>
<ul>
  <li>Communicatin (Wifi/Bluetooth/NFC,etc)
  <li>Files</li>
  <li>Camera</li>
  <li>GPS,microphone,etc.</li>
</ul>
<p>The framework also offers some cryptographic functions.</p>
<p><b>Linux UID/GID for applications </b></p>
<p>Android leverages Linux user management to separate apps. Each app is provided with its own user id (UID) and runs as a separte process, provided that it is allowed to run. Each app has access to only its resources. This protection is enforced by the Linux Kernel. Generally, the apps are assigned a UID between 10,000 to 99,999. If given an id of 10108, it'll have a user name of u0_a_108. </p>

<p><b>The App Sandbox</b></p>
<p>An app has access to only its own resources. Each time a new app is installed, a new directory is created <b>data/data/[package-name]</b>. The permissions of the directory are set in a way that only the app with its UID can have access to the resources. This adds another layer of security as no other app can have access to the other app's data.</p>
<p>Example<br>
 drwx------ 4 u0_a97 u0_a97 4096 2017-01-18 14:27 com.android.calendar <br>
 drwx------ 6 u0_a120 u0_a120 4096 2017-01-19 12:54 com.android.chrome </p>
 
 <p><b>NOTE : </b>Developers who want to share common sandbox can sidestamp sandboxing. This can be done if the two apps are signed with the same certificate and have the same user id (having the sharedUserId in their AndroidManifest.xml files),they can have access to each other's directory.</p>

<p><b>Zygote</b></p>
<p>It starts up during Android Initialization. It contains all the necessary libraries an app needs to function. It sets up a socket (/dev/socket/zygote) and listens for connections from local clients.It then forks up a process, which then loads and executes app-specific code.</p>

<p><b>Inter process Communication</b></p>
<p>Intent: Intent is an asynchronous communication framework. It allows both point-to-point and publish-subscribe messaging. An intent is a messaging object that can be used to request an action from another object. The three fundamental use cases of intent are: </p>
<ul>
  <li>Starting an Activity : An activity represents a single app screen. </li>
  <li>Starting a service : A service is a component that runs in the background without the user interface (android 5+ you can start a service with JobScheduler) </li>
  <li>Deliver Broadcast : A broadcast is a message that any app can receive.</li>
</ul>
