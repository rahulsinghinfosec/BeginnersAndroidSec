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

