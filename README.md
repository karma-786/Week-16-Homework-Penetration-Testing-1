## Week 16 Homework Submission File: Penetration Testing 1

#### Step 1: Google Dorking


- Using Google, can you identify who the Chief Executive Officer of Altoro Mutual is:
  - **_Found the information on following website: `demo.testfire.net` Inside Altoro -> About Altoro Mutual -> Executives & Management_**  
  [Executives & Management - Altoro Mutual](http://www.altoromutual.com/index.jsp?content=inside_executives.htm "Executives & Management - Altoro Mutual")  
  
    - **Karl Fitzgerald, Chairman & Chief Executive Officer of Altoro Mutual**
    ![Executives & Management - Altoro Mutual]( "Executives & Management - Altoro Mutual")

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

  4. What is the IP address of the DNS server:  

**_`65.61.137.117`_**

#### Step 3: Shodan

- What open ports and running services did Shodan find:

**_`Open Ports: 80, 443, 8080`_** on the following website: `https://www.shodan.io/host/65.61.137.117`

#### Step 4: Recon-ng

- Install the Recon module `xssed`. 
- Set the source to `demo.testfire.net`. 
- Run the module. 

Is Altoro Mutual vulnerable to XSS: 

### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Command for Zenmap to run a service scan against the Metasploitable machine: 
 
- Bonus command to output results into a new text file named `zenmapscan.txt`:

- Zenmap vulnerability script command: 

- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability:

  2. Why is it dangerous:

  3. What mitigation strategies can you recommendations for the client to protect their server:

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

  
## :sunglasses: `Ketan Vithal Patel` :sunglasses:
==============================================
### `July 12, 2021 -- UofT Cybersecurity - Boot Camp`
#### :rose::rose:`Jai Shri Swaminarayan`:rose::rose:
```
હરે કૃષ્ણ હરે કૃષ્ણ, કૃષ્ણ કૃષ્ણ હરે હરે |  
હરે રામ હરે રામ, રામ રામ હરે હરે ||
```
