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

