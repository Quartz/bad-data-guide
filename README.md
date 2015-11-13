# The Quartz Guide to Bad Data

**An exhaustive reference to the problems seen in real-world data along with suggestions on how to resolve them.**

There are many ways to solve data problems. Some problems can't be solved and that means you shouldn't use the data. Other problems can't be solved, but that you should use the data anyway. In order to allow for these ambiguities, this guide is organized by who you should take the problem to *first*. In the details you'll find suggestions for what to do if the first suggestion can't help you.

## Issues that are your source's problem first

* [Absent/null values](#absentnull-values)      
* [Zeros for absent values](#zeros-for-absent-values)      
* [Missing data](#missing-data)      
* [Duplicates](#duplicates)      
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

## Issues you should raise with another expert first

* [Untrustworthy author](#untrustworthy-author)   
* [Opaque process](#opaque-process)      
* [False precision](#false-precision)  
* [Inexplicable outliers](#inexplicable-outliers)
* [Index masks underlying variation](#index-masks-underlying-variation)       
* [P-hacking](#p-hacking)        
* [Benford's Law fails](#benfords-law-fails)  
* [Too good to be true](#too-good-to-be-true)       

## Detailed list of problems

### Absent/null values

Beware blank or "null" values in any dataset unless you are certain you know what they mean. Was data for that year never collected? Did a survey respondent refuse to answer? Did the creator of the data simply not know that person's birthdate?

Anytime you're working with data that has missing values you should ask yourself: "Do I know what the absence of this data means?" If the answer is no, you should ask your source.

### Zeros for absent values

Worse than missing values is when an arbitrary value is used instead. This can be the result of a human not thinking through the implications or it can happen as the result of automated processes that simply don't know how to handle null values. In either case if you see zeros in a series of numbers you should ask yourself if that values is really the number `0` or if it just means "nothing".

### Missing data

Sometimes data is missing and you know because you know something about the universe of what the data purports to be about. If you have a dataset of baseball players and it doesn't have Mickey Mantle in it, something is probably amiss. Trust your intuition if something seems wrong and double-check with your source. The universe of your data might be smaller than you think.

### Duplicates

If the same row appears in your dataset twice you should find out why. Sometimes it need not be a whole row. Campaign finance data frequently includes "amendments" that use the same unique identifiers as the original transaction. If you don't know that you may end up using both the original transaction and the amended transaction in your calculations. If something that seems like it should be unique isn't, find out why.

### Inconsistent spelling

Spelling is one of the most obvious ways of telling if data has been compiled by hand. Don't just look at names—those can be the hardest place to detect spelling errors. Look for places where city names or states aren't consistent. If you find those, you can be pretty sure the data was compiled or edited by hand and that is always, always a reason to be skeptical of it. Data that has been edited by hand is the most likely to have mistakes.

### Inconsistent name order

Does your data have Middle Eastern or East Asian names in it? Are you sure the surnames are always in the same place? Is it possible anyone in your dataset [uses a mononym](https://en.wikipedia.org/wiki/Indonesian_names#Indonesian_naming_system)? These are the sorts of things that data creators habitually get wrong.

### Inconsistent date formats

`10/9/15` and `9/10/15`: which date is in September? If the first one was written by a European and the second one by an American then they both are. Without knowing the history of the data you can't know for sure. Know where your data came from and that it was produced consistently.

### Unspecified units

Neither `weight` nor `cost` conveys any information about the unit of measurement. Never assume that data produced by in the United States is in `lbs` and `$`. If data doesn't spell out it's units, go back to your source and find out. Even if it does spell out it's units always be wary of meanings that may have shifted over time. A dollar in 2010 is not a dollar today.

### Badly chosen categories

TKTK

### Ambiguous field names

TKTK

### Undocumented provenance

TKTK

### Suspicious numbers

If you see any of these numbers in your data, treat them with an abundance of caution:

* [65,535](https://en.wikipedia.org/wiki/65535_%28number%29)
* [2,147,483,647](https://en.wikipedia.org/wiki/2147483647_%28number%29)
* [4,294,967,295](https://en.wikipedia.org/wiki/4294967295)
* [555-3485](https://en.wikipedia.org/wiki/555_%28telephone_number%29)
* 99999

Each of these numbers is a common symptom of computational or human error

### Over-aggregation

TKTK

### Differs from published aggregates

TKTK

### Differs from observed distribution

TKTK

### 65536 rows

TKTK

### Dates in 1900 or 1904

TKTK

### Text converted to numbers

TKTK

### Encoding problems     

All letters are represented by computers as numbers. Encoding problems are issues that arise when text is represented by a specific set of numbers (called an "encoding") and you don't know what it is. This leads to a phenomenon called [mojibake](https://en.wikipedia.org/wiki/Mojibake) where the text in your data looks like garbage, or like this: ���.

Your source should be able to tell you what encoding your data is in. In the event they can't there are ways of guessing that are about 75% reliable. Ask a coder.

### Under-aggregation

TKTK

### Human data entry  

TKTK

### Aggregations of null values

TKTK

### Non-random sample

TKTK

### Large margin of error

TKTK

### Biased sample

TKTK

### Evidence of manual editing

TKTK

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

TKTK

### P-hacking

TKTK

### Benford's Law fails

TKTK

### Too good to be true

TKTK
