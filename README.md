<h1 style="color:red ; ">Task 2 :Web Application Analysis with Burp Suite</h1>

| Summited By                     |  Summited to           |
|:--------------------------------| :----------------------|
| Name : SImol bk                 | Name : Niraj Adhikari  | 
| Email : Simon.bk.088@gmail.com  | 



# Table of Contents

 - [Objective](#objective)
 - [Tools Used](#tools+used)
 - [What is Burp Suite?](#what-is-burp-suite)
 - [Installation Process](#installation-process)
 - [Configuring Burp Suite in Browser](#configuring-burp-suite-in-browser)
 - [Using Burp Suite Repeater Tab for Cross-Site Scripting (XSS) Vulnerability](#using-burp-suite-repeater-tab-for-cross-site-scripting-xss-vulnerability)
 - [Using Burp Suite Intruder Tab for Brute Force](#using-burp-suite-intruder-tab-for-brute-force)
 - [Using Comparer Tab to Analyze Brute Force Attack](#using-comparer-tab-to-analyze-brute-force-attack)
 - [Using Decoder Tab to Decode and Encode Values](#using-decoder-tab-to-decode-and-encode-values)
 - [Using Sequencer in Burp Suite](#using-sequencer-in-burp-suite)
 - [Conclusion](#conclusion)
  
 # Objective:
 This assignment aims to provide hands-on experience with Burp Suite, enabling you to analyze and modify web requests to observe their impact and deepen your understanding of web security testing. Through practical exercises, you'll gain valuable skills in identifying and exploiting vulnerabilities in web applications.

 # Tools used :
 - Tool = Burp suit- Community addition
 - Environment = Kali Linux in (NAT Network Adapter)
   
 # What is Burpsuite?
 BurpSuit is a platform which is developed by PortSwigger for web application security testing. This tool is widely by security researcher, pentester, ect.The tool helps identify vulnerabilities such as SQL injection, cross-site scripting (XSS), and other web-based security issues.

## Installation process (https://portswigger.net/burp/communitydownload.) 
Make sure you have Java 21 or later installed on your computer. For Windows, run the .exe file and follow the simple setup wizard. On macOS, open the .dmg file and drag Burp Suite to your Applications folder. For Linux, make the .sh file executable and run it from the terminal. Once installed, launch Burp Suite, set your browser to use its proxy (usually 127.0.0.1:8080), and install the Burp CA certificate to handle HTTPS traffic.

# Configuring BurpSuite in browser :
## Step 1 : Lunching BurpSuit 
1. Opening Brup suit in Kali linux.
2. Selecting Next, then Start Burp to open the main interface.
   
<img width="1360" height="652" alt="Screenshot_2025-10-15_04_18_40" src="https://github.com/user-attachments/assets/94f22aac-fab9-4432-a841-12dd7b123625" />
<img width="1366" height="768" alt="Screenshot_2025-10-15_04_05_40" src="https://github.com/user-attachments/assets/2b24d087-9af6-4036-bb8e-576f43331462" />

## Step 2 : Configuring Browser Proxy:
1. Open Firefox, go to Settings > General > Network Settings (scroll to the bottom) > Settings.
2. Select Manual proxy configuration.
3. Enter HTTP Proxy: 127.0.0.1 and Port: 8080 and tick mark HTTPS .
4.  Click OK.
   
<img width="1366" height="768" alt="Setting proxy in browser" src="https://github.com/user-attachments/assets/5ef0701a-9238-4713-84e9-ac2cc5cb347f" />

## Step 3: Installing Burp’s CA Certificate for HTTPS
1. Lunch Brup suit and Go to setting
2. Select `import/export burpsuit CA Certificate`
3. Select `.dre` format in Export section and click next.
<img width="1366" height="768" alt="Exporting cert form brupsuit" src="https://github.com/user-attachments/assets/845eb1e2-0071-47c0-b2db-e08490f18b13" />

4. Select the path to export the `.dre` format CA Certificate. 

<img width="1366" height="768" alt="Exported cer" src="https://github.com/user-attachments/assets/a32e299c-b9e4-4be6-b477-c4ff9d1d65e6" />

5. Go to Settings > Privacy & Security > Certificates > View Certificates > Authorities tab > Import.
6. Select the `burpsuit cer.dre` file and check Trust this CA to identify websites.
<!-- <img width="1366" height="768" alt="importing cert in browsrt" src="https://github.com/user-attachments/assets/911529b2-83f2-400c-88c8-9e0ec2db8747" /> -->
7.  Tick all the option that shown while importing.

<img width="1366" height="768" alt="imorting cer" src="https://github.com/user-attachments/assets/48f89567-f8f3-448b-9a40-37fb8b9b397c" />

8. Conform the cretificate in Authorities tab.
    
<img width="1366" height="768" alt="Conformaing cert " src="https://github.com/user-attachments/assets/54159938-1eaf-4be7-b3d2-e65e29244219" />

# Using BurpSuit Repeater tab for Cross-Site Scripting (XSS) vulnerability  

A reflected cross-site scripting (XSS) vulnerability was identified in the search functionality of the `testphp.vulnweb.com` application, specifically in the `/search.php` endpoint. This POC demonstrates how Burp Suite can be used to intercept and modify the request to inject and execute arbitrary JavaScript code in the browser.

## Step taken 
1. Navigate to the Site:
- Open http://testphp.vulnweb.com/ in your proxied browser.
  
  <img width="1366" height="768" alt="Target Website" src="https://github.com/user-attachments/assets/3bc5e808-31ea-4b47-a5cc-3ac97bc1346d" />

2. Submit a Normal Search:
- Enter "batman" in the search field and click "go". And intercepting in the proxy tab in Brupsuit.
  <img width="1366" height="768" alt="Screenshot_2025-10-15_06_36_10" src="https://github.com/user-attachments/assets/2521eb5c-41ad-4b7f-850e-13965cff3262" />

3. Intercept and sending to Repeater Tab:
- Repeat the search but with intercept enabled. In Burp's Intercept tab and send to Repeater, 
<img width="1366" height="768" alt="2" src="https://github.com/user-attachments/assets/aaf1d9fb-e813-4131-8dac-32c3b6844cda" />
4. Checking the Input:
- After sending to repearet tab checking the input in respond tab.
<img width="1366" height="768" alt="3" src="https://github.com/user-attachments/assets/90c5a0dd-2c7a-471a-994e-9a49bdaa628f" />
  
5. Modifying the Request:
- Modify the searchFor parameter to the XSS payload: `<script>alert('batman')</script>`.The modified request body becomes: `searchFor=%3Cscript%3Ealert(%27batman%27)%3C%2Fscript%3E&goButton=go`.
<img width="1366" height="768" alt="5" src="https://github.com/user-attachments/assets/65333137-61d5-46d0-8c9c-5d3ed2061058" />

6. Forward the Request:
- Forward the modified request and switch to the browser. The response will reflect the payload, causing the browser to execute the script.
7. Observe the Execution:
- A JavaScript alert box pops up with the message "batman", confirming successful XSS execution.
<img width="1366" height="768" alt="6" src="https://github.com/user-attachments/assets/54cb0680-5c39-44ec-a26b-8670dbcc45a6" />

# Using Burpsuit intruder tab for Brute Force

 Burp Suite's Intruder tab was used to target the pass parameter while keeping the uname fixed as "test". A simple list of common passwords was tested, successfully identifying the correct password "test" based on response differences (e.g., HTTP status code changing from 302 to 200 upon success).

## Step taken
1. Navigate to the Site:
   - Open `http://testphp.vulnweb.com/` and attempt a login via the "Your profile", which us a a login form (intercepted as POST to /userinfo.php)
     
2. Summit a paramater:
   - In `http://testphp.vulnweb.com/` summit a simple paramater in username and password and intercept in Burpsuit.
     
3. Send to Intruder:
   - Right-click the request in the Proxy history and send it to Intruder.
     
4. Configure Positions:
   - In the Positions tab, set attack type to "Sniper Attack, Battering Ram Attack, Pitchfork Attack, or Cluster Boom attack ". Clear all positions and mark only the pass value with `§` delimiters.
     
5. Configure Payloads:
   - In the Payloads tab, select "Simple list" and load a list of passwords (e.g., from a wordlist file or manually add entries like "password", "123456", "test").
   - Add second payload as needed in other type of attack.
     
6. Start the Attack:
   - Launch the attack and observe results. Look for anomalies like status code changes (302 for failure, 200 for success) or response length differences.
     
7. Verify Success:
   -  A successful login (e.g., with `pass=123456`) will return a 200 status and display user information in the response.

# Proof of Concept of Snipe attack Screenshots
1. Intruder Payloads Configuration: Sniper attack setup with password list.
<img width="1366" height="768" alt="1" src="https://github.com/user-attachments/assets/39532fdb-aa7e-45ec-90c2-7d1a8d8071d2" />

2. Intruder Attack Results: Successful payload ("test") with status 200.
<img width="1366" height="768" alt="2" src="https://github.com/user-attachments/assets/05235ee8-48ff-4404-ab06-bf6197edb088" />

3. Successful Login Page: Browser view after brute force success.
   <img width="1366" height="768" alt="3" src="https://github.com/user-attachments/assets/7bc98f67-7fc3-4fcb-84eb-ad808585b01d" />

# Proof of Concept of Battering Ram Attack: 

1. Intruder Payloads Configuration: Battering Ram attack setup with password list.
<img width="1366" height="768" alt="1" src="https://github.com/user-attachments/assets/c044dee5-9171-46b9-af7d-fcc9f58050c9" />

2. Intruder Attack Results: Successful payload ("test") with status 200.
<img width="1366" height="768" alt="2" src="https://github.com/user-attachments/assets/f870de2d-2b15-4f9b-8ee0-37dc8b6269ed" />

3. Successful Login Page: Browser view after brute force success.
 <img width="1366" height="768" alt="3" src="https://github.com/user-attachments/assets/7bc98f67-7fc3-4fcb-84eb-ad808585b01d" />

# Proof of Concept of Pitchfork Attack:

1. Intruder Payloads Configuration: Pitchfork attack setup with password list.
<img width="1366" height="768" alt="1" src="https://github.com/user-attachments/assets/fa4c7174-f35e-417a-9baf-88df08ddc104" />

2. Intruder Attack Results: Successful payload ("test") with status 200.
<img width="1366" height="768" alt="2" src="https://github.com/user-attachments/assets/90690f02-2f44-40ac-bbab-8633f7e1d00a" />

3. Successful Login Page: Browser view after brute force success
<img width="1366" height="768" alt="3" src="https://github.com/user-attachments/assets/ce4cf011-9a55-46ed-b8ef-9e534516f677" />

# Proof of Concept of Cluster Boom Attack:

1. Intruder Payloads Configuration: Pitchfork attack setup with password list.
<img width="1366" height="768" alt="1" src="https://github.com/user-attachments/assets/17cffc23-9da4-4484-835b-98e30ad02338" />
   
2. Intruder Attack Results: Successful payload ("test") with status 200.
<img width="1366" height="768" alt="2" src="https://github.com/user-attachments/assets/3266950d-591b-4dfd-bd21-deaa8c5c88d5" />

3. Successful Login Page: Browser view after brute force success
<img width="1366" height="768" alt="3" src="https://github.com/user-attachments/assets/ce4cf011-9a55-46ed-b8ef-9e534516f677" />

# Using Comparer tab to analysis Brutforce attack

1. Analyze Results and Send to Comperer Tab: 
   - In the Intruder results tab, select a failed response (e.g., pass=wrong, 302 status) and a successful response (e.g., pass=test, 200 status) and sent it to Compere tab.
<img width="1366" height="768" alt="Screenshot_2025-10-16_04_01_30" src="https://github.com/user-attachments/assets/556688d8-bf43-4edc-b930-99c2a5ef6d9d" />


2. Word compare:
  - After sending to comparer tab click `words` and analysis the result.
<img width="1366" height="768" alt="1" src="https://github.com/user-attachments/assets/2eebd4a2-3ce4-464b-ab19-e615f0bd5f42" />


3. Bytes compare:
   - And also analyzing the result in `bytes` format.
<img width="1366" height="768" alt="Bytes" src="https://github.com/user-attachments/assets/7477d657-229d-46f9-9937-9208c1318f19" />

# Using Decoder tab to Decode and encode the value : 

The Decoder tab in Burp Suite is used to manually encode, decode, and hash data (e.g., Base64, Hex, MD5) to analyze and manipulate web application inputs/outputs, helping identify obfuscated content, test security vulnerabilities, or prepare payloads for penetration testing.

## Step 1 :
   - Sending encrypted value in decoder to analyze and encode the value.
<img width="1364" height="656" alt="Base64_1" src="https://github.com/user-attachments/assets/ba9e38ef-8f7d-47b4-b4a6-b656eb042764" />
     
## Step 2 : 
   - Analysing the result.
<img width="1364" height="656" alt="Base64_2" src="https://github.com/user-attachments/assets/e05652d9-7ecf-4b88-85ae-24eeeaffb233" />

## Step 3 :
  - In right side of Decoder tab manually choosing the type to of encoding or decoding as the type of the value or using smart decode.
  - In this case I have re-encodes by changing the value in `url format` 
<img width="1364" height="656" alt="url_3" src="https://github.com/user-attachments/assets/d62fb612-b522-41ef-9e27-b3e3b689c7d7" />

## Step 4 : 
  - And at the last I have decoder the re-encoded to analyzethe result.
<img width="1364" height="656" alt="url_4" src="https://github.com/user-attachments/assets/51bd4b3b-c57f-41d2-aeb4-9d614d628802" />

# Using Sequencer in Burpsuite :
The Sequencer tab in Burp Suite is used to analyze the randomness and predictability of session tokens or other critical data, helping to identify weak or insecure token generation processes that could be exploited in session hijacking or authentication attacks.

## Step 1 : 
   - Intercepting the log in request from `GinandJuice.Shop/login` in burpsuite to capture the `Cookie`.
   - We see the `Cookie: AWSALB=WCzpnf72kTBOp+BwIbL4uPt5ohWN/i015oG15mKuVq7+TDfZRVXImRCANi5Pi6Fk2EUadGueneB668TR3h4IsfRMnovilKTn+PZn6X96ceLWoJbPKuMxfqYmGI6Q;` in our proxy tab.
<img width="1366" height="768" alt="1" src="https://github.com/user-attachments/assets/416ca2d6-90e6-48c3-8054-07d28a2828ec" />

## Step 2 : 
   - After capturing the request I send it to the `Sequencer tab` and select `Cookie` in the sequencer.
<img width="1366" height="768" alt="2" src="https://github.com/user-attachments/assets/0aac54bf-f404-4ae0-827f-951c4481d7c6" />

## Step 3 :
  - And I started live capture.
<img width="1366" height="768" alt="3" src="https://github.com/user-attachments/assets/3348235e-cec8-418b-a424-db13c774071b" />

## Step 4 :
   - After the capture is complete I click on `analyze now` to analyze the report.
   - As per OWASP Session id length Session identifiers must have at least 64 bits of entropy to prevent brute-force session guessing attacks. (https://owasp.org/www-community/vulnerabilities/Insufficient_Session-ID_Length)
   - In this websit the length of session it is 674 bits which conclude that the site is not Vulnerable with brute-force session guessing attacks.
<img width="1366" height="768" alt="4" src="https://github.com/user-attachments/assets/62db1894-1496-404a-8d29-fded69c11490" />
<img width="1366" height="206" alt="4 1" src="https://github.com/user-attachments/assets/62335414-6359-45ba-accb-a00b23c2e536" />

### Step 4.1 :
    - Report for Character-level analysis.
<img width="1366" height="768" alt="4 2" src="https://github.com/user-attachments/assets/d0782a46-69fc-459a-9407-53ae23affa0a" />

### Step 4.2 :
    - Report for Bit-Level analysis.
 <img width="1366" height="768" alt="4 3" src="https://github.com/user-attachments/assets/b6e988c1-0ff3-4ccc-a17e-3cdfc48ae084" />

# Conclusion
This hands-on Burp Suite exercise on Kali Linux illuminated key web security testing techniques, successfully exploiting a reflected XSS vulnerability on testphp.vulnweb.com via the Repeater tab by injecting JavaScript payloads, and brute-forcing weak login credentials ("test") using Intruder's Sniper, Battering Ram, Pitchfork, and Cluster Bomb attacks, with Comparer revealing response differences like 302-to-200 status shifts. Decoder enabled efficient payload encoding/decoding for evasion testing, while Sequencer analysis of GinandJuice.Shop cookies confirmed robust 674-bit entropy, exceeding OWASP's 64-bit threshold against session guessing.





 
















