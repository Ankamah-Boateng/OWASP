# OWASP ZAP Full Web Application Scan on DVWA

**Target:** [http://172.17.0.2/dvwa/index.php](http://172.17.0.2/dvwa/index.php)

**Tool:** OWASP ZAP 2.13.0

**Environment:** DVWA running on local Docker network (172.17.0.2)

---

## 1. Objective

The goal of this exercise was to perform a full web application vulnerability scan on Damn Vulnerable Web Application (DVWA) using OWASP ZAP, identify security weaknesses, and document findings with appropriate remediation steps.

---

## 2. Methodology / Workflow

### Step 1: Environment Preparation

* DVWA was deployed and confirmed accessible at `http://172.17.0.2/dvwa/index.php`.

* OWASP ZAP was launched in **Standard Mode**.

* Browser traffic was routed through ZAP using the built-in proxy.

### Step 2: Target Setup

* The target URL was added to the **Sites** tree in ZAP.

* Application pages were manually browsed to populate the site map.

### Step 3: Spidering (Crawling)

* ZAP Spider was executed to automatically discover hidden paths, parameters, and resources.

* Results were reviewed to ensure adequate coverage of the application.

### Step 4: Active Scan

* A full **Active Scan** was launched against the DVWA target.

* ZAP tested input points for common web vulnerabilities such as injection flaws, misconfigurations, and missing security headers.

### Step 5: Results Review

* Alerts were reviewed in the **Alerts** tab.

* Each finding was analyzed based on risk level, confidence, and exploitability.

---

## 3. Key Findings

### 3.1 High-Risk Vulnerabilities

1. **Remote Code Execution – CVE-2012-1823**
 
2. **Source Code Disclosure – CVE-2012-1823**

* **Risk Level:** High

* **Confidence:** Medium

* **Affected URL:** `http://172.17.0.2/dvwa/index.php`

* **Impact:**
  Successful exploitation can lead to full server compromise.

---

### 3.2 Medium / Low-Risk Vulnerabilities

1. **Absence of Anti-CSRF Tokens**

2. **Content Security Policy (CSP) Header Not Set**

3. **Missing Anti-clickjacking Header (X-Frame-Options)**

4. **Cookies Missing HttpOnly Flag**

5. **Cookies Without SameSite Attribute**

6. **Server Version Disclosure via HTTP Headers**

7. **X-Content-Type-Options Header Missing**

8. **Authentication Request Identified**

9. **Session Management Response Identified**

10. **Hidden Files Discovered**

These findings indicate weak security hardening and poor defensive configuration.

---

## 4. Remediation Recommendations

### For Remote Code Execution (CVE-2012-1823)

* Upgrade PHP to a secure, supported version.

* Disable PHP CGI if not required.

* Properly configure `allow_url_include` and `auto_prepend_file`.

* Apply strict input validation and server-side filtering.

### For Missing Security Headers

* Implement the following HTTP headers:

  i. `Content-Security-Policy`

  ii. `X-Frame-Options`

  iii. `X-Content-Type-Options`

* Regularly review server security headers using automated tools.



### For CSRF Issues

* Implement CSRF tokens on all state-changing requests.

* Validate tokens server-side.



### For Cookie Security

* Set cookies with:

  * `HttpOnly`
  * `Secure`
  * `SameSite=Strict` or `Lax`

### General Hardening

* Remove unnecessary files and directories.

* Disable verbose server banners.

* Conduct regular vulnerability scans and penetration tests.

---

## 5. Conclusion

This scan highlights how misconfigurations and outdated components can introduce critical vulnerabilities. OWASP ZAP proved effective in identifying both high-risk exploitation paths and basic security hygiene issues. Continuous testing, patching, and secure configuration are essential for maintaining a secure web application.

---

## 6. Disclaimer

This assessment was conducted on DVWA, an intentionally vulnerable application, strictly for educational and ethical cybersecurity practice.
