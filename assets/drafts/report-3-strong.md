Title: Access to other users' invoices via editable invoice number in URL (IDOR) on InvoiceFlow

Summary and impact:
A logged-in user can view other customers' invoices by changing the invoice number in the URL. This exposes names, addresses and invoice details of customers to anyone with an account. This is a breach of the confidentiality of customer data.

Steps to reproduce:
1. Go to https://invoiceflow.test/login and log in as ana@example.test (password Test1234!).
2. In the menu choose My invoices and open invoice 1042. The URL is now https://invoiceflow.test/invoice/1042.
3. In the address bar, change 1042 to 1043 and press Enter.
4. An invoice appears with the name and address of another customer.

Expected behavior: An "Access denied" message.
Actual behavior: The full invoice of another customer is displayed.

Recommendation:
Verify server-side that the logged-in user owns the requested invoice.
