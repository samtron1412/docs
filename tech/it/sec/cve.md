[TOC]

# Overview
- The Common Vulnerabilities and Exposures (CVE) system provides a reference-method for publicly known information security vulnerabilities and exposures.
- The **National Cybersecurity FFRDC**, operated by the **MITRE Corporation**, maintains the system, with funding from the **National Cyber Security Division** of the **United States Department of Homeland Security**.
- CVE IDs are listed on MITRE's system as well as in the US **National Vulnerability Database**.
- Requesting a CVE ID: using the [CVE Request Form][4]

# CVE identifiers
- MITRE Corporation's documentation defines CVE Identifiers as unique, common identifiers for publicly known information-security vulnerabilities in publicly released software packages.
- The assignment of a CVE identifier is not a guarantee that it will become an official CVE entry (e.g. a CVE may be improperly assigned to an issue which is not a security vulnerability, or which duplicates and existing entry).
- CVEs are assigned by a CVE Numbering Authority (CNA); there are three primary types of CNA:
	+ The MITRE Corporation functions as Editor and Primary CNA.
	+ Various CNAs assign CVE numbers for their own products (e.g. Microsoft, Oracle, HP, Red Hat, etc.)
	+ A third party coordinator such as CERT Coordination Center may assign CVE numbers for products not covered by other CNAs.
- CVE numbers may not appear in the MITRE or NVD CVE databases for some time due to issues that are embargoed (the CVE number has been assigned but the issues has not been made public), or in cases where the entry is not researched and written up by MITRE due to resource issues.

# CVE data fields
- **Description**: This is a standardized text description of the issue(s). One common entry is: `** RESERVED ** This candidate has been reserved by an organization or individual that will use it when announcing a new security problem. When the candidate has been publicized, the details for this candidate will be provided.` This means that the entry number has been reserved by MITRE for an issue or a CNA has reserved the number.
- **References**: This is a list of URLs and other information (such as vendor advisory numbers) for this issue.
- **Date Entry Created**: This is the date the entry was created. It's not the date when this issue was discovered.

# Famous CVEs
1. [heartbleed][2]
2. [shellshock][3]

# References
1. [Wikipedia - Common Vulnerabilities and Exposures][1]
2. [Wikipedia - Heartbleed][2]
3. [Wikipedia - Shellshock][3]
4. [CVE Request Form][4]

[1]: https://en.wikipedia.org/wiki/Common_Vulnerabilities_and_Exposures "Wikipedia - Common Vulnerabilities and Exposures"
[2]: https://en.wikipedia.org/wiki/Heartbleed "Wikipedia - Heartbleed"
[3]: https://en.wikipedia.org/wiki/Shellshock_(software_bug) "Wikipedia - Shellshock"
[4]: https://cveform.mitre.org/ "CVE Request Form"
