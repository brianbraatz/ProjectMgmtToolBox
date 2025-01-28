---
created: 2024-03-25T10:03:12 (UTC -05:00)
tags: []
source: https://stackoverflow.com/questions/16256388/recreating-a-google-spreadsheets-query-in-excel
author: user2327631
        
            14111 gold badge11 silver badge33 bronze badges
---

# filtering - Recreating a Google Spreadsheets QUERY() in Excel - Stack Overflow

source: https://stackoverflow.com/questions/16256388/recreating-a-google-spreadsheets-query-in-excel

> ## Excerpt
> I have a massive Excel Workbook that I use for tracking product titles and descriptions, and I'm trying to get it to generate .csv files for importing those products into eBay and my own website. I...

---
I have a massive Excel Workbook that I use for tracking product titles and descriptions, and I'm trying to get it to generate .csv files for importing those products into eBay and my own website. I'm 99% of the way there, but I can't seem to find the Excel equivalent of Google Spreadsheet's QUERY() function, and there are two spots I need to use it:

1st, I need to populate a column in SheetB with the Product IDs in SheetA that have not been listed on the site. In Google Spreadsheets, I would do this with `=query('SheetA'A:B,"select A where isblank(B)")` but I can't for the life of me figure out the equivalent in Excel.

2nd, I need to take all the non-blank rows from four different sheets and put them together into one sheet.

There has to be something obvious I'm missing, but I'm missing it. Help me, magical internet people, you're my only hope!
