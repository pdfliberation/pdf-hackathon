## EXTRACTING STRUCTURED DATA FROM FORM 990 NONPROFIT DISCLOSURES

[CitizenAudit.org](http://citizenaudit.org/) has run millions of nonprofit disclosures through tesseract, so a large amount of text is ready for processing. But Form 990 has changed slightly each year, and also there are at least three versions, the EO, PF and T, not to mention the usual variance in formatting like line breaks and noise that you get with tesseract.

So we want to start extracting particular fields out of the text, presumably with regex, but the challenge will be ensuring and testing that they work robustly on a significant portion of the forms, not just the one you designed it on, and that they don’t get false positives on others.

I have created a sample corpus of the text versions of 5,000 recent Form 990s (recent years are the priority anyway) in CSV or PostgreSQL form, whichever you prefer. In addition to the actual text, they also include what type of form it is (EO, T, PF) and a URL that you can use to see the original PDF. Viewing the PDF will likely be essential to know what is going on and verify results in some cases. The URL in the sample file will look like `/irs.gov/eo/2010_11_T/85-0248639_990T_201006.pdf`. It is at the domain [https://bulk.resource.org](https://bulk.resource.org)

You can also take the EIN that is in these downloads and view text and get links to the PDFs by going to citizenaudit.org/[EIN]/. Also, there is an API; feel free to ask me for a key.

Download sample files:

[http://s3.amazonaws.com/s3.citizenaudit.org/irs/bulk/sample.csv.zip](http://s3.amazonaws.com/s3.citizenaudit.org/irs/bulk/sample.csv.zip)

[http://s3.amazonaws.com/s3.citizenaudit.org/irs/bulk/sample.sql.zip](http://s3.amazonaws.com/s3.citizenaudit.org/irs/bulk/sample.sql.zip)

Another sample you can browse online:

[http://s3.amazonaws.com/nonprofittext_bulk/samples/index.html](http://s3.amazonaws.com/nonprofittext_bulk/samples/index.html)

Below is a list of fields we’d like to extract eventually. Feel free to email me at lrosiak@gmail with any questions, and thanks!

-Luke Rosiak

1. Name, title and compensation of all officers (Part VII - Section A)

2. Independent contractors (Part VII - Section B)

3. Noncash contributions (Part VIII - 1g) (also should be available in Sked M)

4. Itemized expenses (Part IX - line 24a to 24f, Column A)

5. Total functional expenses (Part IX - line 26, Column A)

6. Program service expenses (Part IX - line 26, Column B

5 and 6 are key to most reporters who are trying to figure out whether or not a charity meets the general standards set by charity watchdogs for % of expenses spent on programs -- even with the data in the 2012 extract you cant answer this question

7. Joint Cost  (Part IX - line 26 - Columns A, B,C and D)

8. Information on Activities Outside of the US (Schedule F - Part I, table 3 - activities per region) - it’d be nice to know which orgs filed one, even if we can extract the data

9. Information on Activities Outside of the US (Schedule F - Part II)

10. Fundraising or Gaming Activites - Schedule G. Would need the whole table in Part I to make it useful

11. Grants and Assistance to organizations in the US (Sked I - table in Part II) -this would could be really tricky b/c how organizations fill it out varies greatly depending on how many items they have to report

12. Business transactions involved related persons. Even just being able to know that an org had filed a sked L would be helpful. If this is hard to do on the checklist of required skeds, maybe there’s a may to just note that they included a sked L. (It includes all the interesting caveats, like oh by the way we’re paying my brother $1 million year just for fun.)

13. Schedule R - related organizations - mostly info in Part II, all columns (i.e. Police Protective Fund)

14. substantial diversion of assets - Part VI, question 5 (WaPo investigation--yes/no/x---difficult or impossible for tesseract)

****

**#1** Name, title and compensation of all officers (Part VII - Section A)

**EXAMPLE 1:**

Form .ASSOCIATION EASTERN FEDERAL BANK 22--3050651 Page7
{Part Vll) Compensation of Officers, Directors, Trustees, Key Employees, Highest Compensated

Employees, and Independent Contractors

Check if Schedule 0 contains a response to any question In this Part i:i
Section A. Officers, Directors, Trustees, Key Employees, and Highest Compensated Employees
1a Complete this table for all persons required to be listed Report compensation tor the calendar year ending with or within the organization's tax year

0 List all of the organization's current officers. directors. trustees (whether individuals or organizations), regardless of amount of compensation.
Enter -0- in columns (D), (E), and (F) if no compensation was paid.

0 List all of the organization's current key employees, if any. See instructions for definition of 'key employee.'

0 List the organization's five current highest compensated employees (other than an officer, director, trustee, or key employee) who received reportable
compensation (Box 5 of Form W-2 and/or Box 7 of Form of more than $100,000 from the organization and any related organizations.

0 List all of the organization's former officers, key employees, and highest compensated employees who received more than $100,000 of
reportable compensation from the organization and any related organizations.

0 all of the organization's former directors or trustees that received, in the capacity as a former director or trustee of the organization,
more than $10,000 of reportable compensation from the organization and any related organizations.
List persons in the following order: individual trustees or directors; institutional trustees; officers; key employees; highest compensated employees;
and former such persons.

Check this box if neither the organization nor any related organization compensated any current officer, director, or trustee.

(Al (3) (C) (D) (E) (F)
Name and niie Average (do not man one Reportable Reportable Estimated
hours per box, unless person is both an compensation compensation amount Of
week a from from related other
(descnbe 13 the organizations compensation
hours for 3 organization from the
related organization
organizations 3 and related
in Scgedule ?3 organizations
5 5 ?2 :2

(1) DAVID LENTINI
DIRECTOR (2) RHEO EROUILLARD
DIRECTOR (3) RICHARD J. CANTELE, JR.
DIRECTOR 1.00 0. O. 0.
(4) JOSEPH J. GRECO

PRESIDENT (5) MARTIN J. GEITZ
VICE PRESIDENT (6) GERALD D. coIA

TREASURER (7) GEORGE w. HERMANN

SECRETARY 132007 or-23-12 Form 990 (2011)

**EXAMPLE 2**

Form 990-Ez (2012) MINISTERIOS CRISTIANOS SHALOM INC 46-2200140 Page 2
I Part II I Balance Sheets (see the instructions for Part II)

Check it the organization used Scheduleoto respond to any question in this Partll . . . . . . . . . . . . . . . . . . . . . . . D
(A) Beginning of year (8) End of year
22Cash,savings,andinvestments  500 22 1,200
23Landandbui|dings 25Totalassets g 500 25 1,200
26 Total liabilities (describein ScheduleONet assets or fund balances (line 27 of column (B) must agree with line 211,200
I Part I Statement of Program Service Accomplishments (see the instructions for Part Expenses
Check if the organization used ScheduIeOto respond to any question in this Part . . . . . . . . . . (Required for section
What is the organization's primary exempt purpose? RELIGIOUS ORGANIZATION 501(c)(3) and 501(c)(4)
Descnbe the organization's program service accomplishments for each of its three largest program services, orgamzahons and Seem
as measured by expenses In a clear and concise manner. describe the services provided, the number of 4947(3)) "55- P"a'
persons benefited, and other relevant information for each pggram title for others
28 PREACHING THE GOSPEL or JESUS CHRIST
(Grants If this amount includes foreign grants, check here . . . . . . . . D D 28a 0
29
(Grants 55 it this amount includes foreign grants, check here . . . . . . . . F El 293
30
(Grants If this amount includes foreign grants, check here . . . . . . . . (Grants If this amount includes foreign grants, check here . . . . . . . . D D 31a
32 Total program service expenses (add lines 28a through 31aPart IV I List of Officers, Directors, Trustees, and Key Employees List each one even if not compensated (see the instructions for Part IV)
Check if the organization used Schedule 0 to respond to any question in this Part Average Reportable Health benefits,

compensation contributions to employ: E5"'"a"d
(Form benelit plans, and Other
(If not paid, enter -0-) deterred Compensation

(3) Name and title hours per week
devoted to position

ALFREDO CALDERON
PRESIDENT 0 O 0 O

**EXAMPLE 3**

EIN: 57-1203034

Name: MUSEUM OF THE AMERICAN COCKTAIL

Form 99OEZ, Part IV - List of Officers, Directors, Trustees, and Key Employees

(A) Name and address

(B) Title and average
hours per week
devoted to position

(C) Compensation
(If not paid,
enter -0-.)

(D) Contributions to
employee benefit plans
8:
deferred compensation

(E) Expense
aocount and
other allowa noes

DALE DEGROFF
3015 BEECH STREET NW
20015

DIRECTOR 1 00

O

JILL DEGROFF
3015 BEECH STREET NW
20015

DIRECTOR 1 00

ROBERT HESS
3015 BEECH STREET NW
20015

DIRECTOR 1 00

EDWARD HAIGH
3015 BEECH STREET NW
20015

DIRECTOR 1 O0

TIM MCNALLY
3015 BEECH STREET NW
20015

DIRECTOR 1 00

BRENDA MAITLAND
3015 BEECH STREET NW
20015

DIRECTOR 1 O0

TIADELAIDE MARTIN
3015 BEECH STREET NW
20015

DIRECTOR 1 00

CHRIS MCMILLAN
3015 BEECH STREET NW
20015

DIRECTOR 1 O0

LAURA MCMILLAN
3015 BEECH STREET NW
20015

DIRECTOR 1 00

23,331

PHILIP GREENE
3015 BEECH STREET NW
20015

DIRECTOR 1 O0

DEREK BROWN
3015 BEECH STREET NW
20015

DIRECTOR 1 00

**EXAMPLE 4**

Check if the organization used Schedule 0 to respond to an uestion in this Part IV.

PalnV I List Of Officers, Directors, Trustees, and Key Emp5lye.e.S..LISteaCl1 one even if not compensated. (see th

e instructions for Part

x <Ls::s:s:.zs:i2i'
ame an a fess devoted to position (It not paid, enter -0-) benet plans agd 5'
deferred compensation

B12
PRESIDENT

HUNTSVILLE TX77342 3.00 0. 0. 0.
BE

VICE PRESIDENT

HUNTSVILLE TX77342 3.00 0. 0. 0.
REED. BREHPPR

SEC TREAS

HUNTSVILLE TX 77342 3.00 O. 0. 0.

DIRECTOR

HUNTSVILLE TX 77342 3.00 0. 0. 0.
-
DI RECTOR

HUNTSVILLE TX 77342 5.00 O. O. 0.

DIRECTOR

HUNTSVILLE TX 77342 5.00 0. 0. 0.
REEL.
DIRECTOR

HUNTSVILLE TX 77342 3.00 0. O. 0.





02114112

Form 990-E72011)


PAGE
Form (2011) WALKER COUNTY FARM BUREAU 7 4 - 60 66625 Page 3

[Part V IOther Information (Note the Schedule A and personal benefit contract statement requirements in

**#2 - Independent contractors**

**EXAMPLE 1 -  **what it looks like if it’s blank

51 Complete this table for the organization's five highest compensated independent contractors who each received more than $100,000
ofcompensation from the organization Ifthere is none, enter "None

Name and address ofeach independent contractor paid more than $100,000 Type ofservice Compensation
NONE

**EXAMPLE 2 - **what it looks like if it’s blank

Title and average (is) Reportable compensation Health benefits, Estimated amount of
Name and address of each employee hours per week (Forms contributions to employee other compensation
paid more than $100,000 devoted to position benet plans and
deferred compensation







D-

e Total number of other employees paid over $100,000

51 Complete this table for the organization's five highest compensated independent contractors who each received more than $100,000 of
comgrisation from the organization. If there is none, enter 'None.'
(in) Name and address of each independent contractor paid more than $100,000

Type of service Compensation

**EXAMPLE 3 - **when it’s filled out

Section B. Independent Contractors

1 Complete this table for yourfive highest compensated independent contractors that received more than

100,000 of compensation from the organization Report compensation for the calendar year ending with

or within the organization's tax year

(A) (B) (C)
Name and business address Description of services Compensation
LINDA HUMPREYS MD
CONTRACTED 119,950

OHIO RIVER BLVD
PITTSBURGH, PA 15202

**EXAMPLE 4 - **when it’s filled out

Section B. Independent Contractors
1 Complete this table for yourfive highest compensated independent contractors that received more than
100,000 of compensation from the organization Report compensation for the calendar year ending with
or within the organization's tax year
(A) (B) (C)
Name and business address Description of services Compensation
THE GOODWAY GROUP PRINTING AND DISTRIBUTION
16 A STREET SERVICES 423,798
BURLINGTON, MA 01803
UNIVERSITY OF CHICAGO PRESS
11030 SOUTH LANGLEY AVENUE PUBLISHING 160,205

CHICAGO, IL 60628

**EXAMPLE - 5**

4 For any individual listed on line 1a, is the sum of reportable compensation and other compensation from the
organization and related organizations greater than $150,000? If "Yes,"complete ScheduleJforsuch
 Did any person listed on line 1a receive or accrue compensation from any unrelated organization or individual for
services rendered to the organization? If "Yes,"complete ScheduleJforsuch person . . 5 NO
Section B. Independent Contractors
1 Complete this table for yourfive highest compensated independent contractors that received more than
100,000 of compensation from the organization Report compensation for the calendar year ending with
or within the organization's tax year
(A) (B) (C)
Name and business address Description of services Compensation
THE BRENNAN GROUP
1 WALNUT STREET GOVERNMENT RELATIONS 125,168
BOSTON, MA 02108
SLOWEYMCMANUS COMMUNICATIONS
PUBLIC RELATIONS SERVICE 119,990

10 TREMONT STREET 6TH FLOOR

BOSTON, MA 02339

2 Total number of independent contractors (including but not limited to those listed above) who received more than
$100,000 ofcompensation from the organization I-2**
**

**#3 total functional expenses**

**EXAMPLE 1**

24 Other expenses Itemize expenses not covered above (List
miscellaneous expenses in line 24f Ifline 24famount exceeds 10% of
line 25, column (A) amount, list line 24fexpenses on Schedule 0

a AUTO LEASES 12,283 12,283
VEHICLE AND EQUIPMENTR 11,425 11,425
SNOW REMOVAL 7,086 7,086
GENERAL MAINTENANCE 5,710 5,710

All other expenses 58 58
25 Total functional expenses. Add lines 1 through 24f 345,032 255,437 73,595 0
26 Joint costs. Check here Ir if following

SOP 98-2 (ASC 958-720) Complete this line only ifthe
organization reported in column (B) Joint costs from a
combined educational campaign and fundraising solicitation

Form 990 (2011)

Form 990 (2011)

**EXAMPLE 2**

24 Other expenses Itemize expenses not covered above (List
miscellaneous expenses in line 24f Ifline 24famount exceeds 10% of
line 25, column (A)amount, list line 24fexpenses on Schedule O

a SUBCONTRACT RESEARCH 672,150 672,150
b EDUCATION AND OUTREACH 150,644 150,644
30,666 28,779 1,845 42
d FIO-SEAKEYS 9,532 9,532
e
f All other expenses 5,788 4,500 788 500
25 Total functional expenses. Add lines 1 through 24f 1,422,340 1,219,235 199,530 3,925
26 Joint costs. Check here I- iffollowing

SOP 98-2 (ASC 958-720) Complete this line only ifthe
organization reported in column (B) Joint costs from a
combined educational campaign and fundraising solicitation

Form 990 (2011)

**EXAMPLE 3**

21 Payments to affiliates . . . . 135 135

22 Depreciation, depletion, and amortization

23 Insurance2,423 2,423

24 Other expenses. itemize expenses not covered ,above (List miscellaneous expenses in line 24eline 24e amount exceeds 10% of line 25, column $53 W :5 g Q
(A) amount, list line 24e expenses on Schedule 0Grounds maintenance 3,282 3,232
b Construction costs for display wall 353 853
c Fundraisjng 5,456 5,456 5,405
d _Gun reimbursement 3,000 3,000
e All other expenses 523 523
25 Total functional expenses. Add llnes1 through 24e 24,934 19,523 5,405

26 Joint costs. Complete this line only If the
organization reported in column (B) joint costs
from a combined educatlonal campaign and
fundralsin solicitation. Check here D if
followlng OP 98-2 (ASC 958-720) . . .

Fon'i1 990 (2012)

**EXAMPLE 4**

24 Other expenses Itemize expenses not covered above (List
miscellaneous expenses in line 24f Ifline 24famount exceeds 10% of
line 25, column (A) amount, list line 24fexpenses on Schedule 0

a UTILITIES 15,821 14,556 1,265

MAINTENANCE REPAIRS 12,919 11,752 1,167

CLOTHING 60,305 60,305

BOOKS AND SUPPLIES 8,515 5,561 2,954

ASSISTEENS ACTIVITIES 19,153 13,529 5,624

All other expenses 25,688 17,890 7,798
25 Total functional expenses. Add lines 1 through 24f 257,475 225,209 32,257 0
26 Joint costs. Check here Ir if following

SOP 98-2 (ASC 958-720) Complete this line only ifthe
organization reported in column (B) Joint costs from a
combined educational campaign and fundraising solicitation

Form 990 (2011)

Form 990 (2011)

Balance Sheet

Page 11

**#6 - program service expenses -- see above - ‘total functional expenses’ - it’s the second number after total expenses. I realize this might be impossible to capture..**

**#7 joint cost **- it’s used by less than 5 percent of exempt orgs, didnt see any examples of orgs that had actually filed it in from a quick scan of the text file.

