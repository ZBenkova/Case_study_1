# Vulnerability Coverage Study Cases – Aruba & Arista

> Working notes template for investigating vulnerabilities on network devices.
>
> Goal:
>
> * support answers with evidence
> * clearly separate facts from assumptions
> * explain the reasoning behind decisions
> * leave space for my own findings and screenshots

---

# Study Case 1 – Aruba

## Step 1: Initial Research

### What types of network devices does Aruba produce?

**Notes:**

*
*
*

### How could HPE’s acquisition of Aruba affect the source of vulnerability information?

**Notes:**

*
*
*

### Does Aruba develop one or multiple operating systems for their products?

**Notes:**

* Operating system:
* Used for:
* Additional OS:

### Sources Used

* Link:
* Link:
* Link:

---

## Step 2: Security Advisory

### Advisory Link

*

### Does this advisory cover one or multiple CVEs?

* [ ] One CVE
* [ ] Multiple CVEs

### Identified CVEs

* CVE-
* CVE-

### Affected Operating Systems and Versions

| Operating System | Vulnerable Versions | Notes |
| ---------------- | ------------------- | ----- |
|                  |                     |       |
|                  |                     |       |
|                  |                     |       |

### Quote / Evidence from the Advisory

```text
paste quote here
```

### My Conclusion

*
*

---

## Step 3: Command Selection

### AOS-8

**Selected command:**

```text
```

**Why this command is useful:**

*
*

**Does it include the device model?**

* [ ] Yes
* [ ] No

**Does it include the OS version?**

* [ ] Yes
* [ ] No

**Relevant output example:**

```text
```

### AOS-10

**Selected command:**

```text
```

**Why this command is useful:**

*
*

**Does it include the device model?**

* [ ] Yes
* [ ] No

**Does it include the OS version?**

* [ ] Yes
* [ ] No

**Relevant output example:**

```text
```

---

## Step 4: Gathering Information Using SNMP

### What request types does SNMP support?

| Request Type | Purpose |
| ------------ | ------- |
|              |         |
|              |         |
|              |         |

### What is an OID?

**Notes:**

*
*

### Is there a specific OID focused on gathering the system description of a product?

* Name:
* OID:
* What it returns:

### What port number is used by SNMP by default?

* Requests:
* Trap messages:

---

## Step 5: Reading SNMP Information

Output:

```text
ArubaOS (MODEL: Aruba7005), Version 10.7.0.1 SSR (91033)
```

### What information can be extracted from the output?

| Item        | Value |
| ----------- | ----- |
| Vendor / OS |       |
| Model       |       |
| Version     |       |

### Does the output provide evidence that the asset is vulnerable?

* [ ] Yes
* [ ] No
* [ ] Cannot determine without the advisory

### Reasoning

*
*
*

### What additional information is still missing?

*
*

---

## Step 6: Conclusion and Discussion

### Knowledge gained from this study case

*
*
*

### Which sources can be used to identify the vendor and operating system of a network asset?

| Source | What it provides | Requires credentials? | Reliability |
| ------ | ---------------- | --------------------- | ----------- |
|        |                  |                       |             |
|        |                  |                       |             |
|        |                  |                       |             |

### Which source is the quickest?

*

### Which source is the most reliable?

*

### Which source requires credentials?

*

### Steps to check whether the asset has a known vulnerability

1.
2.
3.
4.
5.

---

---

# Study Case 2 – Arista

# Part 1

## Step 1: Initial Research

### What type of devices does Arista produce?

**Notes:**

*
*
*

### What is EOS?

**Notes:**

*
*

### Where are security advisories published?

**Notes:**

*
*

### Sources Used

*
*
*

---

## Step 2: Security Advisory

### Advisory Link

*

### CVE-ID

```text
CVE-
```

### What EOS versions are considered vulnerable?

| EOS Version | Status     |
| ----------- | ---------- |
|             | Vulnerable |
|             | Fixed      |

### What hardware products are affected?

*
*
*

### Does exploitation require a specific configuration?

* [ ] Yes
* [ ] No

**If yes, what configuration is required?**

*
*

### What network protocol is mentioned in the advisory?

*

### Does the advisory provide mitigation or remediation guidance?

* [ ] Yes
* [ ] No

**If yes, what guidance is provided?**

*
*

### Quote / Evidence from the Advisory

```text
paste quote here
```

---

## Step 3: Version Output Analysis

```text
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
```

### Relevant Information

| Information | Why it is relevant |
| ----------- | ------------------ |
|             |                    |
|             |                    |

### Potentially Relevant Information

| Information | What additional research is required |
| ----------- | ------------------------------------ |
|             |                                      |
|             |                                      |

### Irrelevant Information

| Information | Why it is not relevant |
| ----------- | ---------------------- |
|             |                        |
|             |                        |

### Most Important Information for Further Research

*

### Research Plan

1.
2.
3.
4.

---

## Step 4: Vulnerability Evaluation

### Evidence suggesting that the asset is vulnerable

*
*
*

### Evidence suggesting that the asset is not vulnerable

*
*
*

### Evidence that is not currently available

*
*

### Assumptions

> Clearly mark anything that has not been confirmed.

* Assumption:
* Reason:

---

## Step 5: Conclusion

### If the asset is vulnerable, what quick solution would I propose?

*
*
*

### What long-term solution would I propose for similar vulnerabilities in the future?

*
*
*

### If the asset is not currently vulnerable, what preventive measure would I propose?

*
*

---

# Part 2

## Step 1: Additional Information About the CVE

### Rapid7 / Tenable

**What new information did I learn?**

*
*
*

### KEV – Known Exploited Vulnerabilities

* [ ] The CVE is listed in KEV
* [ ] The CVE is not listed in KEV

### What would it mean if the CVE was listed in KEV?

*
*

---

## Step 2: New Arista Security Advisory

### Advisory Link

*

### What EOS versions are vulnerable?

| EOS Version | Status     |
| ----------- | ---------- |
|             | Vulnerable |
|             | Fixed      |

### What hardware is affected?

*
*
*

### Does the same classification of `show version` information still apply?

* [ ] Yes
* [ ] No

### If not, what changes?

| Information | New Classification | Reason |
| ----------- | ------------------ | ------ |
|             |                    |        |
|             |                    |        |

### Evidence suggesting that the asset is vulnerable

*
*

### Evidence suggesting that the asset is not vulnerable

*
*

### What information is still missing?

*
*

### Recommended Action

*
*
*

---

# Final Notes

### What was the most difficult part of the investigation?

*
*

### What information was the easiest to obtain?

*
*

### What would I do differently next time?

*
*
