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

TKTK

### Zeros for absent values

TKTK

### Missing data

TKTK

### Duplicates

TKTK

### Inconsistent spelling

TKTK

### Inconsistent name order

TKTK

### Inconsistent date formats

TKTK

### Unspecified units

TKTK

currency
weight

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
