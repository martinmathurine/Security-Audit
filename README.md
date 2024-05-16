# Security-Audit

## Introduction – Background Information
Please note, in this lab scenario, a virtual machine environment was set up to simulate a private home computer network. The network consisted of various virtual hosts, including simulated media streaming devices, smartphones, tablets, and desktop PCs. Each virtual host was assigned an IP address within a specified range. The virtual environment was configured to mimic a typical home network setup, allowing for comprehensive vulnerability assessment testing.

Nessus, like other vulnerability scanners, actively tests computer networks to detect and prevent attacks. It recommends patches, is free and open-source, and has a user-friendly interface. Vulnerability assessments shift cybersecurity from reactive to proactive, identifying and prioritising weaknesses. This report explores the importance of vulnerability assessments in security audits, discussing aspects of GRC and action plans for resolving vulnerabilities.

## Requirements for Vulnerability Assessments
Adhering to industry standards can boost a company's competitiveness by enhancing its reputation and reducing costs through the use of standard practices. Legal compliance, including liability insurance and adherence to regulations like the Data Protection Act 2018 and GDPR, ensures lawful handling of data. The Computer Misuse Act 1990 governs lawful interactions with electronic data, ensuring security assurances like the CIA triad are met [2]-[4].

Obtaining certifications like Cyber Essentials and ISO 27001 demonstrates commitment to cybersecurity, attracting stakeholders and new business [5]. Training and certifications for designated staff, such as CompTIA Security+ and CEH, are prerequisites for vulnerability assessment and penetration testing [6]. Risk assessments aid governance by evaluating organisational controls, including policies and incident response processes [7].

Conducting a vulnerability assessment involves defining the scope, scanning IT infrastructure for weaknesses, and ranking vulnerabilities based on severity [8]. Tools like Nessus use the CVSS to assign numerical scores for prioritisation [6]. Mitigating threats with tools like antivirus software and remedying vulnerabilities through updates or additional security measures complete the process [8].

## Vulnerability Assessments vs. Penetration Testing
In a comprehensive vulnerability assessment, the objective is to identify common potential security weaknesses, assess the risk severity level and then recommend whether to mitigate or remediate them. Vulnerability assessments are performed on computer networks (wired/wireless), databases, web apps, host servers and wireless network infrastructure configurations.
As part of a full security audit, penetration testing aims to exploit the vulnerabilities that the assessment initially found within the compromised network, identify security weaknesses, and determine how to strengthen them. Unlike automated scanning tools like Nessus, human penetration testers can ask deeper goal-orientated questions about the initial assessment simulating a real-life cyber-attack.

Typically, vulnerability assessments are automated to cover a wide variety of unpatched vulnerabilities,, saving significant time. There are many tools used to perform a vulnerability assessment, such as Nessus’ vulnerability scanner, Wireshark to analyse network protocols capturing packet data as well as Aircrack-ng to assess Wi-Fi security, among many others. On the other hand, penetration testing tools are approached from a manual perspective for a more robust assessment of the computer network carried out by field experts using many tools. Penetration testing tools help assure that the organisation’s vulnerability assessments are accurate. [6]-[9]

## Practical Vulnerability Assessment
### Scanning Environment
In this lab, I'm using Nessus Essentials, the free version of the Nessus software suite, to scan my private computer network. The network consists of six hosts: a mains-powered media streaming device box, a TV set-top box, a USB media streaming device, a smartphone, a tablet, and a Windows-based desktop PC. The mains-powered media streaming device box and TV set-top box are connected via 1Gb ethernet, while the other hosts are wirelessly connected on the 5GHz Wi-Fi band. Each device is linked to my Internet service provider's (ISP) wireless router hub.

### Scope of Testing
The objective and scope of the scan involve identifying potential security weaknesses within the confines of my virtual machine's home private computer network, including the host devices connected to it within a known IP range. In the real world, organisations will perform vulnerability assessments regularly depending on their methodology to mitigate network IT security risks. However, for the purpose of this report, only a focused test was performed.

### Configuration and Profiles
Nessus Essentials has some pre-configured profiles to perform many vulnerability assessments in my private network. These profiles can also be customised for more specific scanning. [11] Once Nessus Essentials is installed and set up, it can perform vulnerability scans. Since the hosts have been identified manually/visually, a host discovery assessment will be performed by setting the target IP range of hosts to scan between ommiting my private network’s router from the scanned targets. I found all host IP addresses by simply logging into my router's admin console. Another method is to type ‘arp -a’, which returns all IP addresses in a LAN.  In Nessus Essentials, a configuration is a set of options defined to scan for vulnerabilities in different ways. A profile is a set of configurations designed for a specific objective for a scan. Scan settings enable you to refine scan parameters to meet your specific network security needs. The scan settings you can configure vary depending on the Tenable-provided template on which a scan or policy is based. By, using the pre-configured profiles in Nessus Essentials a cyber-security professional can be more efficient and accurate which is vital in mitigating security risks using a pre-defined policy across multiple clients.

Knowing the hosts on your network is the first step to any vulnerability assessment. Launching a host discovery scan after previously identifying the host devices myself in my private network, this pre-configured profile scanned the full target IP range, a fully qualified domain name (FQDN), operating systems (OS) and open ports. This scan confirmed the same host devices on my network showing only six hosts. The resources used for this type of scan were light and did not affect the performance of my network. The configurations used in host discovery include host enumeration, OS identification and port scanning (common ports/all ports). [12]-[14]

Next, to configure Nessus Essentials for a full comprehensive vulnerability scan I first created a new custom policy using the advanced scan policy template. Though policies need to be manually configured, creating a new policy in this regard can provide a more thorough scan. Policies define the actions for the scanner – a scan needs the policy to function. To re-configure the settings for this policy template, I must first give a name and description for the policy which are ‘new policy’ and ‘my new policy’ respectively. In the discovery section’s ‘remote host ping’, this was turned off because if any of the IP addresses do not respond to pinging such as the Internet Control Message Protocol (ICMP) then it may miss ports that are open. All fragile devices were left unticked because I do not have any of these devices. In a work environment leaving fragile devices’ checkboxes unticked may result in a denial-of-service (DoS) leaving a client displeased as this could lead to devices or the entire network becoming inaccessible. For port scanning, I would scan the entire TCP and UDP port range (T:1-65535,U:1-65535), but for the sake of time, I have chosen to scan using the default setting. If I were to scan using the full UDP ports I would also tick the box, but as mentioned previously enabling a UDP port scanner may dramatically increase the scan time and produce unreliable results. Therefore, for this focus test, I have chosen to leave this option deselected for now. In service discovery I would choose to search for all TCP and UDP ports but since I have only used the default settings in this section searching for only all TCP ports. Searching for all TCP and UDP ports will allow all TLS services running on non-default ports to be found – ensuring that ‘probe for all ports to find services’ is essential. 

In the assessments tab, in a working environment, I would choose the ‘perform thorough test’ but this will further increase the scan time and stress my theoretical home network, so I left it unchecked for the sake of this assessment. The next tab about scanning for web applications was not selected because they were not within the scope of my testing. Requesting information about the SMB domain should be checked to query domain users, however, this is a home network, so it is unnecessary. Scanning for malware is not within the scope so this was left unchecked. 
For the ‘reports’ tab, ‘show missing patches that have been superseded’ was left unchecked because it will show all patches that are missing on my Windows-based [or Linux-based] desktop PC that is missing instead of the top-level patch from the most recent date that will encompass all prior patches. This will provide the client with fewer data but more concise information.
For the ‘plugins’ tab, I first disabled all plugins so that I could choose the components that apply to the scope of the testing and scanning environment set out in this vulnerability assessment. Therefore, the plugins chosen are applicable to my network. I only have Windows and Apple devices in this personal homelab so plugins for those were selected. The selected plugins are as follows; backdoors, denial of service, DNS, firewalls, gain a shell remotely, general, MacOS X local security checks, misc., Windows, Windows: Microsoft bulletins and Windows: user management. Also, no credentials were set.

I then created a new custom scan using the user-defined scan template which takes me to a setting to choose my custom policy. I then named and described the custom scan as ‘policy_scan’ and ‘my new policy scan for today’ respectively. The target IP addresses of the six host devices were entered. Once the custom scan is saved, only then could I launch the vulnerability assessment for analysis. [15][16]

### Factors That Could Affect the Completeness of the Scan
To ensure the completeness of the scan, software/firmware for all hosts was updated so that Nessus Essentials can detect and apply the latest risk assessments to each host. Not doing so could produce inaccurate results if Nessus does not know there is a software update. Also, allowing Nessus through my anti-virus exception list and firewall software as this could hamper the scanning process from fulfilling the policy. [17] [18]

## Summary of the Results
### Analysis of Test Results
To review the generated results from the vulnerability assessment, there were no unexpectedly found hosts on my network since I performed a thorough host discovery scan using adequate tools. Once the vulnerability scan is completed, I was given all the vulnerabilities ranging from informational, low, medium, high and critical. After producing an HTML dashboard report of my test results (as shown in Appendix A) it gives a dashboard view summary which is simple to understand and effective when relaying highly technical information and data to a client that may not understand all of the technical jargon and just wants to see results. From my custom vulnerability scan, it clearly shows the CVSS assigned numerical scores illustrating the weaknesses within the network. The plugins returned many potential informational risks which could be used to identify sensitive data stored within the network. Although these are from the lowest risk factor, these risks should still be taken into consideration when considering the robustness of the network.
To further analyse the test results, I created a technical report review in the CSV format selecting all columns for a more detailed analysis. The CSV document is then opened for editing in Microsoft Excel. Empty cells or non-relevant cells containing little to no data were cleared to make the scan analysis look more concise. The document is then formatted, custom sorted and filtered by the ‘plugin id’ and ‘risk factor’. Then, by reading the ‘synopsis’, ’‘description’ and the ‘solution’ to understand what is happening on the network’s services. This is why it is very important to run regular vulnerability assessments to ensure that the risks have been mitigated or resolved completely so that the scan ultimately becomes clean. [15] [16]

(See **Appendix A**)

### The Main Vulnerabilities
My mains-powered media streaming box device's IP address has a reported medium-risk DNS issue, but this may be a false positive since it is in standby mode possibly though I have no content streaming issues this is most likely a false red flag. To remedy this, I could reset my DNS from ‘automatic’ to ‘manual’ and vice versa. I did not have to adjust or recheck the environment to get results. My vulnerability scan was thorough for the scope of the testing and the results were almost consistently rated as below low risk and the security issue that I could mitigate was resolved by following Microsoft’s documentation to do so.

The only other host to report three medium-risks was my Windows-based desktop PC. There were two mixed SSL-related issues both pertaining to multiple certificate trust issues on the 3389/TCP port. This port is usually reserved for remote desktop (RDP) access and I have two RDP clients on my desktop PC which are already up-to-date firmware-wise, so this too is a false positive. However, the vulnerability scan does let me know that RDP clients are prone to man-in-the-middle (MITM) attacks which are severe security breaches and should be treated with caution to monitor this port. Additionally, the third medium-risk issue was related to a Server Block Message (SMB) protocol within Windows 11’s local policies being disabled. Although this was remedied by enforcing message signing in the host's configuration this, however, was not reflected in the rescanning of this host a second time as shown in Appendix A. By not enforcing message signing in the host's configuration, an unauthenticated, remote attacker may be able to exploit this to conduct a MITM attack. Moreover, “if someone changes a message during transmission, the hash won't match, and SMB will know that someone tampered with the data. The signature also confirms the sender's and receiver's identities. This prevents relay attacks.” [19] [20]

From the vulnerability assessment conducted, I have shown that my virtual private home network is secure. The results were accurate although there were some false positives, one was resolved and two others were just notifying me that there is RDP access within my network which I have authorised and monitored myself to be acceptable.

### Resolving Reported Vulnerabilities
The plan of action to resolve the SMB issue was to configure a setting using the local security policy console by using the Run command prompt box and entering ‘secpol.msc’. Under the ‘security settings’ of the console tree, I selected ‘local policies’ to edit the ‘security options’. The policy that I needed to enable within its properties was called, ‘Microsoft network client: Digitally sign communications (always)’. Afterwards, I relaunched a new scan using the same security parameters, but this time focusing only on the inflicted host. After retesting twice, the results were the same even though I’d performed the solution to resolve it which is supported by Microsoft’s own documentation. [19] [20] The results from the discovered vulnerabilities are in my opinion overcautious, however, that can also be perceived as a good thing as the assessment proved to be appropriate to what I expected and one of the issues was resolved successfully as the results of the retesting showed otherwise as a false positive even though the solution was resolved.

### Results of Retesting
To demonstrate that the countermeasure worked, please refer to Appendix A.

[See **Appendix A**]

## Concluding Reflections
To conclude, Nessus is an industry-standard tool used to perform vulnerability assessments to know the posture of a network and the connected devices. Performing vulnerability assessments on my virtual private home network has given me a greater insight into how to effectively secure a network even at an enterprise level ensuring the confidentiality, integrity and availability of an organisation’s personal information and data in ways that I have not considered until now. I also learned that being thorough during a comprehensive vulnerability scan is not enough if best practices are not in place. Regular and thorough scans to check the health of a network depending on the scanning environment and scope of the testing I have found to be the most effective way to prevent security exploits from malicious attackers. 
As a result, this homelab has made me competent in the foundation of security auditing. 

## References
- [1] ‘What Is the Nessus Scanner? Working and Key Features’. Spiceworks, https://www.spiceworks.com/it-security/data-security/articles/what-is-nessus-scanner/. Accessed 5 Mar. 2023.
- [2] ‘Data Protection’. GOV.UK, https://www.gov.uk/data-protection. Accessed 5 Mar. 2023.
- [3] About Cyber Essentials. https://www.ncsc.gov.uk/cyberessentials/overview. Accessed 5 Mar. 2023.
- [4] Tankard, Colin. ‘Cyber Essentials Accreditation – Is It Worth It?’ Elite Business Magazine, 21 Oct. 2022, https://elitebusinessmagazine.co.uk/technology/item/cyber-essentials-accreditation-is-it-worth-it. Accessed 5 Mar. 2023.
- [5] ECSA, Strahinja Stankovic. ‘How To Perform A Successful Network Vulnerability Assessment’. PurpleSec, 7 July 2019, https://purplesec.us/perform-successful-network-vulnerability-assessment/. Accessed 5 Mar. 2023.
- [6] ‘Penetration Testing for Regulatory Compliance’. Reciprocity, https://reciprocity.com/resource-center/penetration-testing-for-regulatory-compliance/. Accessed 5 Mar. 2023.
- [7] ‘Pen Testing vs. Vulnerability Scanning: What’s the Difference? | TechTarget’. Security, https://www.techtarget.com/searchsecurity/tip/The-differences-between-pen-tests-vs-vulnerability-scanning. Accessed 5 Mar. 2023.
- [8] Church, Andrew. ‘4 Steps to Conducting a Proper Vulnerability Assessment’. Candid Blog, 20 Nov. 2020, https://blog.candid.org/post/4-steps-to-conducting-a-proper-vulnerability-assessment/. Accessed 5th Mar. 2023.
- [9] ‘Manual vs Automated Penetration Testing’. BlueFort Security, https://www.bluefort.com/news/latest-blogs/manual-vs-automated-penetration-testing/. Accessed 5 Mar. 2023.
- [10] Mitigo. Cyber and Data Security – Five Legal Obligations You Shouldn’t Ignore. https://www.lawsociety.org.uk/topics/small-firms/cyber-and-data-security-five-legal-obligations-you-should-not-ignore. Accessed 5 Mar. 2023.
- [11] Download Nessus. https://www.tenable.com/downloads/nessus?loginAttempted=true. Accessed 5th Mar. 2023.
- [12] Example: Host Discovery (Nessus 10.5). https://docs.tenable.com/nessus/Content/HostDiscovery.htm. Accessed 5th Mar. 2023.
- [13] Scan and Policy Settings (Nessus 10.5). https://docs.tenable.com/nessus/Content/TemplateSettings.htm. Accessed 5th Mar. 2023.
- [14] Preconfigured Discovery Scan Settings (Nessus 10.5). https://docs.tenable.com/nessus/Content/DiscoverySettingsPreconfigured.htm. Accessed 5th Mar. 2023.
- [15] Nessus Scan Essentials And Scan Analysis (Hands-On). www.youtube.com, https://www.youtube.com/watch?v=ynTagBRTB-4. Accessed 5th Mar. 2023.
- [16] How to Configure Nessus Vulnerability Scanner. www.youtube.com, https://www.youtube.com/watch?v=ho7hTbuhXz4. Accessed 5th Mar. 2023.
- [17] Antivirus Software (Nessus 10.5). https://docs.tenable.com/nessus/Content/AntivirusSoftware.htm. Accessed 5th Mar. 2023.
- [18] ‘4 Ways to Improve Nessus Scans Through Firewalls’. Tenable®, 18 Dec. 2020, https://www.tenable.com/blog/4-ways-to-improve-nessus-scans-through-firewalls. Accessed 5th Mar. 2023.
- [19] Deland-Han. Overview of Server Message Block Signing - Windows Server. 23 Feb. 2023, https://learn.microsoft.com/en-us/troubleshoot/windows-server/networking/overview-server-message-block-signing. Accessed 5th Mar. 2023.
- [20] vinaypamnani-msft. Configure Security Policy Settings (Windows 10). 17 Feb. 2023, https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/how-to-configure-security-policy-settings. Accessed 5th Mar. 2023.

## Appendix A

Fig, 1. Host discovery through logging into my router’s IP address in my web browser to identify hosts connected to LAN.
<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/08fa795c-48b5-41a5-b69c-5b94ef4495f4"/>

Fig, 2. Using the pre-configure profile for host discovery through Nessus Essentials to scan for a target IP addresses within my LAN.
<img width="500" src="
  "/>


Fig, 3. The host discovery results showing all IP addresses for connected network devices.
<img width="500" src="
  "/>


Fig, 4. Created a new custom policy template which I would use to configure the settings in regard to my personal scanning environment and scope of testing.
<img width="500" src="
  "/>




Fig, 5. Selected the advanced scan type in order to do a comprehensive scan.
<img width="500" src="
  "/>



Fig, 6. Selected ‘new scan’ so that I can create a new scan template.
<img width="500" src="
  "/>


Fig, 7. For my scan template I used the ‘user-defined’ scan template where it was possible to select my previously created custom policy.
<img width="500" src="
  "/>


Fig, 8. This screenshot illustrates the plugins chosen as it pertains to my scanning environment and scope of the testing. 
<img width="500" src="
  "/>


Fig, 9. This custom scan was aptly titled, ‘policy_scan’.
<img width="500" src="
  "/>


Fig, 10. This screenshot illustrates the test results from the initial comprehensive vulnerability scan.
<img width="500" src="
  "/>


Fig, 11. Illustrates the SSL certificate issue.
<img width="500" src="
  "/>
  

Fig, 12. Illustrates another SSL certificate issue.
<img width="500" src="
  "/>


Fig, 13. This screenshot shows many potential risks ranging from informational to medium risk.
<img width="500" src="
  "/>


Fig, 14. Shows the SMB issue which was eventually resolved manually.
<img width="500" src="
  "/>


Fig, 15. A new custom scan was created with a target on the single IP address to be time efficient which contained the SMB issue that I resolved through enabling it in the local security policy console.
<img width="500" src="
  "/>


Fig, 16. Produced two reports which were a simple a dashboard report and a technical analysis report shown in both HTML and CSV formats, respectively.
<img width="500" src="
  "/>


Fig, 17. A simple dashboard report. Suitable for clients that just want to have a short but detailed scan results.
<img width="500" src="
  "/>


Fig, 18. The technical analysis report which data has been cleaned, filtered and sorted. In this screenshot the CSV document has been sorted by ‘plugin ID‘ so that an IT professional can easily see what type of issues to batch fix as duplicate plugin IDs are shown together.
<img width="500" src="
  "/>



