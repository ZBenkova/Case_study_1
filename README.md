# Vulnerability Coverage Study Cases – Aruba & Arista

> Working notes for investigating vulnerabilities on network devices.
>
> Goal:
>
> * support answers with evidence
> * clearly separate facts from assumptions
> * explain the reasoning behind decisions
> * leave space for screenshots and command output

---

# Study Case 1 – Aruba

## Step 1: Initial Research

### What types of network devices does Aruba produce?

Aruba produces enterprise networking devices, mainly:

* Wireless access points
* Wireless LAN controllers
* Network switches
* Gateways and SD-WAN appliances
* Campus and branch networking devices
* Network management and cloud platforms

### How could HPE’s acquisition of Aruba affect the source of vulnerability information?

**Notes:**

* Aruba was acquired by HPE in 2015.
* Older vulnerability information may still be published under the Aruba name.
* Newer advisories are often published on HPE Aruba Networking websites.
* When researching vulnerabilities, it may be necessary to search both Aruba and HPE support portals.

### Does Aruba develop one or multiple operating systems for their products?

**Notes:**

* Aruba develops multiple operating systems.

**Operating systems:**

* ArubaOS – used primarily for wireless controllers, gateways, and controller-based AP deployments.
* Aruba Instant – used on Instant APs without a controller.
* AOS-CX – used on Aruba CX switch platforms.
* AOS-S (formerly ArubaOS-Switch / ProVision) – used on older switch families.

**Used for:**

| Operating System | Device Type           |
| ---------------- | --------------------- |
| ArubaOS          | Controllers, gateways |
| Aruba Instant    | Standalone APs        |
| AOS-CX           | Modern CX switches    |
| AOS-S            | Legacy switches       |

### Sources Used

* Aruba product documentation
* HPE Aruba Networking support documentation
* Aruba Central supported device list

---

## Step 2: Security Advisory

### Advisory Link

* Add the Aruba advisory URL here

### Does this advisory cover one or multiple CVEs?

* [x] Multiple CVEs

### Identified CVEs

* CVE-________
* CVE-________

### Affected Operating Systems and Versions

| Operating System | Vulnerable Versions | Notes                           |
| ---------------- | ------------------- | ------------------------------- |
| ArubaOS 8.x      | Fill from advisory  | Wireless controller OS          |
| ArubaOS 10.x     | Fill from advisory  | Newer cloud-managed deployments |
| AOS-CX / AOS-S   | Only if mentioned   | May not be affected             |

### Quote / Evidence from the Advisory

```text
Paste the exact vulnerable version statement from the Aruba advisory here.
```

### My Conclusion

* The advisory affects only the operating systems and versions explicitly listed.
* It is not possible to determine whether a device is vulnerable until both the OS family and the exact version are known.

---

## Step 3: Command Selection

### AOS-8

**Selected command:**

```text
show version
```

**Why this command is useful:**

* Displays the device model.
* Displays the ArubaOS version.
* Provides enough information to compare against the advisory.

**Does it include the device model?**

* [x] Yes

**Does it include the OS version?**

* [x] Yes

**Relevant output example:**

```text
ArubaOS Version 8.10.0.5
MODEL: Aruba7005
```

### AOS-10

**Selected command:**

```text
show version
```

**Why this command is useful:**

* Provides the current ArubaOS 10 software version.
* Identifies the exact platform or gateway model.

**Does it include the device model?**

* [x] Yes

**Does it include the OS version?**

* [x] Yes

**Relevant output example:**

```text
ArubaOS Version 10.7.0.1
MODEL: Aruba7005
```

---

## Step 4: Gathering Information Using SNMP

### What request types does SNMP support?

| Request Type | Purpose                                    |
| ------------ | ------------------------------------------ |
| GET          | Retrieve a specific value                  |
| GETNEXT      | Retrieve the next OID in the tree          |
| GETBULK      | Retrieve multiple values efficiently       |
| SET          | Change a value on the device               |
| TRAP         | Unsolicited notification from the device   |
| INFORM       | Notification that requires acknowledgement |

### What is an OID?

**Notes:**

* OID stands for Object Identifier.
* It is a unique numeric path used in SNMP to identify a specific piece of information.
* Example: system description, hostname, uptime, or interface name.

### Is there a specific OID focused on gathering the system description of a product?

* Name: sysDescr
* OID: 1.3.6.1.2.1.1.1.0
* What it returns: Vendor, product model, operating system, and version string.

### What port number is used by SNMP by default?

* Requests: UDP 161
* Trap messages: UDP 162

---

## Step 5: Reading SNMP Information

Output:

```text
ArubaOS (MODEL: Aruba7005), Version 10.7.0.1 SSR (91033)
```

### What information can be extracted from the output?

| Item        | Value     |
| ----------- | --------- |
| Vendor / OS | ArubaOS   |
| Model       | Aruba7005 |
| Version     | 10.7.0.1  |

### Does the output provide evidence that the asset is vulnerable?

* [ ] Yes
* [ ] No
* [x] Cannot determine without the advisory

### Reasoning

* The output identifies the exact operating system and version.
* Vulnerability status depends on whether version 10.7.0.1 appears in the advisory.
* The model alone is not enough to determine exposure.

### What additional information is still missing?

* The exact affected versions from the advisory.
* Whether the advisory also requires a specific feature or configuration.

---

## Step 6: Conclusion and Discussion

### Knowledge gained from this study case

* Network vendors may use several operating systems across different device families.
* The most important information for vulnerability assessment is the exact OS version.
* SNMP can sometimes provide enough information without logging into the device.

### Which sources can be used to identify the vendor and operating system of a network asset?

| Source                  | What it provides           | Requires credentials?   | Reliability    |
| ----------------------- | -------------------------- | ----------------------- | -------------- |
| show version            | Exact model and OS version | Yes                     | High           |
| SNMP sysDescr           | Model, vendor, OS version  | Usually no or read-only | Medium to High |
| Banner / web login page | Vendor or product family   | No                      | Low            |

### Which source is the quickest?

* SNMP sysDescr, if SNMP is enabled.

### Which source is the most reliable?

* The `show version` command.

### Which source requires credentials?

* The `show version` command.

### Steps to check whether the asset has a known vulnerability

1. Identify the vendor and model.
2. Identify the exact operating system and version.
3. Locate the official vendor advisory.
4. Compare the installed version to the vulnerable versions.
5. Check whether a specific feature or configuration is required.

---

# Study Case 2 – Arista

# Part 1

## Step 1: Initial Research

### What type of devices does Arista produce?

**Notes:**

* Arista Networks produces switches, routers, data center networking platforms, cloud networking products, and virtual networking appliances.

### What is EOS?

**Notes:**

* EOS stands for Extensible Operating System.
* It is Arista’s Linux-based network operating system used across most Arista devices.

### Where are security advisories published?

**Notes:**

* Arista security advisories are published on the Arista Support → Advisories & Notices → Security Advisories page.

---

## Step 2: Security Advisory

### Advisory Link

* Add the advisory URL here

### CVE-ID

```text
CVE-2025-8872
```

### What EOS versions are considered vulnerable?

* 4.34.1F and below in the 4.34.x train
* 4.33.4M and below in the 4.33.x train
* 4.32.7M and below in the 4.32.x train
* 4.31.8M and below in the 4.31.x train
* All releases before 4.31.x

### What hardware products are affected?

* All listed EOS-based hardware platforms and virtual appliances.
* The platform is only affected if it runs a vulnerable EOS version.

### Does exploitation require a specific configuration?

* [x] Yes

**If yes, what configuration is required?**

* OSPFv3 must be enabled or configured.
* If OSPFv3 is not configured, the device is not exposed.

### What network protocol is mentioned in the advisory?

* OSPFv3

### Does the advisory provide mitigation or remediation guidance?

* [x] Yes

**If yes, what guidance is provided?**

* Upgrade to a fixed EOS release.
* Disable OSPFv3 temporarily if it is not required.

### Quote / Evidence from the Advisory

```text
“If OSPFv3 is not configured there is no exposure to this issue.”
```

---

## Step 3: Version Output Analysis

```text
switch> show version
Arista DCS-7150S-64-CL-F
...
Software image version: 4.32.2F
```

### Relevant Information

| Information                     | Why it is relevant                            |
| ------------------------------- | --------------------------------------------- |
| Arista DCS-7150S-64-CL-F        | Confirms the hardware platform                |
| Software image version: 4.32.2F | Needed to compare against vulnerable versions |

### Potentially Relevant Information

| Information            | What additional research is required                |
| ---------------------- | --------------------------------------------------- |
| Architecture: i386     | Determine whether architecture matters for the CVE  |
| Internal build version | Check whether the advisory references build numbers |

### Irrelevant Information

| Information   | Why it is not relevant               |
| ------------- | ------------------------------------ |
| Serial number | Does not affect vulnerability status |
| Uptime        | Not related to the CVE               |
| Memory values | Not related to the vulnerability     |

### Most Important Information for Further Research

* The software image version 4.32.2F.

### Research Plan

1. Compare 4.32.2F to the vulnerable versions listed in the advisory.
2. Confirm whether the 7150 series is affected.
3. Determine whether OSPFv3 is configured.
4. Identify the fixed version to recommend.

---

## Step 4: Vulnerability Evaluation

### Evidence suggesting that the asset is vulnerable

* The 7150 series is listed as affected hardware.
* EOS version 4.32.2F is lower than 4.32.7M.
* The advisory states that 4.32.x versions below the fixed release are vulnerable.

### Evidence suggesting that the asset is not vulnerable

* The installed version is 4.32.2F, not 4.32.2M, so train differences may matter.
* The device is only vulnerable if OSPFv3 is enabled.

### Evidence that is not currently available

* Whether OSPFv3 is configured on the switch.
* Whether the advisory affects only M-train releases or all 4.32.x releases.

### Assumptions

* Assumption: The device may be vulnerable.
* Reason: The version appears older than the fixed version and the hardware is affected, but configuration has not been verified.

---

## Step 5: Conclusion

### If the asset is vulnerable, what quick solution would I propose?

* Upgrade to the first fixed EOS version.
* Temporarily disable OSPFv3 if not needed.

### What long-term solution would I propose for similar vulnerabilities in the future?

* Maintain an inventory of device versions.
* Regularly monitor vendor advisories.
* Use automated vulnerability tracking.

### If the asset is not currently vulnerable, what preventive measure would I propose?

* Continue monitoring for future EOS advisories.
* Keep OSPFv3 disabled unless required.

---

# Part 2

## Step 1: Additional Information About the CVE

### Rapid7 / Tenable

**What new information did I learn?**

* Third-party scanners often provide CVSS scores and exploitation details.
* They may explain whether the vulnerability can be detected remotely.
* They may include temporary mitigation steps before a patch is available.

### KEV – Known Exploited Vulnerabilities

* [ ] The CVE is listed in KEV
* [x] The CVE is not listed in KEV

### What would it mean if the CVE was listed in KEV?

* The vulnerability is being actively exploited.
* The issue should be treated as high priority.

---

## Step 2: New Arista Security Advisory

### Advisory Link

* [https://www.arista.com/zh/support/advisories-notices/security-advisory/23120-security-advisory-0132](https://www.arista.com/zh/support/advisories-notices/security-advisory/23120-security-advisory-0132)

### What EOS versions are vulnerable?

| EOS Version                                      | Status     |
| ------------------------------------------------ | ---------- |
| Earlier affected releases listed in the advisory | Vulnerable |
| Patched release listed by Arista                 | Fixed      |

### What hardware is affected?

* Only specific EOS platforms listed in the advisory.
* Some older series are explicitly excluded.
* Virtual appliances may also be affected.

### Does the same classification of `show version` information still apply?

* [x] Yes

### Evidence suggesting that the asset is vulnerable

* The device model may appear in the affected hardware list.
* The installed EOS version may be older than the fixed version.

### Evidence suggesting that the asset is not vulnerable

* The advisory explicitly excludes several product families.
* The switch may not run a vulnerable release train.

### What information is still missing?

* The exact EOS version installed on the asset.
* Whether the model appears in the affected list.

### Recommended Action

* Compare the installed EOS version to the fixed version.
* Upgrade if the device is within the vulnerable range.
* Document the finding and retain the command output as evidence.

---

# Final Notes

### What was the most difficult part of the investigation?

* Determining whether the version train and build type were actually vulnerable.
* Distinguishing confirmed facts from assumptions when configuration details were missing.

### What information was the easiest to obtain?

* The model and operating system version from `show version`.

### What would I do differently next time?

* Gather both the advisory and the device output before starting analysis.
* Check configuration requirements earlier in the investigation.
