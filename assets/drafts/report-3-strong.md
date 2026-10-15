Title: Access to other accounts' invoices via editable invoice number in URL (IDOR) on InvoiceFlow

Summary and impact:
A logged-in user can view other accounts' invoices by changing the invoice number in the URL. I confirmed this with my own two test accounts: logged in as one, I opened an invoice that belongs to the other, and the page showed that account holder's name, billing address and invoice lines. On production this same flaw would expose real customers' invoices to any logged-in user, so it is a breach of the confidentiality of customer data.

Steps to reproduce:
1. Go to https://invoiceflow.test/login and log in as my own test account ana@example.test. (A throwaway test account I created myself; I will share the password through the program's secure channel rather than in this report.)
2. In the menu choose "My invoices" and open invoice 1042, which belongs to Ana. The URL is now https://invoiceflow.test/invoice/1042.
3. In the address bar, change 1042 to 1043 and press Enter.
4. Invoice 1043 is displayed. It belongs to my second test account bob@example.test, not to Ana, and shows Bob's name, billing address and invoice lines. I confirmed 1043 is Bob's by logging in as Bob separately and seeing the same invoice under "My invoices".

What I tested and did not test:
- Both accounts (Ana and Bob) are my own test accounts, so no real customer data was accessed.
- This was read-only: I only opened the page (GET) and did not edit, download or delete anything.
- Logged out, opening /invoice/1043 sends me to the login page, so the issue requires being logged in as some account.

Expected behavior: An "Access denied" message, or no invoice shown.
Actual behavior: The full invoice of the other account is displayed.

Severity reasoning:
A login is required (any registered user) and I showed read access only, no changes. The invoice number is a short sequential integer (1042 to 1043), so other invoices are easy to reach by changing the number. My own assessment is CVSS 3.1 AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:N/A:N (6.5, Medium); the program may rate it under its own model.

Recommendation:
Verify server-side, on every request to /invoice/<id>, that the logged-in user owns the requested invoice, and return 403 (or 404) otherwise.
