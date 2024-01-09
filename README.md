# Automate-accounting
## Exploratory data analysis, visualization, and suggestions for performing an automated bank reconciliation.

The event of associating a payment or collection with a document that is pending payment or collection is called bank reconciliation or invoice settlement. When an invoice is marked as paid, it creates an accounting event called a journal entry.

The exercise is to pose/develop the techniques or model you would use to do this automatically, linking invoices and transactions or leaving transactions unlinked because they are direct journal entries.

**Not all bank transactions pay an invoice.** For example, a payment of a commission, payroll, tax... is not handled with an associated document and a direct journal entry is made against an accounting account.

* One bank transaction can pay N invoices.

* Several bank transactions can pay one invoice. For example, when a partial payment is made on an invoice and then the rest is credited to you.

* A bank transaction can be split. For example, if you pay an invoice in another currency, you take the exchange rate difference to an accounting account. Or if you pay a commission for paying this invoice.


#### Transactions

Extract of bank transactions (transactions.csv) from different current accounts of a fictitious client.

- id: unique identifier in the database
- date: value date of the bank transaction
- amount: amount of the bank transaction, (-) means outflow of money, (+) means inflow of money
- concept: concept of the transaction
- bank: origin bank of the transaction
- currency: transaction currency
- category: category of the bank transaction


#### Invoices

Extract of documents (invoices and remittances) payable and receivable read from the customer's accounting system.

- id: identification of the corresponding document
- due_date: due date of this invoice, indicating the last day on which it can (theoretically) be paid and collected.
- customer_name: name of the customer or supplier to which the invoice is linked. The transfers have by default the client "REMESASBANCOS".
- issue_date: Date when the document was issued.
- amount: Amount of the document. (-) denotes outgoing money, (+) incoming money.

* Many companies pay N specific days per month, so it is very common that overdue invoices are paid later because they are received on your customer's paydays or you pay them on your monthly payday.


**Accounting algorithm**

1. **Pre-processing**: Techniques such as cleansing, normalisation, etc. are used to help reconcile bank transactions with invoices.

2. **Relation**: A proprietary method is developed to establish relationships between the two sets of data in order to close outstanding documents and take into account 1:N, 1:1, N:1 and partial cases.
