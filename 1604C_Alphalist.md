# BIR 1604-C Alphalist &ndash; Column Reference

This reference documents every column in the Alphalist tool (`1604C_Alphalist.html`), organized the same way the sheet itself is: a **root/group name** (the merged header spanning several columns, where one exists), the **column code** exactly as printed on the BIR form, the **column name**, and a **description** of what it captures or how it's calculated.

**Field types used throughout:**
| Type | Behavior |
|---|---|
| Text | Free-typed entry |
| Select | Dropdown limited to the official code list |
| Number | Manually entered peso amount |
| Computed | Read-only, calculated automatically from other columns on the same row |
| TIN | 9-digit comb-box (grouped 3-3-3), matching the digit-box style used on the main BIR forms |
| Yes/No | Paired checkboxes (checking one clears the other) |

---

## Schedule 1 &ndash; Alphalist of Employees

### Present Employer

| Root / Group | Code | Column Name | Type | Description |
|---|---|---|---|---|
| &mdash; | 1 | Seq. No. | Auto | Row number, assigned automatically as entries are added. |
| NAME OF EMPLOYEES | 2a | Last Name | Text | Employee's last name. |
| NAME OF EMPLOYEES | 2b | First Name | Text | Employee's first name. |
| NAME OF EMPLOYEES | 2c | Middle Name | Text | Employee's middle name. |
| &mdash; | 3 | Nationality/Resident (foreigners only) | Text | Nationality or residency status; only required for foreign employees. |
| &mdash; | 4 | Current Employment Status | Select (R / C / CP / S / P / AL) | Employment classification &ndash; Regular, Casual, Contractual/Project-Based, Seasonal, Probationary, or Apprentice/Learner. |
| PERIOD OF EMPLOYMENT | 5a | Period From (MM/DD) | Text | Start date of employment with the present employer during the year. |
| PERIOD OF EMPLOYMENT | 5b | Period To (MM/DD) | Text | End date of employment with the present employer during the year (if separated). |
| &mdash; | 6 | Reason of Separation | Select (T / TR / R / D) | Terminated/Resigned, Transferred, Retirement, or Death &ndash; only if applicable. |
| &mdash; | 7a | Gross Compensation Income (present employer) | Computed | `7f + 7j` &ndash; total non-taxable plus total taxable compensation. |
| NON-TAXABLE/EXEMPT | 7b | 13th Month Pay & Other Benefits | Number | Portion of 13th month pay/other benefits within the non-taxable threshold. |
| NON-TAXABLE/EXEMPT | 7c | De Minimis Benefits | Number | De minimis benefits within regulatory limits. |
| NON-TAXABLE/EXEMPT | 7d | SSS/GSIS/PHIC/HDMF & Union Dues | Number | Employee-share mandatory contributions and union dues. |
| NON-TAXABLE/EXEMPT | 7e | Salaries (&le;P250,000) & Other Comp. | Number | Salaries and other compensation covered by the P250,000 non-taxable threshold. |
| NON-TAXABLE/EXEMPT | 7f | Total Non-Taxable/Exempt Compensation | Computed | `7b + 7c + 7d + 7e`. |
| TAXABLE | 7g | Basic Salary (net of contributions) | Number | Basic salary net of SSS/GSIS/PHIC/HDMF contributions and union dues. |
| TAXABLE | 7h | 13th Month Pay & Other Benefits (excess of threshold) | Number | Portion of 13th month pay/other benefits exceeding the non-taxable threshold. |
| TAXABLE | 7i | Salaries & Other Forms of Comp. | Number | Taxable salaries and other compensation not covered elsewhere. |
| TAXABLE | 7j | Total Taxable Compensation Income | Computed | `7g + 7h + 7i`. |

### Previous Employer

| Root / Group | Code | Column Name | Type | Description |
|---|---|---|---|---|
| &mdash; | 8 | TIN (Previous Employer) | TIN | Taxpayer Identification Number of the employee's previous employer for the year. |
| &mdash; | 9 | Employment Status | Select (R / C / CP / S / P / AL) | Same classification codes as column 4, for the previous employer. |
| PERIOD OF EMPLOYMENT | 10a | Period From (MM/DD) | Text | Start date of employment with the previous employer. |
| PERIOD OF EMPLOYMENT | 10b | Period To (MM/DD) | Text | End date of employment with the previous employer. |
| &mdash; | 11 | Reason of Separation | Select (T / TR / R / D) | Same codes as column 6, for the previous employer. |
| &mdash; | 12a | Gross Compensation Income (previous employer) | Computed | `12f + 12j`. |
| NON-TAXABLE | 12b | 13th Month Pay & Other Benefits | Number | Same definition as 7b, previous employer. |
| NON-TAXABLE | 12c | De Minimis Benefits | Number | Same definition as 7c, previous employer. |
| NON-TAXABLE | 12d | SSS/GSIS/PHIC/HDMF & Union Dues | Number | Same definition as 7d, previous employer. |
| NON-TAXABLE | 12e | Salaries (&le;P250,000) & Other Comp. | Number | Same definition as 7e, previous employer. |
| NON-TAXABLE | 12f | Total Non-Taxable/Exempt Compensation | Computed | `12b + 12c + 12d + 12e`. |
| TAXABLE | 12g | Basic Salary (net of contributions) | Number | Same definition as 7g, previous employer. |
| TAXABLE | 12h | 13th Month Pay & Other Benefits | Number | Taxable 13th month pay/other benefits, previous employer. |
| TAXABLE | 12i | Salaries & Other Forms of Comp. | Number | Same definition as 7i, previous employer. |
| TAXABLE | 12j | Total Taxable Compensation Income | Computed | `12g + 12h + 12i`. |

### Summary (Present & Previous Employer)

| Root / Group | Code | Column Name | Type | Description |
|---|---|---|---|---|
| &mdash; | 13 | Total Taxable Compensation Income (Present & Previous) | Computed | `7j + 12j`. |
| &mdash; | 14 | Tax Due (January to December) | Number | Annual income tax due on the employee's total compensation. |
| TAX WITHHELD (Jan&ndash;Nov) | 15a | &mdash; Previous Employer | Number | Tax withheld January through November by the previous employer. |
| TAX WITHHELD (Jan&ndash;Nov) | 15b | &mdash; Present Employer | Number | Tax withheld January through November by the present employer. |
| &mdash; | 16 | 5% Tax Credit (PERA Act of 2008) | Number | Tax credit under the Personal Equity and Retirement Account Act, if applicable. |
| YEAR-END ADJUSTMENT | 17a | Amount Withheld/Paid in Dec. or Last Salary | Computed | `MAX(14 &minus; (15a + 15b) &minus; 16, 0)` &ndash; additional tax still due, collected on last pay. |
| YEAR-END ADJUSTMENT | 17b | Over-Withheld Tax Refunded to Employee | Computed | `MAX((15a + 15b + 16) &minus; 14, 0)` &ndash; excess tax refunded to the employee. |
| &mdash; | 18 | Amount of Tax Withheld as Adjusted | Computed | `15a + 15b + 16 + 17a` if there's an amount still due, otherwise `15a + 15b + 16 &minus; 17b`. This is the figure reflected on BIR Form No. 2316. |
| &mdash; | 19 | Substituted Filing? | Yes/No | Whether the employee qualifies for substituted filing (see requisites below the table). |

---

## Schedule 2 &ndash; Alphalist of Minimum Wage Earners

### Present Employer

| Root / Group | Code | Column Name | Type | Description |
|---|---|---|---|---|
| &mdash; | 1 | Seq. No. | Auto | Row number, assigned automatically. |
| NAME OF EMPLOYEES | 2a | Last Name | Text | Employee's last name. |
| NAME OF EMPLOYEES | 2b | First Name | Text | Employee's first name. |
| NAME OF EMPLOYEES | 2c | Middle Name | Text | Employee's middle name. |
| &mdash; | 3 | Current Employment Status | Select (R / C / CP / S / P / AL) | Same classification codes as Schedule 1. |
| &mdash; | 4 | Region No. Where Assigned | Text | DOLE region where the employee is assigned, used to determine the applicable minimum wage. |
| PERIOD OF EMPLOYMENT | 5a | Period From (MM/DD) | Text | Start date of employment with the present employer. |
| PERIOD OF EMPLOYMENT | 5b | Period To (MM/DD) | Text | End date of employment with the present employer. |
| &mdash; | 6 | Reason of Separation | Select (T / TR / R / D) | Same codes as Schedule 1. |
| &mdash; | 7a | Gross Compensation Income (present employer) | Computed | `7o + 7r`. |
| NON-TAXABLE | 7b | Basic/SMW per Day | Number | Statutory minimum wage rate per day. |
| NON-TAXABLE | 7c | Basic/SMW per Month | Number | Statutory minimum wage rate per month. |
| NON-TAXABLE | 7d | Basic/SMW per Year | Number | Statutory minimum wage rate per year. |
| NON-TAXABLE | 7e | Factor Used (No. of Days/Year) | Number | Number of working days per year used to annualize the daily rate. |
| NON-TAXABLE | 7f | Basic/SMW (actual, net of contributions) | Number | Actual basic pay received, net of SSS/GSIS/PHIC/HDMF contributions and union dues. |
| NON-TAXABLE | 7g | Holiday Pay | Number | Holiday pay, exempt for minimum wage earners. |
| NON-TAXABLE | 7h | Overtime Pay | Number | Overtime pay, exempt for minimum wage earners. |
| NON-TAXABLE | 7i | Night Shift Differential | Number | Night shift differential pay, exempt for minimum wage earners. |
| NON-TAXABLE | 7j | Hazard Pay | Number | Hazard pay, exempt for minimum wage earners. |
| NON-TAXABLE | 7k | 13th Month Pay & Other Benefits | Number | Portion within the non-taxable threshold. |
| NON-TAXABLE | 7l | De Minimis Benefits | Number | De minimis benefits within regulatory limits. |
| NON-TAXABLE | 7m | SSS/GSIS/PHIC/HDMF & Union Dues | Number | Employee-share mandatory contributions and union dues. |
| NON-TAXABLE | 7n | Salaries & Other Forms of Comp. | Number | Any other non-taxable salary component. |
| NON-TAXABLE | 7o | Total Non-Taxable/Exempt Compensation | Computed | `7f + 7g + 7h + 7i + 7j + 7k + 7l + 7m + 7n`. |
| TAXABLE | 7p | 13th Month Pay & Other Benefits (excess of threshold) | Number | Portion exceeding the non-taxable threshold &ndash; taxable even for a minimum wage earner. |
| TAXABLE | 7q | Salaries & Other Forms of Comp. | Number | Any taxable salary component (e.g., income earned above minimum wage rates). |
| TAXABLE | 7r | Total Taxable Compensation Income | Computed | `7p + 7q`. |

### Previous Employer

| Root / Group | Code | Column Name | Type | Description |
|---|---|---|---|---|
| &mdash; | 8 | TIN (Previous Employer) | TIN | Taxpayer Identification Number of the previous employer. |
| &mdash; | 9 | Employment Status | Select (R / C / CP / S / P / AL) | Same codes as above, for the previous employer. |
| PERIOD OF EMPLOYMENT | 10a | Period From (MM/DD) | Text | Start date of employment with the previous employer. |
| PERIOD OF EMPLOYMENT | 10b | Period To (MM/DD) | Text | End date of employment with the previous employer. |
| &mdash; | 11 | Reason of Separation | Select (T / TR / R / D) | Same codes as above, for the previous employer. |
| &mdash; | 12a | Gross Compensation Income (previous employer) | Computed | `12k + 12n`. |
| NON-TAXABLE | 12b | Basic/SMW (actual, net of contributions) | Number | Same definition as 7f, previous employer. |
| NON-TAXABLE | 12c | Holiday Pay | Number | Same definition as 7g, previous employer. |
| NON-TAXABLE | 12d | Overtime Pay | Number | Same definition as 7h, previous employer. |
| NON-TAXABLE | 12e | Night Shift Differential | Number | Same definition as 7i, previous employer. |
| NON-TAXABLE | 12f | Hazard Pay | Number | Same definition as 7j, previous employer. |
| NON-TAXABLE | 12g | 13th Month Pay & Other Benefits | Number | Same definition as 7k, previous employer. |
| NON-TAXABLE | 12h | De Minimis Benefits | Number | Same definition as 7l, previous employer. |
| NON-TAXABLE | 12i | SSS/GSIS/PHIC/HDMF & Union Dues | Number | Same definition as 7m, previous employer. |
| NON-TAXABLE | 12j | Salaries & Other Forms of Comp. | Number | Same definition as 7n, previous employer. |
| NON-TAXABLE | 12k | Total Non-Taxable/Exempt Compensation | Computed | `12b + 12c + 12d + 12e + 12f + 12g + 12h + 12i + 12j`. |
| TAXABLE | 12l | 13th Month Pay & Other Benefits | Number | Taxable portion, previous employer. |
| TAXABLE | 12m | Salaries & Other Forms of Comp. | Number | Taxable portion, previous employer. |
| TAXABLE | 12n | Total Taxable Compensation Income | Computed | `12l + 12m`. |

### Summary (Present & Previous Employer)

| Root / Group | Code | Column Name | Type | Description |
|---|---|---|---|---|
| &mdash; | 13 | Total Taxable Compensation Income (Present & Previous) | Computed | `7r + 12n`. |
| &mdash; | 14 | Tax Due (January to December) | Number | Annual income tax due, if any (e.g., on income above minimum wage). |
| TAX WITHHELD (Jan&ndash;Nov) | 15a | &mdash; Previous Employer | Number | Tax withheld January through November by the previous employer. |
| TAX WITHHELD (Jan&ndash;Nov) | 15b | &mdash; Present Employer | Number | Tax withheld January through November by the present employer. |
| &mdash; | 16 | 5% Tax Credit (PERA Act of 2008) | Number | Tax credit under the PERA Act, if applicable. |
| YEAR-END ADJUSTMENT | 17a | Amount Withheld/Paid in Dec. or Last Salary | Computed | `MAX(14 &minus; (15a + 15b) &minus; 16, 0)`. |
| YEAR-END ADJUSTMENT | 17b | Over-Withheld Tax Refunded to Employee | Computed | `MAX((15a + 15b + 16) &minus; 14, 0)`. |
| &mdash; | 18 | Amount of Tax Withheld as Adjusted | Computed | `15a + 15b + 16 + 17a` if there's an amount still due, otherwise `15a + 15b + 16 &minus; 17b`. |
| &mdash; | 19 | Substituted Filing? | Yes/No | Whether the employee qualifies for substituted filing. |

---

## Shared Reference Codes

**Current Employment Status**
| Code | Meaning |
|---|---|
| R | Regular &ndash; hired on a permanent status. |
| C | Casual &ndash; work not usually necessary/desirable to the employer's usual business or trade. |
| CP | Contractual/Project-Based &ndash; employment fixed for a specific project, with completion/termination determined at engagement. |
| S | Seasonal &ndash; timing/duration significantly influenced by seasonal factors. |
| P | Probationary &ndash; trial period during which the employer assesses fitness for regular employment. |
| AL | Apprentices/Learners &ndash; covered by written apprenticeship/learnership agreements. |

**Reason of Separation**
| Code | Meaning |
|---|---|
| T | Terminated/Resigned |
| TR | Transferred |
| R | Retirement |
| D | Death |

**Requisites of Substituted Filing** (all must be true):
1. Receiving purely compensation income, regardless of amount.
2. Working for only one employer in the Philippines for the calendar year.
3. Income tax has been withheld correctly (tax due equals tax withheld).
4. The employee's spouse also meets all three conditions above.
5. Employer filed BIR Form No. 1604-C with Alphalists on or before January 31 of the following year.
6. Employer issued BIR Form No. 2316 to each employee on or before January 31 of the following year (or upon last payment of wages).
7. Employer submitted a duplicate hard copy of BIR Form No. 2316 to the BIR no later than February 28 of the following year.
