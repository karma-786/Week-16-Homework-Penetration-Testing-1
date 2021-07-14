## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:
  - **_Found the information on following website: `demo.testfire.net` Inside Altoro -> About Altoro Mutual -> Executives & Management_**  
  [Executives & Management - Altoro Mutual](http://www.altoromutual.com/index.jsp?content=inside_executives.htm "Executives & Management - Altoro Mutual")  
  
    - **Karl Fitzgerald, Chairman & Chief Executive Officer of Altoro Mutual**  
![Executives & Management - Altoro Mutual](/images/AltoroMutual.PNG "Executives & Management - Altoro Mutual")

- How can this information be helpful to an attacker:  
  - **_This information is very useful to a Hacker (attacker) who wants to send phishing email directly to the executive members._**

#### Step 2: DNS and Domain Discovery

Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located:   
  
**_`Sunnyvale, CA, 94085 - USA`_**  

  2. What is the NetRange IP address:  
  
**_`65.61.137.64 - 65.61.137.127`_**  

  3. What is the company they use to store their infrastructure:  

```
CustName:       Rackspace Backbone Engineering
Address:        9725 Datapoint Drive, Suite 100
City:           San Antonio
StateProv:      TX
PostalCode:     78229
Country:        US
RegDate:        2015-06-08
Updated:        2015-06-08
Ref:            https://rdap.arin.net/registry/entity/C05762718
```  
  
![Whois Record](/images/AltoroMutual-Network-Whois-record.PNG)

  4. What is the IP address of the DNS server:  

**_`65.61.137.117`_**  

![IP Address](/images/AltoroMutual-IP-Address.PNG)

#### Step 3: Shodan

- What open ports and running services did Shodan find:

**_`Open Ports: 80, 443, 8080`_** on the following website: `https://www.shodan.io/host/65.61.137.117`  

![Open Ports](/images/Shodan-65-61-137-117.PNG)

#### Step 4: Recon-ng

- Install the Recon module `xssed`.  
  1.  Search the `module xssed` by entering the command **_`marketplace search xssed`_**
  2.  Install the `module xssed` by entering the command **_`marketplace install recon/domains-vulnerabilities/xssed`_**
  3.  Load the `module xssed` by entering the command **_`modules load recon/domains-vulnerableilities/xssed`_**

![Install the Recon module 'xssed'](/images/Recon-module-xssed-installed.PNG)
  
- Set the source to `demo.testfire.net`.  
  1.  Check the details of the `module xssed` by entering `info`
  2.  To change the `SOURCE` from `default` to `demo.testfire.net` enter command **_`options set SOURCE demo.testfire.net`_**

![Set the SOURCE](/images/Set-the-source-to-demo-testfire-net.PNG)  

- Run the module.  
  - **_`run`_**

![RUN](/images/Run-xssed-demo-testfire-net.PNG)

Is Altoro Mutual vulnerable to XSS: **_Yes it was the only vulnerablities found, as shown above `image`_**  
  - Enter the following script in the `Search bar` on the website: **_`<script>alert("Hello")</script>`_**

![script](/images/run-script-on-the-website-result.PNG)  


### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine:  
  - Run the RDP to start the `Pentesting Lab`.  
  - Open the `Hyper-V-Manager` to view all the active VM's.  
  - Double click the `Kali` VM to start.
  - Start the `Terminal`  
  - From the `Terminal` enter the command `zenmap`
  - The Metasploitable machine IP address is `192.168.0.10`  
  - Input Target `192.168.0.10`
  - Profile: `Quick scan`  
  - The raw nmap Command is `nmap -T4 -A 192.168.0.10`  
  - Click the `SCAN` button to get the results.

![ZENMAP](/images/Zenmap-scan-against-the-Metasploitable-machine.PNG)

- Bonus command to output results into a new text file named `zenmapscan.txt`:
  - To save the results in the `zenmapscan.txt` add the following on the command line: `-oN zenmapscan.txt` so it should look as following: `nmap -T4 -A -oN zenmapscan.txt 192.168.0.10`  
  - You can also enter this in the `Terminal command line`: `nmap -T4 -A -oN zenmapscan.txt 192.168.0.10`  

![zenmapscan.txt](/images/Zenmap-scan-against-the-Metasploitable-machine-save-to-zenmapscan-txt.PNG)

[zenmapscan.txt - file](/zenmapscan.txt)  

- Zenmap vulnerability script command:  
  - There are two scrips that can be located in Zenmap for vulnerability associated with the service running on the 139/445 port.
    - From the **_Profile_** tab select **_Edit Selected Profile_**
    - Select the **_Scripting_** tab and view all the scripts.
    - Check the box off for the **_`ftp-vsftpd-backdoor`_** and **_`smb-enum-shares`_**.
    - **_`Save Changes`_** to save the profile settings.

- The raw command should look like:  
  **_`nmap -T4 -F --script ftp-vsftpd-backdoor,smb-enum-shares 192.168.0.10`_**  

    - `-T4`: -T<0-5>: Set timing template (higher is faster)
    - `-F`: Fast mode - Scan fewer ports than the default scan
    - `--script`: Runs the scripted scan that is followed.
    - `ftp-vsftpd-backdoor`: This script attempts to exploit the backdoor using the innocuous id command by default, but that can be changed with the exploit.cmd or ftp-vsftpd-backdoor.cmd ...
    - `smb-enum-shares`: Host script results: | smb-enum-shares: | account_used: WORKGROUP\​Administrator | ADMIN$ | Type: STYPE_DISKTREE_HIDDEN | Comment: Remote Admin ...
    - `192.168.0.10`: IP address of host that will be scanned.

- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:
      - As per the below snapshots `Zenmap was able to enumerate the vulnerable service` for port 139/445.      
![Zenmap scan against the Metasploitable machine vulnerability scan results](/images/Zenmap-scan-against-the-Metasploitable-machine-vulnerability-scan-results-1.PNG)  
![Zenmap scan against the Metasploitable machine vulnerability scan results](/images/Zenmap-scan-against-the-Metasploitable-machine-vulnerability-scan-results-2.PNG)  

  2. Why is it dangerous:  
      -  **_This is dangerous due to the `VSFTPD 2.3.4` backdoor attack can be applied on `port 21` via a malicious code, if successful execution, opens the backdoor on `port 6200`._**  
          - _This backdoor was introduced into the vsftpd-2.3.4.tar.gz archive between June 30th 2011 and July 1st 2011 according to the most recent information available. This backdoor was removed on July 3rd 2011._ (1)  
          - _The concept of the attack on VSFTPD 2.3.4 is to trigger the malicious vsf_sysutil_extra(); function by sending a sequence of specific bytes on port 21, which, on successful execution, results in opening the backdoor on port 6200 of the system and running as root._ (2)  
  
      - **_The `Windows Server Message Block (SMB)` get access through the organization's networks, the SMB protocols used by PC's for file and printer sharing, along with the remote access services._**  
  
        - _SMB vulnerabilities allow their payloads to spread laterally through connected systems._ (3)    

  3. What mitigation strategies can you recommendations for the client to protect their server:  
      - **_The `vsFPTD 2.3.4 patch was released on July 3, 2011` with the patch constantly monitered and updated._**  

        - _The vsFTPD v2.3.4 backdoor reported on 2011-07-04 (CVE-2011-2523)._ (4)  

      - **_The `SMB` (`CVE-2017-0145`) patch was released by Microsoft `MS17-010` , and the `SAMBA` (`CVE-2017-0145`) patches were released by Red Had for Linux `RHSA-2017:1390`_** (5, 6 & 7)
---

### References

- Hacking Blogs: [What Is Recon-ng? How To Use Recon-ng | Best Guide](https://hackingblogs.com/learn-recon-ng/), May 25, 2018  
- [Recon-ng V5 - Marketplace & Installing Recon Modules (whois, subdomain enumeration)](https://www.youtube.com/watch?v=oSt6WdTaCV4) HackerSploit (Youtube) Nov 25, 2019.
- [Recon-ng 5.1 Cheat Sheet](https://www.blackhillsinfosec.com/wp-content/uploads/2019/11/recon-ng-5.x-cheat-sheet-Sheet1-1.pdf) lanmaster53, Nov 21, 2019.
- Gordon Lyon: [Zenmap is the official Nmap Security Scanner GUI.](https://nmap.org/zenmap/) Zenmap.  
- [Recon-NG Tutorial](https://hackertarget.com/recon-ng-tutorial/) SECURITY NEWS, Feb 16, 2018 on hackertarget.com  
- [vsftpd 2.3.4 - Backdoor Command Execution (Metasploit)](https://www.exploit-db.com/exploits/17491) Tags: Metasploit Framework (MSF) on EXPLOIT DATABASE BY OFFENSIVE SECURITY (1)  
- [Vulnerability analysis of VSFTPD 2.3.4 backdoor](https://subscription.packtpub.com/book/networking_and_servers/9781786463166/1/ch01lvl1sec18/vulnerability-analysis-of-vsftpd-2-3-4-backdoor) Packt (2)  
- Pieter Arntz: [How threat actors are using SMB vulnerabilities](https://blog.malwarebytes.com/101/2018/12/how-threat-actors-are-using-smb-vulnerabilities/) Posted on Malwarebytes, Dec 14, 2018. (3)  
- [Exploiting VSFTPD v2.3.4 on Metasploitable 2](https://www.hackingtutorials.org/metasploit-tutorials/exploiting-vsftpd-metasploitable/) By: HACKING TUTORIALS ON JULY 29, 2016.  
- [File ftp-vsftpd-backdoor](https://nmap.org/nsedoc/scripts/ftp-vsftpd-backdoor.html) Daniel Miller, NMAP.ORG
- [CVE-2011-2523 Detail](https://nvd.nist.gov/vuln/detail/CVE-2011-2523) NATIONAL VULNERABILITY DATABASE (4)  
- [Microsoft Security Bulletin MS17-010 - Critical](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010) Microsoft, Published: March 14, 2017 (5)
- [CVE-2017-7494.html](https://www.samba.org/samba/security/CVE-2017-7494.html) Samba.org (6)
- [CVE-2017-7494](https://access.redhat.com/security/cve/cve-2017-7494) Red Hat, Public on May 23, 2017. (7)   

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

  
## :sunglasses: `Ketan Vithal Patel` :sunglasses:
==============================================
### `July 12, 2021 -- UofT Cybersecurity - Boot Camp`
#### :rose::rose:`Jai Shri Swaminarayan`:rose::rose:
```
હરે કૃષ્ણ હરે કૃષ્ણ, કૃષ્ણ કૃષ્ણ હરે હરે |  Hare Krishna Hare Krishna, Krishna Krishna Hare Hare |
હરે રામ હરે રામ, રામ રામ હરે હરે ||   Hare Ram Hare Ram, Ram Ram Hare Hare ||
```
