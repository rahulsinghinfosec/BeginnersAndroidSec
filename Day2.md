<h1>Day2</h1>
<small>Reources : Hackerone</small>
<p><b>Types of analysis</b></p>
<ul>
  <li>Dynamic Analysis</li>
  <p>It is used to test the application when the application is running.</p>
  <li>Static Analysis</li>
  <p>It is the testing of application when the application ins't running </p>
</ul>

<p>To prevent static analysis by third party or users (for that matters) the vendors try to obfuscate the code.</p>
<p>This can cause hinderance, but a motivated actor will still find ways to reverse engineer the appliation and do to manipulate the application.</p>

<h3>Some other info</h3>
<ul>
  <li>Hardware</li>
  <p>The main hardware platform for Android is ARM with x86 and x86-64 architectures also supported in the later releases.</p>
  <p>Since Android 5.0 Lollipop, 64-bit variants of all platforms are supported in addition to 32-bit variant.</p>
  <li>Kernel </li>
  <p> Android Kernel is based on Linux Kernel’s Long Term Support (LTS) branch.</p>
  <p>As of 2020, the Kernel version for Linux is 4.4, 4.9 or 4.14</p>
  <li>File System</li>
  <p>Initially it used <b>YAFFS2</b> but after Android v2.3 its started <b>EXT4</b>.There is <b>F2FS</b> file system available and in use by OEM(Original Equipment Manufacturer.</p>
</ul>
<h3>Common Directories</h3>
<p>The following directories are common irrespective of the file system being used</p>
<ul>
  <li>Boot: The partition contains the kernel, ramdisk etc. which is required for the phone to boot when powered on.</li>
  <li>System: Contains OS files which include Android UI and pre-installed apps</li>
  <li>Recovery: Alternative option to booting into OS, allows recovery and backup of partitions.</li>
  <li>Data: Saves user data, apps data, messaging, music etc. Can be traversed through the file browser. This is wiped when the factory reset is pressed. Sub-folders are:</li>
  <ul>
    <li>Android – Default for app cache and saved data.</li>
    <li>Alarms – Custom audio files for alarms.</li>
    <li>Cardboard – Contains data for VR files.</li>
    <li>DCIM – Stores pictures and videos were taken by Camera app.</li>
    <li>Downloads – Stores downloaded files from the internet.</li>
    <li>Notifications – Custom tones for notifications of some apps.</li>
    <li>Music, Movies – Default folders to store songs and videos from third-party apps.</li>
    <li>Pictures – Default folder to store pictures taken by third-party apps.</li>
    <li>Podcasts – Stores podcasts files when you use a podcast app.</li>
    <li>Videos – Stores downloaded videos from third-party apps.</li>
  </ul>
  <li>Cache: Storage of frequently used data and app components.</li>
  <li>Misc: Contains other important system setting information. Like USB config, carrier ID.</li>
</ul>

<p><b>Android Architecture</b></p>
<p>The layers (from top to bottom) are </p>
<ol>
  <li>System Apps (Email, Message,etc)</li>
  <li>Java API Framework </li>
  <li>Native C/C++ and Android Runtime</li>
  <li>Hardware Abstraction Layer (HAL)</li>
  <li>Linux Kernel</li>
 </ol>
 <p><b>Android Runtime</b></p>
 <p>A runtime environment is a state in which program can send instructions to the computer’s processor and access the computer’s RAM. Android apps programmed in (for example) Java, will be first converted to byte code during compilation packaged as an APK and run-on runtime.</p>
 <p>ART replaced DVM, and hence added a few benefit as listed</p>
 <p>DVM used JIT(just in time) compilation which meant that the code was taken at the runtime, complied and executed.</p>
 <p>ART uses AOT (ahead of time) compilation that compiles .dex files (bytecode) even before they are needed. This is done during installation and stored in phone storage.</p>
 <p><b>To be noted: After Android N, JIT compilation was reintroduced along with AOT and an interpreter in ART making it hybrid to tackle against problems like installation time and memory. (From Hackingarticles.in)</b></p>
 
 <p><b>Compilation and De-compilation</b></p>
 <p>Compilation : It works as follows</p>
<ul>
  <li>Code written in main.java</li>
  <li>Code compiled and converted to byte code (using java compiler=javac). Final output = main.class</li>
  <li>JVM converts the byte code to the machine code using JIT(or AOT)</li>
  <li>Machine code is run by the CPU</li>
</ul>
<p><b>JVM doesn't work with limited Memory and CPU, so DVM was introducted. First the byte code is converted to .dex file and then that file is taken by DVM(now ART) and converted to machine code using JIT/AOT compilation.</b></p>

<p>Decompiling</p>
<p>An .apk file is just a zipped file containing xml files,dex code,resource files,and other files</p>
<p>It can be decomplied using unzip command : <b>unzip &lt;file_name&gt;.apk</b></p>
<p><b>OR</b> Make use of apktool</p>
<p><b>apktool -d -rs &lt;file_name&gt;.apk</b></p>
<hr>
<p>apktool</p>
<p>It is a tool for reverse engineering 3rd party, closed, binary Android apps. It can decode resources to nearly original form and rebuild them after making some modifications; it makes possible to debug smali code step by step.</p>
<hr>
<p>As we know, that .dex file is created (in one of the steps, during compilation). So, we convert it to standard file using <b>d2j-dex2jar classes.dex</b>, where classes.dex is the dex file found after unzipping the .apk file.</p
<p>This creates a <b>classes-dex2jar.jar</b> file. Now all we have to do is to decompile the source code. <br> This can be done using <b>Jd-gui classes-dex2jar</b></p>
<p><b>NOTE:</b>If the obfuscator isn't used then the code will be readable</p>
  
  
<p><b>What you can exptect after the decompilation?</b></p>
<p>An android application contain the essential (essential for running of the application) and the non-essential files</p>
<p><b>Essential</b></p>
<ul>
  <li>Activities</li>
  <li>UI</li>
  <li>Intent</li>
</ul>
<p><b>Might be present(Non-essential)</b></p>
<ul>
  <li>Service</li>
  <li>Content Providers</li>
  <li>Broadcast</li>
  <li>Receivers</li>
</ul>

<p><b>What to expect in a *.apk file.</b></p>
<p>An apk file is just a zipped file. You can expect the following files within it.</p>
<p>myapp.apk</p>
<ul>
  <li>AndroidManifest.xml</li>
<li>META-INF/</li>
<li>classes.dex</li>
<li>lib/</li>
<li>res/</li>
<li>resources.arsc</li>
</ul>

<ol>
  <li>AndroidManifest.xml</li>
  <p>This is a compressed version of the AndroidManifest.xml file which contains all of the basic application information such as the package name, package version, externally accessibly activities and services, minimum device version, and more. The compressed version of this file is not humanly readable, but there are a couple of tools that are able to uncompress it, most notably being apktool.</p>
  <p>Note: If you use <b>unzip</b> to decompress the *.apk file, the AndroidManifest.xml file will be binary xml format. Which you cannot read. If you use <b>apktool</b> to decompress, then you can view the AndroidManifest.xml file in xml format</p>
  <li>META-INF/</li>
  <p>Consider it a record/document that stores all the metadata of the files of the application. This could include the developer certificate and the checksums of all the files. If you make any modifications on the any of the files and do not re-sign this, you'll get an error while installing it. This is because checksums are based on the file (contents). When the OS will compute the checksum and compare it with the one present in this folder, it won't match. Hence, this will result in an error.</p>
  <li>classes.dex</li>
  <p>This contains the bytecode. Gererally the apps will have one .dex file, but there could be many in some apps. We decompile it to java source code. It can be done using dex2jar.</p>
  <li>resources.arsc</li>
  <p>It is also stored in a binary format. apktool can be used to convert it to human readable format. It contains metadata about the resources and the xml nodes of the compiled files like XML Layout files, drawables,strings and more. It also contains information about their attributes (like width, position, etc) and the resource IDs, which are used globally by both Java and XML app files in the app.</p>
  <li>res/</li>
  <p>It contains compressed binary xml versions of the resources xml files that are paired with resources.arsc </p>
  <li>lib/</li>
<p>Not all Android apps contain a lib/ folder, but any app with native C++ libraries will. Within this folder, you will find different folders per-architecture, each one containing .so files specifically compiled for that target architecture such as “armeabi-v7a” and “x86”.</p>
</ol>
