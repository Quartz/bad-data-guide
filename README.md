# The Quartz Guide to Bad Data

**An exhaustive reference to the problems seen in real-world data along with suggestions on how to resolve them.**

As a reporter your world is full of data. And that data is full of problems. This guide presents a thorough description of many of the kinds of problems that crop up over and over again in the many kinds of data journalists work with.

Most of these problems can be solved. Some problems can't be solved and that means you shouldn't use the data. Other problems can't be solved, but you should still use the data with care. In order to allow for these ambiguities, this guide is organized by who you should take the problem to *first*: your source, a programmer, an expert, etc. In the details of the problem you may also find suggestions for what to do if the first suggestion can't help you.

You can not possibly review every dataset you work with for all of these problems. If you tried you would never get anything published. However, by familiarizing yourself with the sorts of issues you are likely to encounter you will have a better chance of identifying an issue before it causes you to make a mistake.

If you have questions about this guide please email [Chris](mailto:c@qz.com). Good luck!

## Issues that are your source's problem first

* [Absent/null values](#absentnull-values)      
* [Zeros for absent values](#zer8os-for-absent-values)      
* [Missing data](#missing-data)      
* [Duplicates rows or values](#duplicates-rows-or-values)      
* [Inconsistent spelling](#inconsistent-spelling)      
* [Inconsistent name order](#inconsistent-name-order)      
* [Inconsistent date formats](#inconsistent-date-formats)      
* [Unspecified units](#unspecified-units)      
* [Badly chosen categories](#badly-chosen-categories)      
* [Ambiguous field names](#ambiguous-field-names)      
* [Undocumented provenance](#undocumented-provenance)   
* [Suspicious numbers](#suspicious-numbers)      
* [Over-aggregation](#over-aggregation)          
* [Differs from published aggregates](#differs-from-published-aggregates)      
* [Differs from observed distribution](#differs-from-observed-distribution)      
* [65536 rows](#65536-rows)      
* [Dates in 1900 or 1904](#dates-in-1900-or-1904)      
* [Text converted to numbers](#text-converted-to-numbers)      

## Issues that are your problem first

* [Encoding problems](#encoding-problems)        
* [Under-aggregation](#under-aggregation)        
* [Human data entry](#human-data-entry)          
* [Aggregations of null values](#aggregations-of-null-values)      
* [Non-random sample](#non-random-sample)      
* [Large margin of error](#large-margin-of-error)      
* [Biased sample](#biased-sample)      
* [Evidence of manual editing](#evidence-of-manual-editing)      
* [Inflation](#inflation)      
* [Natural/seasonal variation](#naturalseasonal-variation)
* [Manipulated timeframe](#manipulated-timeframe)      
* [Manipulated reference point](#manipulated-reference-point)   
* [Undocumented provenance](#undocumented-provenance)    

## Issues you should take to a programmer first

* [Wrong aggregation](#wrong-aggregation)        
* [Data in scanned documents](#scanned-documents)

## Issues you should raise with third-party expert first

* [Untrustworthy author](#untrustworthy-author)   
* [Opaque process](#opaque-process)      
* [False precision](#false-precision)  
* [Inexplicable outliers](#inexplicable-outliers)
* [Index masks underlying variation](#index-masks-underlying-variation)       
* [P-hacking](#p-hacking)        
* [Benford's Law fails](#benfords-law-fails)  
* [Too good to be true](#too-good-to-be-true)       

## Detailed list of all problems

### Absent/null values

Beware blank or "null" values in any dataset unless you are certain you know what they mean. Was data for that year never collected? Did a survey respondent refuse to answer? Did the creator of the data simply not know that person's birthdate?

Anytime you're working with data that has missing values you should ask yourself: "Do I know what the absence of this data means?" If the answer is no, you should ask your source.

### Zeros for absent values

Worse than missing values is when an arbitrary value is used instead. This can be the result of a human not thinking through the implications or it can happen as the result of automated processes that simply don't know how to handle null values. In any case if you see zeros in a series of numbers you should ask yourself if that values is really the number `0` or if it instead means "nothing". If you aren't sure, ask your source.

### Missing data

Sometimes data is missing and you can't tell from the dataset itself, but you can still know because you know what the data purports to be about. If you have a dataset covering the United States then you can check to ensure all 50 states represented. (And don't forget about [the territories](https://en.wikipedia.org/wiki/Territories_of_the_United_States)—50 isn't the right number if the dataset includes Puerto Rico.) If you're dealing with a dataset of baseball players make sure it has the number of teams you expect. Verify that a few players who you know are included. Trust your intuition if something seems to missing and double-check with your source. The universe of your data might be smaller than you think.

### Duplicate rows or values

If the same row appears in your dataset twice you should find out why. Sometimes it need not be a whole row. Campaign finance data frequently includes "amendments" that use the same unique identifiers as the original transaction. If you didn't know that any calculations you did with the data would be wrong. If something seems like it should be unique verify that it is. If you discover that it isn't, ask your source why.

### Inconsistent spelling

Spelling is one of the most obvious ways of telling if data has been compiled by hand. Don't just look at peoples names—those are often the hardest place to detect spelling errors. Instead look for places where city names or states aren't consistent. (`Los Angelos` is one very common mistake.) If you find those, you can be pretty sure the data was compiled or edited by hand and that is always a reason to be skeptical of it. Data that has been edited by hand is the most likely to have mistakes. This doesn't mean you should use it but you may need to manually correct those mistakes otherwise account for them in your reporting.

### Inconsistent name order

Does your data have Middle Eastern or East Asian names in it? Are you sure the surnames are always in the same place? Is it possible anyone in your dataset [uses a mononym](https://en.wikipedia.org/wiki/Indonesian_names#Indonesian_naming_system)? These are the sorts of things that data creators habitually get wrong. If you're working with a list of ethnically diverse names—which is any list of names—then you should do at least a cursory review before assuming that joining the `first_name` and `last_name` columns will give you something that is appropriate to publish.

### Inconsistent date formats

`10/9/15` and `9/10/15`: which date is in September? If the first one was written by a European and the second one by an American then they both are. Without knowing the history of the data you can't know for sure. Know where your data came from and be sure that it was all created by folks from the same continent.

### Unspecified units

Neither `weight` nor `cost` conveys any information about the unit of measurement. Don't be too quick to assume that data produced by in the United States is in pounds and dollars. Scientific data will often be in metric. For prices may be in their local currency. If data doesn't spell out it's units, go back to your source and find out. Even if it does spell out it's units always be wary of meanings that may have shifted over time. A dollar in 2010 is not a dollar today. And a [ton](https://en.wikipedia.org/wiki/Short_ton) is not a [ton](https://en.wikipedia.org/wiki/Long_ton) nor a [tonne](https://en.wikipedia.org/wiki/Tonne).

### Badly chosen categories

Categorization is a science and it is often applied badly. The most common case of this is data which purports to be `true` or `false`, but really isn't. This often happens with surveys where `refused` or `no answer` are also valid—and meaningful!—values. Another common problem is the usage of any kind of "other" category. If the categories in a dataset of world people's are a bunch of countries and an "other" be sure you know what that means. Did the data collector not know? Were they in international waters? Ex-patriots? Refugees?

Bad categories can also artificially exclude data. This frequently happens with crime statistics. The FBI has defined the crime of "rape" in a variety of different ways over time. In fact, they've done such a poor job of figuring out what rape is that many criminologists argue the statistics should not be used at all. A bad definition might mean a crime is counted in a different category than you expect or that it wasn't counted at all! Be exceptionally leery of this problem when working with data topics where definitions tend to be arbitrary, such as `race` or `ethnicity`.

### Ambiguous field names

What is a `residence`? Is it where someone lives or where they pay taxes? Is it it a city or a county? Field names in data are never as specific as we would like, but particular concern should be applied to those that could obviously mean two or more things. Even if you correctly infer what the data is supposed to be, that ambiguity could have easily caused the person collecting the data to enter the wrong value.

### Undocumented provenance

Data can are made by a variety of kinds of individuals and organizations including businesses, governments, nonprofits and nutjob conspiracy theorists. That data can be gathered in many different ways including surveys, sensors and satellites. It may be typed, tapped or scribbled. Knowing where your data came from can give you a huge amount of insight into its limitations. Survey data, for example, is rarely exhaustive. Sensors vary in their accuracy. Governments are often disinclined to give you unbiased information. Data from a war zone may have a strong geographical bias. To make things situation worse, these sources are often daisy-chained together. Academics sometimes re-distribute data they got from the government. Data that is written by a doctor may be rekeyed by a nurse. Every stage in that chain is an opportunity for error. Know where your data came from.

### Suspicious numbers

If you see any of these numbers in your data, treat them with an abundance of caution:

* [65,535](https://en.wikipedia.org/wiki/65535_%28number%29)
* [2,147,483,647](https://en.wikipedia.org/wiki/2147483647_%28number%29)
* [4,294,967,295](https://en.wikipedia.org/wiki/4294967295)
* [555-3485](https://en.wikipedia.org/wiki/555_%28telephone_number%29)
* 99999

Each of these numbers has an indication of a particular error made by either a human or a computer. If you see them, ensure they actually mean what you think they mean!

### Over-aggregation

Over-aggregation is what we call it when you have data that's been "rolled up" too much. You've got states and you need counties. You've got employers and you need employees. They gave you years, but you want months.

Data can not be disaggregated once it's been put together. If you're given data that's too coarse, you'll need to ask your source for something more specific. They may not have it. If they do have it they may not be able or willing to give it to you. There are many federal datasets that can't be accessed at the local level to protect the privacy of individuals who might be uniquely identified by them. (For example, a single Somali national living in western Texas.) All you can do is ask.

One thing you should never ever do is divide the yearly data you have by 12 and call it the "average per month". That is **always** incorrect. Don't do it.

### Differs from published aggregates

Imagine that after a long FOIA fight you receive a "complete" list of incidents of police use-of-force. You open it up and discover it has 2,467 rows. Great, time to report it out. Not so fast. Before you publish anything from that dataset go find the last time that police chief went on the record about his departments use of force. You may find that in an interview six weeks earlier he said "less than 2,000 times" or that he named a specific number and it doesn't match your dataset.

These sorts of discrepancies between published statistics and raw data can be a very great source of leads. Often times the answer will be simple. For instance, the data may not cover the same time period he was speaking about. But sometimes you'll catch them in a lie. Either way, you should make sure the published numbers match the totals for the data you're given.

### Differs from observed distribution

TKTK

### 65536 rows

The maximum number of rows an old-fashioned Excel spreadsheet was allowed to have was 65,536. If you receive a dataset with that number of rows you have almost certainly been given truncated data. Go back and ask for the rest. Newer versions of Excel allowed for 1,048,576 rows, so it's less likely you'll be working with data that hits the limit.

### Dates in 1900 or 1904

For reasons beyond obscurity, Excel's default date from which it counts all other dates is `January 1st, 1900`. *Unless* you're using Excel on a Mac, in which case it's `January 1st, 1904`. There are a variety of ways in which data in Excel can be entered or calculated incorrectly and end up as one of these two dates. If you spot them in your data, it's probably an issue.

### Text converted to numbers

Not all numerals are numbers. For instance, the US Census Bureau uses "FIPS codes" to identify every place in the United States. These codes are of various lengths and are numeric. However, they are *not* numbers. `037` is the FIPS code for Los Angeles County. It is not the number `37`. The numerals `37` are, however, a valid FIPS code: for North Carolina. Excel and other spreadsheets will often make the mistake of assuming numerals are numbers and stripping the leading zeros. This can cause all kinds of problems if you try to convert it to another file format or merge it with another dataset.

### Encoding problems     

All letters are represented by computers as numbers. Encoding problems are issues that arise when text is represented by a specific set of numbers (called an "encoding") and you don't know what it is. This leads to a phenomenon called [mojibake](https://en.wikipedia.org/wiki/Mojibake) where the text in your data looks like garbage, or like this: ���.

In the vast majority of cases your text editor or spreadsheet application will figure out the correct encoding, however, if it screws it up you could publishing somebody's name with a weird character in the middle. Your source should be able to tell you what encoding your data is in. In the event they can't there are ways of guessing that are about fairly reliable. Ask a programmer.

### Under-aggregation

Under aggregation is the opposite of [Over-aggregation](#over-aggregation). In this case you've got counties, but you want states or you've got months but you want years. Fortunately this is usually pretty straightforward. In general, data can be summarized by using the Pivot Table feature of Excel or Google Docs, by using a SQL database or by writing custom code. Pivot Tables are a fabulously useful tool that every reporter should learn, however, they do have their limits. For exceptionally large datasets or aggregations to unusual groups you should ask a programmer and they can code a solution that's easier to verify and reuse.

See also: [Wrong aggregation](#wrong-aggregation).

### Human data entry  

Human data entry is such a common problem that symptoms of it are mentioned in at least 10 of the other issues described here. There is no worse way to screw up data than to let a single human type it in. For example, I once acquired the complete dog licensing database for Cook County, Illinois. Instead of requiring the person registering their dog to choose a breed from a list, the creators of the system had simply given them a text field to type into. As a result this database contained at least 250 spellings of `Chihuahua`. Even with the best tools available, data this messy can't be saved. It is effectively meaningless. It's not that important with dog data, but you don't want it happening with soldiers or stock markets. Beware human entered data.

### Aggregations of null values

TKTK

### Non-random sample

A non-random sampling error occurs when a survey or other sampled dataset either intentionally or accidentally fails to cover the entire population. This can happen for a variety of reasons ranging from time-of-day to the respondent's native language and is a common source of error in sociological research. It can also happen for less obvious reasons, such as when a researcher thinks they have a complete dataset and chooses to work with only part of it. If the original dataset was incomplete for any reason then any conclusions drawn from their sample will be incorrect.

### Large margin of error

TKTK

### Biased sample

Like a [non-random sample](#non-random-sample), a bias sample results from a lack of care with how the sampling is executed. Or, from willfully misrepresenting it. A sample might be biased because it was conducted on the internet and poorer people don't use the internet as frequently as the rich. Surveys must be carefully weighted to ensure they cover proportional segments of any population that could skew the results. It's almost impossible to do this perfectly so it it often done wrong.

### Evidence of manual editing

Manual editing is almost the same as [human data entry](#human-data-entry) except that it happens after the fact and often with good intentions. In fact, data is often manually edited in an attempt to fix data that was originally entered by humans. Problem start to creep in when the person doing the editing doesn't have complete knowledge of the original data. I once saw someone spontaneously "correct" a name in a dataset from `Smit` to `Smith`. Was that person's name really `Smith`? I don't know, but I do know that data is now a problem. Without a record of that change, it's impossible to verify what it should be.

Issues with manual editing are one reason why you always want to ensure your data has [well-documented provenance](#undocumented-provenance). A lack of provenance can be a good indication that someone may have monkeyed with it. Academics often get data from the government, monkey with it and then redistribute it to journalists. Without any record of their changes it's impossible to know if the changes they made were justified. Whenever feasible always try to get the *primary source* or at least the oldest version you can and then do your own analysis from that.

### Inflation

TKTK

### Natural/seasonal variation

TKTK

### Manipulated timeframe

TKTK

### Manipulated reference point

TKTK

### Undocumented provenance

TKTK

### Wrong aggregation

TKTK

### Data in scanned documents

TKTK

### Untrustworthy author

TKTK

### Opaque process

TKTK

### False precision

TKTK

### Inexplicable outliers

TKTK

### Index masks underlying variation

Analysts who want to follow the trend of an issue often create indices of various values that they can track. There is nothing intrinsically wrong with using an index. They can have great explanatory power. However, it's important to be cautious of indices that combine disparate measures. For example, the United Nations [Gender Inequality Index](p.org/en/content/gender-inequality-index-gii) combines several measures related to women's progress toward equality.

One of the measures used in the GII is "representation of women in parliament". Two countries in the world have law's mandating gender representation in their parliaments: China and Pakistan. As a result these two countries perform far better in the index than countries that are similar in all other ways. Is this right? Maybe so, but it certainly isn't obvious. The GII and similar indices should always be used with careful analysis to ensure their underlying variables don't swing the index in unexpected ways.

### P-hacking

TKTK

### Benford's Law fails

TKTK

### Too good to be true

There is no global dataset of public opinion. Nobody knows the exact number of people living in Siberia. Crime statistics aren't comparable across borders. The US government is not going to tell you how much fissile material it keeps on hand.

Beware any data that purports to represent something that you could not possibly know. It's not data. It's somebody's estimate and it's probably wrong.
