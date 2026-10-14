Version: NAFATH-V4
Track: Networking

## Overview
A national service provider depends on software, artificial intelligence (AI) models, mobile applications, networks, and data. If secrets are stored inside the code, anyone who reads it can steal them. AI models can be manipulated by attackers who feed them false inputs or corrupt their training data. A weak mobile application can allow attackers to access the user's data. Even if all these elements are secure, internet traffic can be rerouted through an attacker's network. One vulnerable component, such as the Log4j library behind Log4Shell, can impact thousands of systems at once. A list of software components, called a Software Bill of Materials (SBOM), helps us understand what is included in our products. A weakness in any one part can threaten all the others, so every part must be checked.

## Software
The Twelve-Factor App says that configuration, such as database addresses and credentials, should be stored in environment variables, not in the code. Configuration changes between environments such as development and production, while the code stays the same. Keeping secrets in code is risky because code is often shared and published, so the secrets leak with it. A good test is whether the code could be made open source at any moment without exposing any credentials.
Resource: The Twelve-Factor App, III. Config 
- https://12factor.net/config

## AI
NIST's taxonomy groups adversarial attacks on machine learning into main categories. Evasion attacks happen after deployment: the attacker alters an input, such as an image, so the model gives a wrong output. Poisoning attacks happen during training: the attacker corrupts training data or the model so it learns wrong behavior. Privacy attacks try to extract sensitive training data or model information. For generative AI, NIST lists misuse attacks. The categories differ mainly in attack timing and attacker goal.
Resource: Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations (NIST AI 100-2e2025) - https://doi.org/10.6028/NIST.AI.100-2e2025

## Mobile
The OWASP Mobile Application Security Verification Standard (MASVS) sets baseline security and privacy requirements for mobile apps. Its controls are grouped into areas such as storage, cryptography, network, platform, code, resilience and privacy. It is used as a metric to compare apps, as guidance during development and testing, and in procurement. Testers verify an app by checking each requirement using the OWASP Mobile Application Security Testing Guide (MASTG).
Resource: OWASP Mobile Application Security Verification Standard (MASVS) 
- https://github.com/OWASP/masvs
## Networking
BGP route hijacking happens when an AS falsely announces IP prefixes it does not own, often more specific ones that routers prefer, so other networks send traffic through the attacker. RPKI lets prefix holders publish signed Route Origin Authorizations, and routers use them to mark origin announcements as valid, invalid or not found. RPKI validates only the origin AS, so it does not protect against forged AS paths or route leaks.
Resource: RFC 6811: BGP Prefix Origin Validation 
- https://www.rfc-editor.org/rfc/rfc6811

## Cybersecurity
Log4Shell was a flaw in Apache Log4j 2 that let an unauthenticated attacker run code on a server by making it log a crafted string that triggered a JNDI lookup to an attacker-controlled server. It scored the maximum CVSS 10.0, because it was remotely exploitable, easy to use, and Log4j is embedded in countless applications. Version 2.15.0 patched it, but the patch was incomplete, so 2.16.0 disabled JNDI by default.
Resource: CVE-2021-44228 Detail, National Vulnerability Database (NIST) 
- https://nvd.nist.gov/vuln/detail/CVE-2021-44228

## Data
A Software Bill of Materials (SBOM) is a formal record of the components used to build software and their supply chain relationships. NTIA's minimum data fields are: supplier name, component name, component version, other unique identifiers, dependency relationship, author of SBOM data, and timestamp. With an SBOM, an organisation can quickly find which products contain a vulnerable component such as Log4j.
Resource: The Minimum Elements For a Software Bill of Materials (SBOM), NTIA 
- https://www.ntia.doc.gov/report/2021/minimum-elements-software-bill-materials-sbom
   
## Misconception in My Track
A common belief is that once RPKI is deployed, BGP hijacking is solved. In fact, RPKI route origin validation only checks that the origin AS of a route is authorised to announce that prefix. It does not validate the rest of the AS path, so an attacker can still forge a route that begins with the legitimate origin AS. RFC 6811 describes the system as closer to protection against misconfiguration than strong security. Evidence: Section 6, Security Considerations, of RFC 6811.

## Open Question
How widely do major networks actually enforce route origin validation today, and what would it take to add reliable validation of the full AS path?
