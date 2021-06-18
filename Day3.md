<h1>Day3</h1>
<p><small>Reference: Hacking Articles</small></p>
<p><b>Activity</b></p>
<ul>
<li>It is a class in Android which, when implemented, provides the user with a screen with a user interface</li>
<li>When a user first opens the app, he's displayed with a default screen. It's a part of <em>MainActivity</em> </li>
<li>All the actions perfromed in Activity pages are done using callbacks.</li>
<li>You might find these 7 callbacks</li>
<ul>
  <li>onCreate()</li>
  <li>onStart()</li>
  <li>onPause()</li>
  <li>onResume()</li>
  <li>onStop()</li>
  <li>onDestroy()</li>
  <li>onRestart()</li>
</ul>
</ul>
<p><b>Services</b></p>
<p>A service is a component that runs in the background to perform long-running operations without needing to interact with the user and it works even if application is destroyed.</p>
<p>A service can take two states</p>
<ul>
<li>Started</li>
<li>Bound</li>
</ul>
<p><b>Broadcast Receivers</b></p>
<p>They respond to broadcast messages originating from other applications or within the system itself. <br>Why is it necessary? This is necessary beacuse, this can initiate a broadcast when it performs some actions. The event could be as simple as downloading an image,etc.</p>

<h3>Mobile App Taxonomy</h3>
<p><b>Native Apps</b></p>
<p>These are apps specifically bulit for the OS, therefore harnessing their power in the most efficient way. The OS provides with SDK through which these apps can be developed. They have the capability to provide the best performence and high degree of reliability.</p>
<p>The problem creeps in when the company has to main 2 different code bases for 2 apps(Android and iOS). This becomes a huge problem when the application at hand was made to perform complex tasks</p>

<p><b>Web Apps</b></p>
<p>The problem of having to maintain different code bases and having differnet development team can be solved using this approach.</p>
<p>Basically they are websites made to look like native apps. They run on a browser and run within the confinements of a browser(sandboxed). Hence they can have performance issues. They are typically built on HTML5. They can have an icon, but in browser's analogy they can be compared to bookmarks (saved on your home screen). An example could be Amazon's India web app.</p>
<p>This brings in reduced development costs.A web file update can serve as an update to the web app as well.</p>

<p><b>Hybrid Apps</b></p>
<p>They aim to fill in the gap between the native and the web apps. A major part of the app relies on the web browser (webview) for execution.</p>
<p>The web-to-native abstraction layer enables access to the device capabilities not accessible over the pure web app. </p>
<p>Some of the popular frameworks that can be used to develop hybrid apps</p>
<ul>
  <li>Apache Cordova</li>
  <li>Google Flutter</li>
  <li>jQuery Mobile</li>
  <li>Native Script</li>
  <li>React Native</li>
<ul>
<p><b>Progresive Web App</b></p>
<p>These are like traditional web apps, with some addtional features. Like, its possible to work offline (which isn't possible on a web app) and access to mobile device hardware is possible </p>
<p>Progressive Web Apps are both available on Android and iOS but not all hardware is available yet</p>
  
