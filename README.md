# Incident Rates

I wanted to take some of the lessons I've learned in the R Ladies exercises and apply them to a real world scenario.

In this case I wanted to take a data set of the latest incident rate for MSOAs in Wales and  have a script which lets me see where the highest incident rates per 100,000 of the population are.

This presented a few challenges.

The first was that the data is in an giant .XLSX file with multiple sheets. I cheated a little and downloaded a CSV of the sheet I wanted. I could have imported just the sheet I wanted direct to R but in the interests of time I did it manually.

My first task was to clean the column headers as they are a mess. And I encounted a real problem. Some of the column headings had parenthesis/brackets in the string. And the rename function in Diplyr just wouldn't play nice. 

I spent an age looking for a solution and while there was lots of guidance on how to treat special characters in a string I couldn't find anything simple which worked.

In the end I used the name() function to replace the header by using the column numbers. 

e.g. names(rollingaverages) [4] <- "msoa"

I couldn't find a way to do this as a batch - I imagine I could probably have create a list of the changes and done in that way but in the end I just did it column by column.

I reordered the column headings so I could read the table a little easier and used %>% to group the results by MSOA, council and period, and showing the max value for incidences. 

This then gave me a tidier dataframe to look at.

What I wanted to do was then sort from high to low in terms of the incidences to see where the biggest number of cases was emerging, and do that filtered on the 7 day rolling average. 

But.... when I sorted incidences by size using arrange(desc(incidences)) it seems to be ignoring higher values which have commas in the number. Not sure why.

I also wanted to filter on a particular time period - which is written as a character string - e.g. "Rolling 7 days (15 Oct - 21 Oct)" - and while I think that worked when I then sorted from highest to lowest I couldn't work out why I was still seeing higher numbers below smaller numbers. 

Exporting the csv to Excel and then sorting and filtering manually led to an interesting finding. Cathays South has the highest 7 day rolling averages of Covid incidences per 100,000 people - 2,060, more than twice the rate of any other local area in Wales.

In fact, what's clear is that areas with high student populations in Cardiff are hotspots for Covid currently.




