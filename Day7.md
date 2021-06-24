<h1>Day 7</h1>
<p>Public data should be available to everyone, but sensitive and private data must be protected, or, better yet, kept out of device storage.</p>
<p>Next to protecting sensitive data, you need to ensure that data read from any storage source is validated and possibly sanitized.</p>
<p><b>Testing Local Storage for Sensitive Data</b></p>
<ul>
  <li>Asking a complex password each time a uses an app, isn't a feasible option. So, it uses tokens/session id's. They are stored in the internal local storage.</li>
  <li>It becomes necessary to ensure that they don't have PII(Personal Identifiable Information)</li>
  <li>Sensitive data is vulnerable when it is not properly protected by the app that is persistently storing it.</li>
  <li>The app may be able to store the data in several places, for example, on the device or on an external SD card</li>
  <li>A lot of information may be processed and stored in different locations.</li>
  <li>Such disclosed information can have many consequences.Including social enginnering.</li>
</ul>
<p>Storing data is essential for mobile apps. Following is the list of storage techniques that can be chosen to store persistent data.</p>
<ul>
  <li>Shared Preference</li>
  <li>SQLite Database</li>
  <li>Realm Database</li>
  <li>Internal Database</li>
  <li>External Database</li>
</ul>

<p><b>Shared Preference</b></p>
<p>The SharedPreferences API is commonly used to permanently save small collections of key-value pairs. Data stored
in a SharedPreferences object is written to a plain-text XML file. The SharedPreferences object can be declared
world-readable (accessible to all apps) or private. Misuse of the SharedPreferences API can often lead to exposure of
sensitive data. </p>
<code>SharedPreferences sharedPref = getSharedPreferences("key", MODE_WORLD_READABLE);</code><br>
  <code>SharedPreferences.Editor editor = sharedPref.edit(); </code><br>
  <code>editor.putString("username", "administrator");</code><br>
  <code>editor.putString("password", "supersecret"); </code><br>
  <code>editor.commit(); </code>
  
<p>Once the activity has been called, the file key.xml will be created with the provided data. This code violates several
best practices.For example</p>
<ul>
  <li>The username and password are stored in clear text in<code> /data/data/<package-name>/shared_prefs/key.xml</code></li>
  <li><code>MODE_WORLD_READABLE</code> allows all applications to access and read the contents of key.xml. <b>MODE_WORLD_READABLE/WRITABLE were depriciated with API 17. Older versions may however be vulnerable to this.</b></li>
</ul>
<p><b>SQLite Database (Unencrypted)</b></p>
<ul>
  <li>SQLite is an SQL database engine that stores data in .db files. The Android SDK has built-in support for SQLite databases. The main package used to manage the databases is<code> android.database.sqlite</code>.</li>
  <code>SQLiteDatabase notSoSecure = openOrCreateDatabase("privateNotSoSecure",MODE_PRIVATE,null); </code><br>
  <code>notSoSecure.execSQL("CREATE TABLE IF NOT EXISTS Accounts(Username VARCHAR, Password VARCHAR);"); </code><br>
  <code>notSoSecure.execSQL("INSERT INTO Accounts VALUES('admin','AdminPass');"); </code><br>
  <code>notSoSecure.close();</code>
  <li>Once the activity has been called, the database file stored in the clear text file <code>privateNotSoSecure</code> will be created with the provided data and <code>/data/data/<package-name>/databases/privateNotSoSecure.</code> </li>
  <li>Sensitive information should not be stored in unencrypted SQLite databases.</li>
</ul>
<p><b>SQLite Databases (Encrypted)</b></p>
<ul>
  <li>With the library SQLCipher, SQLite databases can be password-encrypted.</li>
  <code>SQLiteDatabase secureDB = SQLiteDatabase.openOrCreateDatabase(database, "password123", null);</code><br>
   <code> secureDB.execSQL("CREATE TABLE IF NOT EXISTS Accounts(Username VARCHAR,Password VARCHAR);"); </code><br>
  <Code>secureDB.execSQL("INSERT INTO Accounts VALUES('admin','AdminPassEnc');"); </code><br>
   <code> secureDB.close();</code>
  <li>If encrypted SQLite databases are used, determine whether the password is hard-coded in the source, stored in shared preferences, or hidden somewhere else in the code or filesystem<li>
  <li>Secure ways to retrieve keys include: </li>
  <ol>
    <li>sking the user to decrypt the database with a PIN or password once the app is opened (weak passwords and PINs are vulnerable to brute force attacks)</li>
    <li>Storing the key on the server and allowing it to be accessed from a web service only (so that the app can be used only when the device is online) </li>
  </ol>
</ul>
<p><b>Firebase Real-time Databases</b></p>
<p>Firebase is a development platform with more than 15 products, and one of them is Firebase Real-time Database. It
 can be leveraged by application developers to store and sync data with a NoSQL cloud-hosted database. The data is
stored as JSON and is synchronized in real-time to every connected client and also remains available even when the
application goes offline.</p>
 <p>However it is prone to misconfigurations</p>
 <p>he misconfigured Firebase instance can be identified by making the following network call:<br> https://\<firebaseProjectName\>.firebaseio.com/.json</p>
  <p>The firebaseProjectName can be retrieved from the mobile application by reverse engineering the application.<br> Alternatively, the analysts can use Firebase Scanner, a python script that automates the task above as shown below:</p>
   <code>python FirebaseScanner.py -p <pathOfAPKFile></code> <br>
   <code>python FirebaseScanner.py -f <commaSeperatedFirebaseProjectName></code><br>  
<p><b>Realm Databases</b></p>    
<p>The Realm Database for Java is becoming more and more popular among developers. The database and its contents can be encrypted with a key stored in the configuration file.</p>     
<code>//the getKey() method either gets the key from the server or from a KeyStore, or is deferred from a password.</code>
    <code>RealmConfiguration config = new RealmConfiguration.Builder()</code> <br>
    <code>.encryptionKey(getKey())</code><br>
    <code>.build();</code><br>
    <code>Realm realm = Realm.getInstance(config);</code><br>
    <p>If the database is not encrypted, you should be able to obtain the data. If the database is encrypted, determine whether the key is hard-coded in the source or resources and whether it is stored unprotected in shared preferences or some other location.</p>
    
<p><b>Internal Storage</b></p>
    <p>You can save files to the device's internal storage. 
    Files saved to internal storage are containerized by default and cannot be accessed by other apps on the device. When the user uninstalls your app, these files are removed. The following code would persistently store sensitive data to internal storage:</p>
    <code>FileOutputStream fos = null;</code>
<code>try { </code>
<code>fos = openFileOutput(FILENAME, Context.MODE_PRIVATE);</code><br>
<code>fos.write(test.getBytes());</code><br>
<code>fos.close();</code><br>
<code>} catch (FileNotFoundException e) {</code><br>
<code>e.printStackTrace();</code><br>
<code>} catch (IOException e) {</code><br>
<code>e.printStackTrace();</code><br>
<code>}</code>
    
<p>Search for the class <code>FileInputStream</code> to find out which files are opened and read within the app.</p>
<p><b>External Password</b></p>
<p>Every Android-compatible device supports shared external storage. This storage may be removable (such as an SD card) or internal (non-removable). Files saved to external storage are world-readable. The user can modify them when USB mass storage is enabled. You can use the following code to persistently store sensitive information to external
storage as the contents of the file password.txt :</p>

<code>File file = new File (Environment.getExternalFilesDir(), "password.txt");String password = "SecretPassword";</code><br>
<code>String password = "SecretPassword";</code><br>
<code>FileOutputStream fos;</code><br>
<code>fos = new FileOutputStream(file);</code><br>
<code>fos.write(password.getBytes());</code><br>
<code>fos.close();</code>
<ul>
<li>The file will be created and the data will be stored in a clear text file in external storage once the activity has been called.</li>
<li>It's also worth knowing that files stored outside the application folder <code>(data/data/<package-name>/)</code> will not be deleted when the user uninstalls the application.</li>
</ul>


    
    
