<h1>Day8</h1>
<h5>Reference : OWASP MOBILE SECURITY TESTING GUIDE 1.1.3</h5>
<p><b>Testing Backups for Sensitive Data</b></p>
<p>Like other modern mobile operating systems, Android offers auto-backup features. The backups usually include
copies of data and settings for all installed app</p>
<ul>
  <li>Stock Android has built-in USB backup facilities. When USB debugging is enabled, you can use <code>adb backup</code> to backup</li>
  <li>Backup your data on the Google's Servers</li>
  <li>Two backup APIs can also be used,like: <code>Key/Value Backup</code>, <code>Auto Backup for apps</code>.</li>
</ul>
<p><b>Static Analysis</b></p>
<p>Local</p>
<p>Check the AndroidManifest.xml file. If it has <code>android:allowBackup="true"</code> the app allows users to backup data using adb.</p>
<p><small>If the device was encrypted then the device will be encrypted as well</small></p>
<p>If the flag is set true, check if the app stores any sensitive data</p>
<p>Key/Value Backup: To enable key/value backup, you must define a backup agent in the manifest file. Check for <code>android:backupAgent</code></p>

<p><b>Finding Sensitive Information in Auto-Generated Screenshots</b></p>
<p>Manufacturers want to provide device users with a pleasing experience at application startup and exit,
so they introduced the screenshot-saving feature for use when the application is backgrounded. This feature may
pose a security risk. Sensitive data may be exposed if the user deliberately screenshots the application while sensitive
data is displayed. A malicious application that is running on the device and able to continuously capture the screen
may also expose data. Screenshots are written to local storage, from which they may be recovered by a rogue
application (if the device is rooted) or someone who has stolen the device</p>

<p><b>Static Analysis</b></p>
<p>A screenshot of the current activity is taken when an Android app goes into background and displayed for aesthetic
purposes when the app returns to the foreground. However, this may leak sensitive information.</p>
<p>To determine whether the application may expose sensitive information via the app switcher, find out whether the <code>FLAG_SECURE</code> option has been set. You should find something similar to the following code snippet:</p>
<code>getWindow().setFlags(WindowManager.LayoutParams.FLAG_SECURE,WindowManager.LayoutParams.FLAG_SECURE);</code><br>
<code>setContentView(R.layout.activity_main);</code>
<p><en>If the option has not been set, the application is vulnerable to screen capturing.</en></p>
<p><b>Dynamic Analysis</b></p>
<p>While black-box testing the app, navigate to any screen that contains sensitive information and click the home button
to send the app to the background, then press the app switcher button to see the snapshot. If you can clearly see all the contents then the flag isn't set. But if you can't then the flag is set.</p>


<p><b>Checking Memory for Sensitive Data</b></p>
<p>Analyzing memory can help developers identify the root causes of several problems, such as application crashes.
However, it can also be used to access sensitive data.</p>
<p>First identify sensitive information that is stored in memory. Sensitive assets have likely been loaded into memory at
some point. The objective is to verify that this information is exposed as briefly as possible.</p>
<p>To investigate an application's memory, you must first create a memory dump. You can also analyze the memory in
real-time, e.g., via a debugger. Regardless of your approach, memory dumping is a very error-prone process in terms
of verification because each dump contains the output of executed functions. You may miss executing critical
scenarios.</p>
<p><b>Static Analysis</b></p>
<p>For an overview of possible sources of data exposure, check the documentation and identify application components
before you examine the source code. For example, sensitive data from a backend may be in the HTTP client, the XML
parser, etc. You want all these copies to be removed from memory as soon as possible</p>
<p>However, if you need to expose sensitive data in memory, you should make sure that your app is designed to expose
as few data copies as possible as briefly as possible. In other words, you want the handling of sensitive data to be
centralized (i.e., with as few components as possible) and based on primitive, mutable data structures.</p>
<p>Sometimes it'll happen that you delete sensitive data, thinking that you've deleted it from everywhere. But only its reference will have been deleted. It will reside in the memory</p>
<p>This is what happens when you try to delete AES key. Example: </p>
<code>SecretKey secretKey = new SecretKeySpec("key".getBytes(), "AES");</code><br>
<code>secretKey.destroy();</code>
<p>Overwriting the backing byte-array from <code>secretKey.getEncoded</code> won't remove it from the memory</p>
<p><b>Example</b>The RSA key pair is based on the <code>BigInteger</code> type and therefore resides in memory after its first use outside the <code>AndroidKeyStore</code>. Some ciphers like AES <code>Cipher in BouncyCastle</code> do not properly remove their byte-arrays</p>
<p>Some Safe practices are</p>
<ul>
  <li>Try to identify application components and map where data is used.</li>
  <li>Make sure that sensitive data is handled by as few components as possible.</li>
  <li>Make sure that object references are properly removed once the object containing the sensitive data is no longer needed.</li>
  <li>Make sure that garbage collection is requested after references have been removed.</li>
  <li>Make sure that sensitive data gets overwritten as soon as it is no longer needed.</li>
  <li>Don't represent such data with immutable data types (like BigInteger, String) </li>
  <li>Avoid non-primitive data types (like StringBuilder) </li>
  <li>Overwrite references before removing them, outside the finalize method</li>
  <li>Pay attention to third-party components (libraries and frameworks). Public APIs are good indicators.</li>
</ul>
