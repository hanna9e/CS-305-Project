# CS-305-Project

### Artifact Submitted
**Artemis Financial Practices for Secure Software Report** (Project Two)



### Client Summary

Artemis Financial is a financial services company that needed a security review of their Spring Boot web application. The ask was to assess the existing codebase for vulnerabilities and then implement secure communication via HTTPS/SSL. Specifically, that meant generating a PKCS12 keystore, configuring the Spring Boot app to serve over HTTPS, verifying file integrity with SHA-256 checksums, and running an OWASP dependency-check scan to surface any known CVEs in third-party libraries.



### What I Did Well / Why Secure Coding Matters

The area where I felt most confident was the implementation side such as generating the keystore with `keytool`, wiring it into `application.properties`, and getting the app running on HTTPS. I also took the OWASP scan results rather than just listing CVEs, I looked at whether each flagged dependency was actually in the execution path and assessed realistic risk.

Secure coding matters because vulnerabilities in financial software are serious. A SQL injection or an expired/self-signed cert that gets ignored in prod can expose customer financial data, trigger regulatory penalties, and destroy the trust that a financial services company depends on.



### What Was Challenging or Helpful

The OWASP dependency-check plugin was the most frustrating part, NVD API rate limits and version compatibility issues caused me to spend too much time troubleshooting before getting a scan output. That friction was actually useful though, it forced me to understand how the tool works the way it does rather than just clicking run and reading a report. Understanding the NVD CVE data source, how suppressing files work, and how to interpret false positives is knowledge that transfers directly to professional security tooling.



### Increasing Layers of Security / Future Approach

For this project, security layers included: HTTPS enforcement, certificate-based authentication via the keystore, SHA-256 checksum verification for file integrity, and dependency scanning. Going forward, I'd approach vulnerability assessment in tiers — automated scanning, static analysis, and manual code review for flaws that scanners miss.



#### Verifying Functionality and Security After Refactoring

After implementing SSL and refactoring the Spring Boot configuration, I verified functionality by confirming the app launched without errors, the HTTPS endpoint was working, and the browser showed a valid (self-signed, in this case) certificate. To check for newly introduced vulnerabilities, I re-ran the OWASP dependency-check scan after my `pom.xml` changes to make sure no new CVEs were introduced through updated or added dependencies. I also reviewed the keystore configuration to avoid common misconfigurations like wrong alias, wrong password format or wrong store type.


### Useful Resources and Tools

- **`keytool`** (JDK built-in) — certificate and keystore generation
- **OWASP Dependency-Check Maven plugin** — automated CVE scanning
- **Spring Boot `application.properties`** SSL configuration
- **SHA-256 via `MessageDigest`** — programmatic checksum verification
- **OWASP Top 10** — conceptual framework for categorizing and prioritizing vulnerabilities

All of these are directly applicable to real-world secure backend development. The OWASP tooling in particular is standard in professional Java/Spring shops.



## What I Would Show Future Employers

The Project Two report and the working Spring Boot application with HTTPS configured. Together they demonstrate that I can do more than identify vulnerabilities on paper, I can implement a fix, verify it didn't break anything, scan for regressions, and document the reasoning behind it. That combination of practical implementation and written communication is what's actually useful in a security engineering role. I'd also highlight the checksum verification code specifically since it shows understanding of cryptographic integrity concepts at the code level.
