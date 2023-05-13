# ChatGPT-Training-Guide
Here, you'll find a detailed guide to train ChatGPT for conversational AI tasks. This includes steps for data preparation, model configuration, and fine-tuning. We provide code snippets, tips, and resources to help you navigate the training process. Always refer to OpenAI's official documentation for the most current information.


It's important to understand that ChatGPT's data only extends until September 2021. Thus, the information it can provide is limited to that timeframe. For instance, let's consider the ROWNUMBER function in DAX. This function was introduced in April 2023, after the cut-off date of ChatGPT's training data. Consequently, ChatGPT can't generate responses that include knowledge of this function.
<br /><br /><br />
![DAX New function](https://github.com/MahdiSheikhi/ChatGPT-Training-Guide/blob/main/Assests/DAX-ROWNUMBER-NoData.png)

 https://learn.microsoft.com/en-us/dax/rownumber-function-dax
 <br /><br /><br />


However, we can leverage our own knowledge to supplement ChatGPT's understanding. After incorporating the definition of ROWNUMBER provided by Microsoft, ChatGPT can utilize this information as demonstrated below.
<br /><br /><br />
![DAX New function](https://github.com/MahdiSheikhi/ChatGPT-Training-Guide/blob/main/Assests/DAX-New-Function.png)
https://learn.microsoft.com/en-us/dax/new-dax-functions
<br /><br />
You can find train text data here:

<br /><br />


I want to introduce you new DAX function with following structure and definition. Then, I am going to give you sample to completely understand New DAX function.

ROWNUMBER Returns the unique ranking for the current context within the specified partition, sorted by the specified order. If a match cannot be found then then rownumber is blank.

DAX Syntax = ROWNUMBER ( [<relation>][, <orderBy>][, <blanks>][, <partitionBy>] )
Parameters

relation(Optional) :  A table expression from which the output row is returned.
If specified, all columns in <orderBy> and <partitionBy> must come from it.
If omitted:
- <orderBy> must be explicitly specified.
- All <orderBy> and <partitionBy> columns must be fully qualified and come from a single table.
- Defaults to ALLSELECTED() of all columns in <orderBy> and <partitionBy>.

orderBy(Optional) An ORDERBY() clause containing the columns that define how each partition is sorted.
If omitted:
- <relation> must be explicitly specified.
- Defaults to ordering by every column in <relation> that is not already specified in <partitionBy>.

blanks	(Optional) An enumeration that defines how to handle blank values when sorting.
This parameter is reserved for future use.
Currently, the only supported value is KEEP (default), where the behavior for numerical/date values is blank values are ordered between zero and negative values. The behavior for strings is blank values are ordered before all strings, including empty strings.
partitionBy	(Optional) A PARTITIONBY() clause containing the columns that define how <relation> is partitioned.
If omitted, <relation> is treated as a single partition.


Return value
The rownumber number for the current context.


Remarks
Each <orderBy> and <partitionBy> column must have a corresponding outer value to help define the current row on which to operate, with the following behavior:

If there is exactly one corresponding outer column, its value is used.
If there is no corresponding outer column, then:
ROWNUMBER will first determine all <orderBy> and <partitionBy> columns that have no corresponding outer column.
For every combination of existing values for these columns in ROWNUMBER parent context, ROWNUMBER is evaluated and a row is returned.
ROWNUMBER’s final output is a union of these rows.
If there is more than one corresponding outer column, an error is returned.
If the columns specified within <orderBy> and <partitionBy> cannot uniquely identify every row in <relation>, then:

*-ROWNUMBER will try to find the least number of additional columns required to uniquely identify every row.
*-If such columns can be found, ROWNUMBER will
**-Try to find the least number of additional columns required to uniquely identify every row.
**-Automatically append these new columns to <orderBy> clause.
**-Sort each partition using this new set of orderBy columns.
*-If such columns cannot be found and the function detects a tie at runtime, an error is returned.


Example
The following DAX query:
 
```DAX
EVALUATE
ADDCOLUMNS(
    'DimGeography',
    "UniqueRank",
    ROWNUMBER(
    	'DimGeography',
    	ORDERBY(
    		'DimGeography'[StateProvinceName], desc,
    		'DimGeography'[City], asc),
    	PARTITIONBY(
    		'DimGeography'[EnglishCountryRegionName])))
ORDER BY [EnglishCountryRegionName] asc, [StateProvinceName] desc, [City] asc
```

Returns a table that uniquely ranks each geography with the same EnglishCountryRegionName, by their StateProvinceName and City.



Now that you have a full understanding of new DAX function , I want you to act like a professional coder and to use this function while generating DAX query.Are you ready to start generating DAX query with new function ? If so, respond with ‘YES’ and nothing else.

   <br /><br /><br />

![DAX New function](https://github.com/MahdiSheikhi/ChatGPT-Training-Guide/blob/main/Assests/DAX-ROWNUMBER-Generated.png)

  <br /><br /><br />


