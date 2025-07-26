# Nessus Essentials Vulnerability Management Life Cycle Lab

## Introduction – Background Information
A virtual lab simulating a typical home network was created, featuring multiple hosts like smart devices and PCs with assigned IPs. This environment enabled realistic vulnerability assessment testing.

Nessus was used to identify and prioritise security weaknesses, supporting a proactive risk management approach. This report highlights the role of vulnerability assessments in audits, with focus on policy and the full life cycle of vulnerability management.

## Requirements for Vulnerability Assessments
Adhering to industry standards improves reputation, reduces costs, and ensures compliance. Legal obligations under the Data Protection Act 2018, GDPR, and the Computer Misuse Act 1990 require secure handling of data and support the CIA triad [2]–[4].

Certifications like Cyber Essentials and ISO 27001 demonstrate cybersecurity commitment, attracting stakeholders [5]. Staff qualifications, such as CompTIA Security+ and CEH, are essential for vulnerability assessments and penetration testing [6]. Risk assessments support governance by evaluating organisational controls, policies, and incident response processes [7].

Assessments involve defining scope, scanning systems, and prioritising risks using CVSS scoring [6], with tools like Nessus aiding this process. Remediation includes applying updates or implementing additional security measures [8].

## Vulnerability Assessments vs. Penetration Testing
Vulnerability assessments aim to identify common security weaknesses, evaluate risk severity, and recommend mitigation or remediation. These assessments cover networks, databases, web applications, servers, and wireless configurations.

Penetration testing, conducted as part of a broader security audit, involves exploiting identified vulnerabilities to uncover deeper weaknesses and strengthen defences. Unlike automated tools such as Nessus, penetration testers perform manual, goal-oriented testing that simulates real cyber-attacks.

Vulnerability assessments typically rely on automated tools like Nessus, Wireshark, and Aircrack-ng for broad coverage and efficiency. Penetration testing employs manual techniques and specialised tools to validate and extend assessment findings, providing a more thorough evaluation [6]–[9].

## Practical Vulnerability Assessment
### Scanning Environment
This lab utilised Nessus Essentials, the free edition of Nessus, to scan a LAN comprising six hosts: a media streaming device, TV set-top box, USB media streamer, smartphone, tablet, and Windows desktop PC. The media devices connect via Ethernet, while other hosts connect over 2.4 GHz, 5GHz, and 6 GHz Wi-Fi through the ISP’s wireless router.

### Scope of Testing
The scan focused on identifying security weaknesses within the virtual home network and its connected devices in a defined IP range. While organisations typically conduct regular vulnerability assessments, this report details a single, targeted test to demonstrate methodology.

### Configuration and Profiles
Nessus Essentials includes pre-configured profiles for common vulnerability assessments, which can be customised to suit specific needs [11]. Following installation, host discovery was conducted by specifying the target IP range—excluding the router—based on IPs obtained via the router’s admin console and the arp -a command. Host discovery scans enumerated devices, identified operating systems, and detected open ports with minimal network impact [12]–[14].

For a comprehensive vulnerability scan, a custom policy was created using the advanced scan template. The policy was named and configured to optimise scanning efficiency and accuracy. Key adjustments included disabling remote host ping to avoid missing unresponsive devices, leaving fragile device checks unchecked to prevent potential Denial-of-Service (DoS) impacts, and using default port scanning ranges for time efficiency. While scanning all TCP and UDP ports would be ideal, UDP scanning was omitted to reduce scan duration and false positives.

Service discovery targeted all TCP ports, ensuring detection of TLS services on non-standard ports. More thorough tests and additional scans for web applications, SMB domains, and malware were excluded as they fell outside the assessment scope. Reporting settings excluded superseded patches to prioritise concise, relevant remediation data.

Plugins were selectively enabled to reflect the homelab environment, focusing on Windows and Apple device vulnerabilities, including backdoors, DoS, DNS, remote shell access, and user management. No credentials were used during scanning.

A custom scan was then created using the defined policy, targeting the six identified hosts. This configuration enabled the launch of an efficient, focused vulnerability assessment [15][16].

### Factors That Could Affect the Completeness of the Scan
To ensure scan accuracy, all host software and firmware were updated, enabling Nessus Essentials to detect the latest vulnerabilities. Failure to update could result in incomplete or inaccurate findings. Additionally, Nessus was allowed through antivirus and firewall exceptions to prevent scanning interruptions [17][18].

## Summary of the Results
### Analysis of Test Results
No unexpected hosts were detected, confirming the thoroughness of the initial discovery scan. The vulnerability scan identified issues across informational to critical severity levels. The HTML dashboard report (Appendix A) provided a clear summary, suitable for both technical and non-technical stakeholders. CVSS scores highlighted network weaknesses, with numerous informational risks that, despite low severity, warrant attention.

For deeper analysis, the scan results were exported to CSV and processed in Excel. Non-relevant data were removed to improve clarity. Data was sorted and filtered by plugin ID and risk factor, with detailed review of synopses, descriptions, and solutions. This reinforces the importance of regular vulnerability assessments to ensure risk mitigation and maintain a secure network [15][16].

(See **Appendix A**)

### The Main Vulnerabilities
The mains-powered media streaming device showed a medium-risk DNS issue, likely a false positive due to standby mode, as no streaming issues were observed. A potential fix involves toggling DNS settings between automatic and manual. The scan was thorough, with most findings rated below low risk, and any actionable issues resolved per Microsoft guidance.

The Windows desktop PC reported three medium-risk vulnerabilities. Two related to SSL certificate trust issues on TCP port 3389 (used for RDP). These are false positives as RDP clients are up-to-date; however, the scan correctly highlights the risk of man-in-the-middle (MITM) attacks on RDP, warranting monitoring. The third issue involved SMB protocol message signing being disabled in Windows 11 local policies. Enforcing message signing mitigates MITM risks by ensuring data integrity and authenticating sender and receiver identities [19][20]. Despite remediation, rescans still flagged this, consistent with Microsoft documentation.

Overall, the virtual home network is secure, with accurate results and manageable false positives. One vulnerability was resolved, and others serve as monitored alerts for authorised RDP access.

### Resolving Reported Vulnerabilities
The SMB issue was addressed by enabling ‘Microsoft network client: Digitally sign communications (always)’ via the local security policy console (secpol.msc). Despite applying this fix and rescanning the affected host twice, the vulnerability persisted in reports, aligning with Microsoft’s documentation [19][20]. While the scanner’s caution may appear excessive, it confirms the assessment’s thoroughness and validates successful remediation.

### Results of Retesting
To demonstrate that the countermeasure worked, please refer to Appendix A.

[See **Appendix A**]

## Concluding Reflections
Nessus remains an industry-standard tool for assessing network security posture and connected devices. Conducting vulnerability assessments on the virtual private home network provided valuable insight into securing networks at both personal and enterprise levels, reinforcing the importance of confidentiality, integrity, and availability.

The exercise highlighted that thorough scanning alone is insufficient without implementing best practices. Regular, comprehensive assessments tailored to the environment and scope are essential to prevent exploitation by malicious actors.

Overall, this homelab experience has solidified foundational skills in security auditing.

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

***Fig, 1.*** Host discovery via arp -a or router admin console identifying LAN hosts.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/08fa795c-48b5-41a5-b69c-5b94ef4495f4"/>

***Fig, 2.*** Using pre-configured Nessus Essentials profile for LAN IP scanning.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/4dc930f0-58eb-4301-a574-892f8a868be9">

***Fig, 3.*** Host discovery results displaying all connected network devices' IP addresses.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/85d4480e-7ea9-471d-af59-3f70b5064c6b">

***Fig, 4.*** Custom policy template creation for personal scanning environment settings.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/23ee7df2-8b8b-4fad-9c34-674fa5d4e06a">

***Fig, 5.*** Selection of advanced scan type for comprehensive scanning.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/604189e9-28e5-4b01-b736-7bdf03b5a398">

***Fig, 6.*** Creation of new scan template.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/1177b6e1-fe9a-494e-b188-0736ef080761">

***Fig, 7.*** Usage of 'user-defined' scan template with custom policy selection.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/acf2b3c0-d00c-4dc9-a51e-7ed9f1e30561">

***Fig, 8.*** Illustration of chosen plugins for scanning environment and testing scope.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/a0d67eb3-7797-49e7-b149-57a463993459">

***Fig, 9.*** Custom scan named 'policy_scan'.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/7186e642-fd6c-4ab3-9370-fa7f9bd83cb7">

***Fig, 10.*** Initial comprehensive vulnerability scan results.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/27971885-4a03-4e61-9c15-a1fd2399c7b3">

***Fig, 11.*** SSL certificate issue illustration.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/eaa01e73-bc56-4777-8531-47c56626dc73">

***Fig, 12.*** Another SSL certificate issue illustration.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/c7a41037-f775-4c0f-a3e7-49f49198e63b">

***Fig, 13.*** Screenshot showing potential risks from informational to medium.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/7f7a710f-a5dd-4cc0-84b3-e7e83d7897a7">

***Fig, 14.*** Illustration of SMB issue that was resolved manually.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/48c7c431-bead-4688-bba6-517537a76447">

***Fig, 15.*** Creation of new custom scan targeting a single IP address containing SMB issue. Resolved through enabling it in the local security policy console.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/1e9011fc-038b-4366-bd93-00ab4741af6a">

***Fig, 16.*** Production of dashboard and technical analysis reports in HTML and CSV formats, respectively.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/c4b45ddb-4fa3-42bf-a6ac-59ab2a7d8cec">

***Fig, 17.*** Simple dashboard report suitable for clients desiring brief yet detailed scan results.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/65015881-a083-4db4-a996-e73f853a957e">

***Fig, 18.*** Technical analysis CSV report with cleaned, filtered, and sorted data, facilitating batch fixing of issues by plugin ID.

<img width="500" src="https://github.com/martinmathurine/Security-Audit/assets/42855193/987fb798-236b-4b98-a0c6-30d9db0d29f3">
