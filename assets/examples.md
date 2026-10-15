# Three reports, one bug

All three reports describe the same fictional bug in a fictional app called **InvoiceFlow** (`invoiceflow.test`). The domain ends in `.test`, a reserved extension that never resolves to a real site.

For each report, ask yourself:

1. Would I be happy to receive this on a busy day?
2. Could a stranger follow the steps without asking anything?
3. **Could the author explain and defend every sentence?**

Each report below is also a standalone file you can paste straight into the reviewer, handy for a live demo:

- Report 1 (polished but unfollowable): [`drafts/report-1-polished.md`](drafts/report-1-polished.md)
- Report 2 (dramatic): [`drafts/report-2-dramatic.md`](drafts/report-2-dramatic.md)
- Report 3 (strong): [`drafts/report-3-strong.md`](drafts/report-3-strong.md)

[Back to the one-pager](../README.md)

---

## Report 1

> **Title:** Comprehensive Analysis of a Critical Authorization Vulnerability Affecting the Invoice Management Ecosystem
>
> **Executive Summary:** During a thorough security assessment, a critical vulnerability was identified in the InvoiceFlow invoice management ecosystem. This vulnerability could potentially allow malicious actors to compromise the confidentiality, integrity and availability of sensitive data across the entire platform.
>
> **Steps to Reproduce:**
> 1. Navigate to the application.
> 2. Authenticate using valid credentials.
> 3. Locate the vulnerable endpoint `/api/v2/invoices/export`.
> 4. Manipulate the relevant parameter.
> 5. Observe the unauthorized data disclosure.
>
> **Impact:** This could lead to severe financial and reputational damage, regulatory fines and loss of customer trust. **CVSS 9.8 (Critical).**
>
> **Recommendation:** Implement robust access controls and follow industry best practices.

<details>
<summary>What to notice in Report 1</summary>

- **Polished, but not followable.** Which URL? Which account? Which password? Which parameter, and to what value?
- **An endpoint nobody checked.** `/api/v2/invoices/export` does not exist in the app. The real URL is `/invoice/1042`.
- **Claims that were never shown.** "Integrity and availability" and "the entire platform" were not demonstrated. Only one invoice can be read.
- **A severity score without reasoning.** CVSS 9.8 for a bug that needs a login and only reads data does not add up.
- **Generic impact and recommendation.** "Best practices" tells the developer nothing.
- **The test:** could the author defend every sentence if the triager called? Most likely not step 3, the severity or the "entire platform" claim.

</details>

---

## Report 2

> **Title:** HELP!!! HACKED!!! CRITICAL BUG
>
> Hi team, I found a super serious bug on your site. Hackers can steal everything with this!!! I give it a 10 out of 10. You need to fix this immediately.
>
> It is somewhere around the invoices or maybe the account, I am not sure. I tested it and it worked. See attachment for proof.
>
> I have a lot of other reports waiting so I would like a quick answer. How much bounty do I get for this? If you do not pick this up quickly I will make it public.
>
> Regards

<details>
<summary>What to notice in Report 2</summary>

- **Dramatic, vague title** with no vulnerability type or component.
- **No steps, no URL, no account.**
- **Unsure about the location** ("somewhere around... I am not sure").
- **No impact**, only "hackers can steal everything".
- **Inflated severity** ("10 out of 10") with no reasoning.
- **"See attachment"**, but there is no attachment.
- **Pressure and a threat:** urgency, bounty questions and "I will make it public".
- Usually this comes from someone who is excited, new or stressed. The fix is easy. See Report 3.

</details>

---

## Report 3

> **Title:** Access to other accounts' invoices via editable invoice number in URL (IDOR) on InvoiceFlow
>
> **Summary and impact:**
> A logged-in user can view other accounts' invoices by changing the invoice number in the URL. I confirmed this with my own two test accounts: logged in as one, I opened an invoice that belongs to the other, and the page showed that account holder's name, billing address and invoice lines. On production this same flaw would expose real customers' invoices to any logged-in user, so it is a breach of the confidentiality of customer data.
>
> **Steps to reproduce:**
> 1. Go to `https://invoiceflow.test/login` and log in as my own test account `ana@example.test`. (A throwaway test account I created myself; I will share the password through the program's secure channel rather than in this report.)
> 2. In the menu choose **My invoices** and open invoice 1042, which belongs to Ana. The URL is now `https://invoiceflow.test/invoice/1042`.
> 3. In the address bar, change `1042` to `1043` and press Enter.
> 4. Invoice 1043 is displayed. It belongs to my second test account `bob@example.test`, not to Ana. I confirmed this by logging in as Bob separately and seeing the same invoice under **My invoices**.
>
> **What I tested and did not test:** both accounts are my own, so no real customer data was accessed; this was read-only; logged out, `/invoice/1043` sends me to the login page.
>
> **Expected behavior:** An "Access denied" message.
> **Actual behavior:** The full invoice of the other account is displayed.
>
> **Severity reasoning:** a login is required and I showed read access only. The invoice number is a short sequential integer (1042 to 1043), so other invoices are easy to reach by changing it. My own assessment is CVSS 3.1 `AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N` (6.5, Medium); the program may rate it under its own model.
>
> **Recommendation:** Verify server-side that the logged-in user owns the requested invoice.

<details>
<summary>What to notice in Report 3</summary>

- **Specific title** with the vulnerability type, component and impact.
- **Impact in plain language**, matching exactly what was shown.
- **Steps with an account, full URLs and exact values.** A stranger could follow them in ten seconds.
- **Ownership is proven, not assumed.** The author uses two of their own test accounts and confirms whose invoice 1043 is, so there is no doubt and no real customer data was touched.
- **The login is fake on purpose.** `ana@example.test` and `bob@example.test` are throwaway accounts on a reserved `.test` domain, so they are safe to show here. The password is kept out of the report and shared through the program's secure channel. In a real report, use your own test accounts and keep live credentials out of any AI tool.
- **Severity is argued, not asserted.** A login is required and access was read-only, so the author lands on Medium with a vector, instead of reaching for Critical.
- **One finding**, a short recommendation and a calm tone.
- **The test:** the author was there. Every step is something they did and saw, so they can explain and defend every sentence.

</details>

---

## What a good report is

1. **Specific.** Exact URL, account, value.
2. **Reproducible.** A stranger could follow it.
3. **Honest about impact.** What you showed, not what you imagine.
4. **Owned.** You can explain and defend every sentence.

**Use AI. Own every sentence.**
