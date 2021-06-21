<h1>Penetration Testing</h1>
<p>The following points describe the general testing process.</p>
<ul>
  <li><b>Prepration</b>: defining the scope of security testing, including identifying applicable security controls, the organization's testing goals, and sensitive data.</li>
  <li><b>Intelligence Gathering</b>:analyzing the environmental and architectural context of the app to gain a general contextual understanding.</li>
  <li><b>Mapping the application</b>: This phase is an addon to the pervious phase. You get the through understanding of the app, its entry points, the data it holds, and the main potential vuln,and towards the end you generate a couple of test cases. These can be used in the next phase.</li>
  <li><b>Exploitation</b>: In this phase the tester tries to exploit the vulnerabilities found in the previous phase (Mapping the application/Vulnerability Assessment). This phase is necessary to rule out false positives.</li>
  <li><b>Reporting</b>: This part is always present towards the end. Be is web applicaion or mobile application pentesting.The tester makes a formal report to explain how he found the vulnerabilites,and a PoC script/video/image,etc.</li>
</ul>

  
<p><b>Identifying Senstive Data</b></p>
<p>Classification of the sensitivity of the data differs by industry and country</p>
<p>The three general states in which the data is accessible is </p>
<ul>
  <li><b>At rest</b>: The data is sitting on a file or data storage</li>
  <li><b>In use</b> : The application has loaded the data in its address space</li>
  <li><b>In transit</b>: The data is in motion and is in transit between the app and the endpoint or the communicating process(in the mobile itself)</li>
</ul>

<p>What you might want to look for : </p>
<ul>
  <li>User authentication information (creds, PIN)</li>
  <li>Personal Identifiable Information (PII) that can be abused for identy theft. Example: Social security number, credit card, bank account,etc.</li>
  <li>Devide identifiers that may identify a person</li>
  <li>Any data whose protection is a legal obligation</li>
  <li>Any other data whose exposure could lead to financial harm or reputation harm.</li>
</ul>

<p><b>Intelligence Gathering</b><p>
<p>Environment Information <br> This could include company's goals with the app. What type of company it is,etc. </p>
<p>Architecture Information</p>
<ul>
<li>The mobile app : How the app access the data and manages it. How it communicates with other process, maintains user sessions, etc. How it reacts to jailbroken or rooted devices.<li>
<li>The OS : The Operating system and its version that the app runs on.</li>
<li>The networks: Whether it uses encryption (eg TLS) while transferring data. Tik-tok used HTTP for quite a while, after its first release.</li>
<li>Remote Services : The remote services that the app consumes and wheter the compromise of the remote service will result in the compromise of the app itself.</li>
</ul>

<p><b>Authentication Schemes</b></p>
<p>Authentication can be provided by vairous factors. This could be with, someting that a user knows (username/password), something that a user is (biometrics), something that a user has (simcard,etc)</p>
<p>Based on the app type, it also should follow the standards that it falls into. For example, a payment app should follow PCI DSS standard.</p>
<p>Here are some of the guidelines for the <b>non-sensitive apps("level 1")</b></p>
<ul>
  <li>If the app provides user with remote services, than the authentication should be done at the remote end.</li>
  <li>A password policy exists and is checked at the remote end.</li>
  <li>The remote endpoint blocks the account (temporarily) if the number of attemps exceed a particular value.</li>
</ul>
<p>For <b>Sensitive ("Level 2")</b> apps</p>
<ul>
  <li>A second factor of authentication exists.</li>
  <li>The app informs the user with his recent activities in when they logged in.</li>
  <li>Step-up authentication is required to enable the actions when dealing with sensitive data/transactions.</li>
</ul>

<p><b>Stateful vs Stateless Authentication</b></p>
<ul>
  <li>Stateful Authentication</li>
  <p>You might still find HTTP being run as an application protocol. HTTP in itself is a stateless protocol. So, in order to maintain statefulness, the server provides the client with a session id. This session id then servers as a reference to the subsequent requests. But the drawback is that server has to maintain a server state till the user doesn't log out or the session id exipres. The session id is <b>opaque</b>.It doesn't leak any sensitive information</p>
  <li>Stateless Authentication</li>
  <p>In Stateless auth model, there is no involvement of a session id. The user info is stored as a token on the client side and then passed to the server. This eliminates the need to maintain a server state.</p>
</ul>
