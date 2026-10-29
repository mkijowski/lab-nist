# Lab 5 : CEG3400

### NIST Vulnerability Taxonomies

Table of Contents:

* [Background](#background)
* [Objectives](#objectives)
* [Preparation](#preparation)
* [Task 1: Inventory](#task-1---inventory)
* [Task 2: CPE](#task-2---cpe)
* [Task 3: CWE](#task-3---cwe)
* [Task 4: CVE](#task-4---cve)

---

### Background

The purpose of this lab is to familiarize you with the National Vulnerability Database (NVD),
run by NIST (the National Institute of Standards and Technology), and the naming standards
that go with it.

Security professionals use the NVD and related catalogs to find, analyze, and fix
vulnerabilities faster.  Most organizations automate this, but in this lab you will do it by
hand, using a piece of software *you* wrote that had a vulnerability.  (Don't worry, almost
everyone has one.  Many common coding and scripting mistakes lead to a vulnerability.)

---

### Objectives

By the end of this lab you should be able to:

* Describe a software environment using standard CPE names
* Explain how CPE, CWE, CVE, CVSS, KEV, and EPSS relate to each other
* Decide which vulnerabilities to fix first, and defend that decision
* Connect a weakness in your own code to the real-world vulnerabilities it causes
* Write a vulnerability report (CVE record) that someone else could act on

---

### Preparation

* Review the CPE, CWE, CVE, CVSS, KEV, and EPSS slides from lecture,
  especially *Putting it together: what do I patch first?*

Read the following:

* [2025 CWE Top 25 Most Dangerous Software Weaknesses](https://cwe.mitre.org/top25/archive/2025/2025_cwe_top25.html)
* [2025 Top 10 KEV Weaknesses](https://cwe.mitre.org/top25/archive/2025/2025_kev_list.html)
* [Semantic Versioning 2.0.0](https://semver.org/)

Tools you will use:

* [NVD CPE search](https://nvd.nist.gov/products/cpe/search)
* [NVD CVE search](https://nvd.nist.gov/vuln/search) and [CVE.org](https://www.cve.org/)
* [CISA Known Exploited Vulnerabilities (KEV) catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog)
* [FIRST EPSS lookup](https://api.first.org/data/v1/epss?cve=CVE-2021-44228)
  (change the CVE number at the end of the URL)
* [FIRST CVSS v4.0 calculator](https://www.first.org/cvss/calculator/4.0)

**Before you start:** Tasks 2, 3, and 4 all use the same program you wrote.  Skim the
Top 25 list and pick your program and its weakness first, then work through the tasks in order.

---

### Task 1 - Inventory

CPE stands for Common Platform Enumeration.  It is the standard way to name a specific
piece of software or hardware.  The first step in any good security posture is knowing
what you are defending.

Using the [CPE search demonstrated in class](https://nvd.nist.gov/products/cpe/search),
find 5 CPE names for software installed on your laptop.  These 5 must include:

* An operating system
* A web browser
* At least 2 programs related to CS/CEG/IT (compiler, IDE, `git`, Python, etc.)
* One more of your choice, class related or personal

List each one in CPE 2.3 format (`cpe:2.3:[aoh]:vendor:product:version:...`), and match the
version to what is actually installed when you can.  You will reuse these 5 CPEs in Lab 6.

---

### Task 2 - CPE

Task 1 showed you what a [well formed CPE name](https://nvlpubs.nist.gov/nistpubs/legacy/ir/nistir7695.pdf)
looks like.  Now write one for software that doesn't have one yet.

Choose a program you have written that has one of the weaknesses from the 2025 CWE Top 25.
Write a well formed CPE 2.3 name for it, using a made up vendor name (you!) and product name.
The version must be in sem-ver format (for example `1.4.2`).

Then explain:

* Each field you filled in, and why you chose that value
* Each field you left as a wildcard (`*`) or not applicable (`-`), and why

---

### Task 3 - CWE

CWE stands for Common Weakness Enumeration, a list of software and hardware weakness types
maintained by MITRE.  A CVE is one specific bug.  A CWE is the *type* of mistake behind it.

1. Link to your chosen CWE and summarize it in your own words.
2. Explain what you put into your code, how it relates to this CWE, and what an attacker could
   have done with it.
3. Why do you think the mistake made it into your code?  (Didn't know about it, deadline,
   copied from an example, trusted user input, something else?)
4. How would you fix it?  Use the *Potential Mitigations* section of the CWE page and say
   which mitigation fits your code best.
5. **Triage.**  Find 3 real CVEs caused by this same CWE.  Try to include at least one that
   is in the KEV catalog.  For each CVE, record:
   * The CVE ID (linked) and a one sentence description
   * Its CVSS score, and the CVSS version that score uses
   * Whether it is in the KEV catalog
   * Its current EPSS score

   You are responsible for patching all 3 and can only patch one today.  Rank them in the
   order you would patch them and defend your ranking.  Does your order match a ranking by
   CVSS alone?  Why or why not?

---

### Task 4 - CVE

CVE stands for Common Vulnerabilities and Exposures.  In this task you will write a CVE record
for the vulnerability in your own program.

Only a CVE Numbering Authority (CNA) can assign a CVE ID.  For this assignment, I (Matt
Kijowski) am the only CNA for your software, so use `CVE-2026-NNNNN` as a placeholder ID.

Your CVE record must include at least:

* **Affected product(s) and version(s)**: use your CPE from Task 2
* **Vulnerability type and root cause**: reference your CWE from Task 3
* **Description**: what the bug is and what an attacker could do with it, in 2 to 4 sentences
* **Impact**: a CVSS v4.0 base score *and* vector string, from the
  [FIRST CVSS v4.0 calculator](https://www.first.org/cvss/calculator/4.0)
* **Reference**: at least one public reference.  Link to your own GitHub lab repository.

Then defend your CVSS score: explain why you chose each metric value in the calculator.

Since April 2026 the NVD no longer adds its own CVSS score to most new CVEs.  For most new CVEs,
the score the CNA publishes is the only one anyone sees.  Score it like someone will patch (or
ignore) it based on your number, because in the real world they will.
