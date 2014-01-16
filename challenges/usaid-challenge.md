## Unlocking U.S. Foreign Aid Reports Database

### Background
USAID, the U.S. Agency for International Development, is the U.S. Government department responsible for foreign assistance in the lower eighty income countries worldwide.  USAID began in 1961 and for the past fifty years has given money to organizations that work in these low income countries to serve the purpose of reducing poverty through building wells, to training teachers, to funding small businesses, to protecting violence against women, to responding to disasters, to improving conditions in refugee and misplaced persons camps, and more.  Each one of these activities requires a qualitative report that is then uploaded as a PDF to the Development Experience Clearinghouse (DEC) which holds over 168,600 technical and program documents with over 155,500 available for electronic download at: https://dec.usaid.gov  More than 99% of the DEC documents are in the PDF format and therefore not ready for most currently available machine-based analytics tools to process.

### Purpose
By making these pdf’s documents open, more searchable, and machine-readable, aid experts and data analysts can identify what has and hasn’t worked in international development.  Analysis can identify patterns potentially demonstrating the effect that clean water has on education, or education on economy, or transparency on political stability.  Opening theses PDFs may identify flaws and hopefully recommendations for improvement. It may also be able to identify programs that could just as easily be managed entirely by the people in country.  The purpose of USAID is to help create conditions in these countries so that assistance from an aid organization is no longer necessary. 

###Challenges

There are currently two challenges that limit the level of public access to DEC documents:  The current DEC interface is designed for users to access individual DEC documents for small-scale studies.  Creating batch-download capability will allow access and analysis of the docs on a much larger scale.

- **Can you create an API to enable batch-download of DEC documents based on their publication dates in yearly or 5-year increments?** For example: Batch 1 (1980-1984); Batch 2 (1985-1989); Batch 3 (1990-1994); Batch 4 (1995-1999); Batch 5 (2000-2004); Batch 6 (2005-2009); Batch 7 (2010-2014).

More than 99% of the DEC documents are in the PDF format and therefore not ready for most currently available machine-based analytics tools to process.

-  **Can you create an automatic process to extract text, pictures, and tables in the DEC PDFs to either integrated or separate files in machine-readable formats, such as XML (particularly StratML), TXT, and CSV, while maintaining the linkages and traceability between the texts, pictures, and tables as are in the original PDFs?** The software or process should be capable of processing large numbers of PDFs with automatic output and sorting functions.

 Successfully opening the DEC will help USAID understand and analyze these public documents, and will set a new standard for ensuring information about U.S. foreign assistance is not tied up in PDFs.

###Resources
Here are sample PDFs of the kinds found at https://dec.usaid.gov

 - [Does Foreign Aid Work? Efforts to Evaluate U.S. Foreign Assistance](http://pdf.usaid.gov/pdf_docs/pcaac439.pdf)
 - [Household Food Security, Agriculture, Health and Emergency Preparedness &hellip; of Mali](http://pdf.usaid.gov/pdf_docs/pnady041.pdf)
 - [Emerging Technology & Practice for Conservation Communications in Africa](http://pdf.usaid.gov/pdf_docs/pnady812.pdf)
 - [The Catalog](http://pdf.usaid.gov/pdf_docs/pnaec555.pdf)

And the [Federal Government’s metadata standards](http://project-open-data.github.io/schema/) that are required for collecting data and information after November 20th, 2013. These don’t apply to the current DEC documents, but may be useful in understanding the depth of categorization and analysis that USAID is aiming to accomplish in gathering new information.  Improving the DEC will help USAID create a better transition from the previous methods of gathering information to a new, structured, and more accountable process.

