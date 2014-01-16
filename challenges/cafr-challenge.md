## PDF Liberation Hackathon – Local Government Audited Financial Report Challenge

Most large US cities publish Comprehensive Annual Financial Reports (CAFRs) in the form of PDFs. These documents contain a large set of audited financial statements with footnotes. This challenge requires you to extract a single statement – a ten-year history of revenues and expenditures – from the latest CAFR for the four hackathon cities (Chicago, New York, San Francisco and Washington DC). By doing this we can compare revenue sources and spending priorities across cities over a number of years.

We have downloaded the CAFRs and placed them in a [shared Dropbox folder](https://www.dropbox.com/sh/xejzj0quoyl0vsm/iIWc4Ik4z2). For reference, links to web based copies of these reports are provided at the end of this document. Automatically downloading these files would be nice, but is not essential to this already difficult challenge.

The schedules required from each city’s CAFR are listed below:

| City | Fiscal Year | File Name on Dropbox | Schedule Name | PDF Page(s) |
| ---- | ----------- | -------------------- | ------------- | ----------- |
| Chicago | 2012 | Chicago_CAFR2012.PDF | GENERAL GOVERNMENTAL REVENUES BY SOURCE – Last Ten Years and GENERAL GOVERNMENTAL EXPENDITURES BY FUNCTION – Last Ten Years | 130-133 of 170 |
| New York | 2013 | NYC_CAFR2013.PDF | Changes in Fund Balances – Governmental Funds – Ten Year Trend | 330- 331 of 397 |
| San Francisco | 2013 | SF_CAFR2013.PDF | CHANGES IN FUND BALANCES OF GOVERNMENTAL FUNDS - Last Ten Fiscal Years | 241 of 257 |
| Washington DC | 2012 | DC_CAFR2012.PDF | Changes in Fund Balances, Governmental Funds, Last Ten Fiscal Years | 184 of 207 |

We are only seeking to process the Revenue and Expenditure data themselves. Fund Balances and other entries toward the bottom of each schedule can be omitted.

This challenge is difficult because the formats vary across cities and because the Washington DC CAFR was produced by scanning and thus requires OCR processing. The other three CAFR PDFs have embedded text and should thus be easier to process. Analyzing the Chicago report is complicated by the fact that row captions are missing from pages 131 and 133; you need to use the captions from pages 130 and 132, respectively.

In addition to extracting the data, the challenge requires transforming it into a standard database-ready format. Rather than actually loading the data into a database, it will be sufficient to produce a tab- delimited file. The Dropbox folder contains a tab delimited file (named `pdflb_cafr_outputs.txt`) with the expected output.

Following is a list of fields that should appear in the output file:

| Fields | Description |
| ---- | ------ |
| CITY | Based on the source document (values are Chicago, New York, San Francisco, Washington DC) |
| Fiscal Year (FY) | Column Headers from Each Table (values are 4-digit numbers ranging from 2003- 2012 in Chicago and DC, and 2004-2013 in New York and San Francisco) |
| Revenue or Expenditure (REV_EXP) | Indicator or whether the category is a Revenue or Expenditure item. Valid values are "Revenues" or "Expenditures". |
| CATEGORY | These are the row headers or captions (examples are "Property Tax, "Utility Tax", "Public Safety", "General Government". |
| AMOUNT | This is the dollar amount in each cell of the PDF tables |


The challenge is to produce this expected output with the highest degree of automation possible. The ideal solution would be one that could easily be applied to previous reports issued by each of the four cities and to comparable reports issued by other cities.

You are welcome to produce visualizations of the data, include additional data or try adding more cities if you have time. You can find more CAFRs at [http://www.publicsectorcredit.org/ca](http://www.publicsectorcredit.org/ca). We recommend working only with larger cities, since many smaller governments do not provide ten-year histories.

CAFR Locations on the Web:

- Chicago [http://www.cityofchicago.org/content/dam/city/depts/fin/supp_info/CAFR/2012/CAFR_2012.pdf](http://www.cityofchicago.org/content/dam/city/depts/fin/supp_info/CAFR/2012/CAFR_2012.pdf)
- New York [http://comptroller.nyc.gov/wp-content/uploads/documents/CAFR2013.pdf](http://comptroller.nyc.gov/wp-content/uploads/documents/CAFR2013.pdf)
- San Francisco [http://www.sfcontroller.org/modules/showdocument.aspx?documentid=4935](http://www.sfcontroller.org/modules/showdocument.aspx?documentid=4935)
- Washington DC (in two parts)
    - [http://cfo.dc.gov/sites/default/files/dc/sites/ocfo/publication/attachments/CAFR%201.pdf](http://cfo.dc.gov/sites/default/files/dc/sites/ocfo/publication/attachments/CAFR%201.pdf)
    - [http://cfo.dc.gov/sites/default/files/dc/sites/ocfo/publication/attachments/CAFR%202.pdf](http://cfo.dc.gov/sites/default/files/dc/sites/ocfo/publication/attachments/CAFR%202.pdf)
