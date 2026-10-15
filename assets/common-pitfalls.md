# Common pitfalls: what gets rejected, and how to score honestly

These are general principles that hold across most programs. They are distilled from HackerOne's published standards, which are the authoritative and current version. Check the links, do not trust a copy: policy changes, and the pages below are kept up to date.

- Common reasons reports are closed as invalid: [Core ineligible findings](https://docs.hackerone.com/en/articles/8494488-core-ineligible-findings)
- How severity is meant to be scored: [Detailed platform standards](https://docs.hackerone.com/en/articles/8369826-detailed-platform-standards)

[Back to the one-pager](../README.md)

---

## Usually not a bug on its own

The items below are commonly closed as invalid. They can be valid, but only with clear, demonstrated impact. If you report one of these, lead with the real-world impact you actually showed, or expect it to be closed.

### Needs an unlikely interaction or circumstance

- **Self-XSS or self-DoS**, unless you can use it against another account.
- **Tabnabbing** and **broken-link hijacking**.
- **Content spoofing** and **text injection**.
- Issues that only affect **end-of-life browsers or operating systems**.
- Attacks that need **physical access to the device**, unless that is explicitly in scope.

### No demonstrated real-world impact

- **Clickjacking** on a page with no sensitive action.
- **CSRF** on a form with no sensitive action, for example logout.
- **Permissive CORS** with no impact shown.
- **Version or banner disclosure**, descriptive error messages or headers.
- **CSV injection**.
- **Open redirect**, unless you chain it into additional impact.

### Optional hardening, not a vulnerability

- Missing **HttpOnly** or **Secure** cookie flags.
- Opinions on **Content-Security-Policy** configuration.
- **SSL/TLS** configuration, and lack of **SSL pinning**.
- Lack of **jailbreak detection** in mobile apps.
- Optional email security such as **SPF, DKIM or DMARC**.
- **Most rate-limiting** issues.

### Hazardous, never test unless explicitly authorized

- **Denial of service** (DoS, DDoS) or anything that can affect availability.
- **Social engineering** of staff or users (phishing, support requests).
- **Noisy or spammy** attacks (flooding notifications or forms).
- Attacks against **physical facilities**.

---

## Severity you can defend

Score what you actually demonstrated, not what you imagine could happen. A few rules that trip people up:

- **IDOR with unpredictable IDs.** If the identifier is hard to guess (for example a random UUID), exploitation is harder, so severity should stay lower by default. Only argue for a higher score if you can show a reliable, repeatable way to obtain the IDs, for example they leak in an API response, in the HTML, or follow an enumerable pattern.
- **Self-sign-up.** If anyone can create an account with no other privileges needed, then "privileges required" is none. Do not treat an account you signed up for yourself as a meaningful barrier.
- **Deleting data.** Deletion affects integrity, not availability. Score integrity by how much you could delete, and leave availability at none unless you actually took the service down.
- **Sensitive personal data.** Direct access to many users' sensitive personal data over the internet is critical. The moment you confirm you can reach real personal data, stop testing and report it. Do not pull more than you need to prove the point.

The common thread: every number and every claim should trace back to something you observed and can explain. If you cannot defend the score, lower it.
