[Table of content]
  
  
  <h1 style="text-align:center;">Task 2 :Web Application Analysis with Burp Suite</h1>

  # Objective:
 This assignment aims to provide hands-on experience with Burp Suite, enabling you to analyze and modify web requests to observe their impact and deepen your understanding of web security testing. Through practical exercises, you'll gain valuable skills in identifying and exploiting vulnerabilities in web applications.

 # Tools used :
 - Tool = Burp suit- Community addition
 - Environment = Kali Linux in (NAT Network Adapter)
 # What is Burp suit?
 BurpSuit is a platform which is developed by PortSwigger for web application security testing. This tool is widely by security researcher, pentester, ect.The tool helps identify vulnerabilities such as SQL injection, cross-site scripting (XSS), and other web-based security issues.

## Installation process (https://portswigger.net/burp/communitydownload.) 
Make sure you have Java 21 or later installed on your computer. For Windows, run the .exe file and follow the simple setup wizard. On macOS, open the .dmg file and drag Burp Suite to your Applications folder. For Linux, make the .sh file executable and run it from the terminal. Once installed, launch Burp Suite, set your browser to use its proxy (usually 127.0.0.1:8080), and install the Burp CA certificate to handle HTTPS traffic.

# Configuring BurpSuit in browser :
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













 
