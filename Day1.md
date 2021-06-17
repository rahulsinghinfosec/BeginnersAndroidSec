<h1>Day 1</h1>
</h3>The basics</h3>
<p><b>Why perform staitic code analysis?</b></p>
<p>When it comes to black box penetration testing, a hacker/pentester will tinker with those functionalities that are visible to him in the environment.
So, there are changes that he/she might skip some core and important functionalities.</p> 
<p>Also a penetration tester will only be able to do assessments and PT as per his/her skill level, as the applications these days are too complex and involve mulitiple
frameworks and dependencies.</p>
<p>So,some misconfigurations and bugs might skip the black box approach. Once the application is deployed and available to the public, some malicious actor might actually
find or come across those misconfigurations and bugs while tinkering with the application.</p>


<p>Advantages of code analysis</p>
<ul>
  <li>In depth analysis of all the core functionalities.</li>
  <li>The presence of harmful functions can be checked.</li>
  <li>The presence of misconfigurations can be checked.</li>
  <li>Helps you enchance your knowlege in Android Security.</li>
</ul>

<p>Which languages can I expect the code to be in? </p>
<ul>
  <li><b>Java</b></li>
  <p>Java was the official language to code in before Kotlin. It has a simple and plain syntax but also can be quite complicated.</p>
  <p>The complexity could be due to constructors, null pointer exceptions, concurrency checked exception,etc.</p>
  
  <li><b>Kotlin</b></li>
  <p>It is not the official language of Android. It was developed by Google, and it is strikingly similar to Java. It runs on the same JVM as Java did.</p>
  <p>Users don't have to worry about null pointer exceptions and other stuff, and no need to end a statement with a semi-colon</p>
  
  <li><b>C++</b></li>
  <p>You can develop Android Apps using C++ but using Android Native Environment</p>
  <p>This is not what Google recommends</p>
  
  <li><b>C#</b></li>
  <p>An android app can also be developed using C#.The syntax is similar to Java, and there are no memeory leaks issue, was it is with C language</p>
  
  <li><b>Python</b></li>
  <p>Though an android phone has a JVM to run the Java byte code, when the application is made to run on a mobile phone, yet you can develop an android app using Python.</p>
  <p>This can be achieved by using tools that convert python apps into Android packages that can run on android devices.</p>
  <p>Example: Kivy</p>
  
  <li><b>Corona</b></li>
  <p>It is a Software Development Kit, that can be used to develop android apps using Lua</p>
  <p>Lua has less functionalities when it comes to comparison with Java, and hence this makes learning Lua easy.</p>
</ul>

<p><b>Back Porting</b></p>
<p>It refers to the act of applying the fix for a current version of software to an older version</p>

<h5>Note</h5>
<ul>
  <li>Runtime</li>
  <p>Runtime provides an environment that converts the code written in high language to be converted to machine level code</p>
  <li>JVM</li>
  <p>It stands for Java Virtual Machine. It is used to run java applications for web, desktop,servers,etc.</p>
  <li>DVM</li>
  <p>It stands for Delvik Virtual Machine. It is a VM that runs the  Delvik bytecode, which is complied from programs written in java.<b>DVM is different from JVM</b></p>
  <p>One of the advantages that DVM has over JVM that it can run on low memory mobile devices and can load faster as compared to a JVM.</p>
  <p>It is also more efficient when it runs mutiple instances on the same device</p>
  <p><b>After android 5.0, DVM was replaced with Android Runtime.</b></p>
</ul>
<p><b>Differences between JVM and DVM</b></p>
<ul>
  <li>JVM is stack base while DVM is register based.
  <li>JVM parses bytecode and converts it to machine code. DVM converts java byte code to Dalvik bytecode and then converts it to machine code.</li>  
  <li>Android was designed to run multiple DVM instances</li>
  <li>So, when you open a new application, a new DVM instance is created with a separate process in the shared memory space and deployes the code to run the application</li>
</ul>
  
<h5>My notes</h5>
<p>I think this is the main reason, why we say that android apps are sandboxed.Beacause a new DVM instance is being launched each time a new application is launched.So one app cannot interfere with the the other app. </p>
