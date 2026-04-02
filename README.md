Vulnerability coverage study cases
These study cases train reasoning around vulnerability management on network devices.
The goal of this exercise is to:
When asked to answer questions: support by evidence (screenshots, quotes, links).
Decisions: support them with reasoning and provide alternate options.
When something is assumed, mark it clearly.
What to watch out for:
Guesses and unmarked assumptions,
Answers without any evidence.
Decisions without logical reasoning chain.
Study Case 1
You will investigate a vulnerability of an Aruba asset in this case.
Estimated time required for this study case: 45 minutes.
Step 1: Initial Research 
Start with a fast research of Aruba. Below you can see example information that may be interesting for this case study.
What types of network devices does Aruba produce?
How could HPE’s acquisition of Aruba affect the source of vulnerability information?
Does Aruba develop one or multiple operating systems for their products?
You may use the website of the vendor, other relevant websites, official Youtube channel, AI, or any other resource you will find relevant to perform the research.
Step 2: Security Advisory
Open the web advisory from this link. Gather the following information:
Does this advisory cover one or multiple CVE(s)?
What operating systems and operating system versions are affected by the vulnerability/vulnerabilities?
Step 3: Command Selection
The documentation for both AOS-8 and AOS-10 contain a list of commands available using the command line interface (CLI). The commands for AOS-8 are available here. The commands for AOS-10 are available here.
Select one command for each OS which would provide evidence about the vulnerability of an asset. Look for commands that reveal software version and model. (Hint: You are interested in version information.)
Read the example outputs of commands you consider. The example outputs are included in the documentation. Check if the command really includes an operating system version.
Step 4: Gathering Information Using SNMP
Using CLI usually requires providing SSH credentials. However, there are alternative protocols that may be used, such as SNMP. Do quick research on the SNMP protocol. Your research should focus on the following questions:
What types of requests does SNMP support?
What is OID?
Is there a specific OID focused on gathering the system description of a product?
What port number is used by SNMP by default?
Step 5: Reading SNMP Information
Below you can see an output provided by Aruba asset after sending GET request to sysDescr OID (1.3.6.1.2.1.1.1)
ArubaOS (MODEL: Aruba7005), Version 10.7.0.1 SSR (91033)
Evaluate the command output. Does it provide evidence suggesting the asset is (not) vulnerable?
Step 6: Conclusion and Discussion
Summarize the knowledge you gained during the study case.
If you are given a network asset, which sources can be used to identify the vendor of the asset and operating system running on the asset? Which source is the quickest? Which one is most reliable? Which one requires credentials?
If you identify the vendor and OS, list the steps to check whether the asset has a known vulnerability.
Study Case 2
You will investigate a vulnerability of an Arista asset in this study case.
Part 1
Estimated time required for this part: 60 minutes.
Step 1: Initial Research 
Start with a fast research of Arista. Below you can see example information that may be interesting for this case study.
What type of devices does Arista produce?
What is EOS?
Where are security advisories published?
Step 2: Security Advisory
Open the web advisory from this link. Gather the following information:
CVE-ID of the vulnerability described in the advisory.
What EOS versions are considered to be vulnerable?
What hardware products are considered to be vulnerable?
Does the vulnerability require specific configuration of the asset to be exploited? Or is every asset with the specified EOS version and from the specific product series always vulnerable?
What network protocol is mentioned in the advisory?
Does the advisory provide guidance to resolve/mitigate the vulnerability?
Step 3: Version output
Below you can see an example output of the show version command run on an Arista asset. Read the output.
switch> show version
Arista DCS-7150S-64-CL-F
Hardware version:    01.01
Serial number:       JPE13120819
System MAC address:  001c.7326.fd0c

Software image version: 4.32.2F
Architecture:           i386
Internal build version: 4.32.2F-1649184.4132F.2
Internal build ID:      eeb3c212-b4bd-4c19-ba34-1b0aa36e43f1

Uptime:                 16 hours and 39 minutes
Total memory:           4017088 kB
Free memory:            1348228 kB
Answer the following questions:
What pieces of information are relevant to evaluate whether the asset is potentially vulnerable to CVE-2025-8872.
What pieces of information are irrelevant?
What pieces of information are potentially relevant? What additional research would be required?
If you identify pieces of information that would require additional research, identify the piece which you consider as the most relevant. Plan the research and perform it.
We recommend using text highlighting to mark relevant, irrelevant, and potentially relevant information.
Step 4: Vulnerability Evaluation
From what you have already learned, summarize the information:
Evidence that suggests that the asset is vulnerable.
Evidence that suggests that the asset is not vulnerable.
Evidence that is not available at the moment.
Step 5: Conclusion
If you have a vulnerable asset in a company network, what quick solution would you propose to handle this vulnerability? And what long-term solution would you propose to handle similar vulnerabilities in the future?
If you don’t have a vulnerable asset in a company network, what preemptive measure would you propose to handle this vulnerability in the future?
Part 2
Estimated time required for this part: 30 minutes.
Step 1: Additional information about CVE
Open vulnerability database of vulnerability scanner vendors, for example Rapid7 VulnDB and Tenable CVE database. Try to search for the CVE of the vulnerability. Have you learned any new information?
Check if this vulnerability is exploited in the wild using Known Exploited Vulnerabilities Catalog. What would it mean if it was?
Step 2: New Security Advisory
You will investigate another vulnerability of an Arista asset in this task. This task is similar to the previous one but it is focused on a different vulnerability.
Open the web advisory from the following link. Gather the following information:
What EOS versions are considered to be vulnerable?
What hardware products are considered to be vulnerable?
Read the output of the show version command again. In the previous vulnerability, you have identified the relevant, irrelevant, and potentially relevant pieces of information. Does this still hold for this advisory as well? If not, what changes need to be made?
From what you have already learned, summarize the information:
Evidence that suggests that the asset is vulnerable.
Evidence that suggests that the asset is not vulnerable.
Evidence that is not available at the moment.
Based on your investigation, what action would you recommend to handle the vulnerability?

