# pyDatasetGen
A Python library for producing customizable randomly generated datasets to be used in testing and development.

_Original code by Neil Aitken, UBC Digital Scholarship in the Arts_

## Summary
pyDatasetGen provides a simple way to generate customized datasets to test data mining and data visualization code. Sometimes we need 
to test our code, but want to avoid unnecessary interaction with a dataset that might contain private, proprietary, sensitive, or restricted information. Provided we know the 
general format of the dataset (categories of data and column names), we create small or large test datasets that mimic the real dataset, without endangering the original dataset,
making unauthorized copies, or having to file repeated requests for access.

## Features

### Variable texts
**pyDatasetGen** supports the random generation of the following variable types
1. **comment**: a string typical of a message or caption
2. **int**: an integer value generated from the provided min and max
3. **count**: an integer value to represent view counts or likes generated from a min, max, and median (most common value)
4. **fixedint**: a string version of a randomly generated number of a certain number of digits (eg. fixedint(6) --> 001318)
5. **char**: a single character string containing a randomly chosen character picked from a given range (eg. char(A-Z) --> D)
6. **date**: a date string (YYYY-MM-DD) generated from the provided start date and end date (both provided in YYYY-MM-DD format)
7. **email**: a properly formatted email address using only ASCII characters. Email tends to use some part of the user's generated name as part of the account name
8. **url**: a properly formatted URL, with the possibility of a subpage
9. **hashtag**: a short randomly generated hashtag that has a '#' prefix
10. **fullname**: a randomly generated name featuring a first name followed by a last name. Names are drawn from a variety of languages and cultures and represent different genders.
11. **fullname_rev**: like fullname, but name string displays last name first, followed by a comma, then the first name (eg. "LastName, FirstName"). Good if the column is to be sorted
12. **firstname**: generates just a first name
13. **lastname**: generates just a last name (surname)
14. **streetaddress**: generates a street address (eg. 123 Mill Bay)
15. **phonenum**: generates a phone number (eg. 626-123-4567)
16. **booktitle**: generates a book title
17. **callnumber**: generates a call number for a book, either Library of Congress or Dewey Decimal, (eg. callnumber(loc)
18. **issn**: generates an issn (identification number for a journal or periodical)
19. **isbn**: generates an isbn (identification number for a book)
20. **isxn**: randomly generates an issn or isbn


## Configuration

### CFG_GEN_DATASET.TXT
This file defines the columns in the dataset and how they should be generated. Entries can be defined as lists (denoted by [] with comma separated elements) or a generated element (? followed by type). 
Any line can be commented out (disabled) by placing a # at the start.

Example 1
```
platform=[twitter,instagram,facebook,youtube,telegram]
hashtags=[#edmonton,#canada,#chickenwar,#badmonkey,#15minrice,#oilers,#bigoil,#sanctuary,#immigration,#fireisland,#tradewar,#badidea,#sadnews]
#hashtags=?hashtag
message=?sentence
email=?email
url=?url
name=?fullname
date=?date(2023-01-01,2024-12-31)
comment_count=?int(0,50,2500)
like_count=?int(0,200,14000)
```

Example 2
It is also possible to define an entry using a combination of variable types provided they are separated by '+'

```
userid=char(A-Z)+int(1000,2000)+-+fixedint(6)
```

### CFG_GEN_BASE.TXT
This file defines the basic building blocks for hashtags, messages, and other types of non-name random text. At the very least, the following entries must be present: 
- adjectives (adjectives that should be used for building descriptive phrases, user handles, hashtags, etc)
- nouns (nouns that should be used for creating phrases, user handles, hashtags, etc)
- actors (people or creatures that perform actions)
- group (words that represent organizations, categories of people, or other collectives)
- places (usually specific geographic locations, but any location would work)

Example
```
adjectives=[new,old,fiery,smoky,ancient]
nouns=[cloud,can,box,door]
actors=[driver,banker,scientist,professor,dog,cat]
group=[police,students,immmigrants,big industry]
places=[Vancouver,Toronto,NYC,Greenland,Berlin,Canada,Scotland]
```

If additional categories are added, the code can be extended to access these categories.

### CFG_GEN_NAMES
This file contains the lists of male, female, and family names for a variety of different language/heritage groups. The first two entries should be **name_groups** and **name_subgroups** which 
list the languages/heritages prefixes that you want used in name generation. **name_subgroups** simply stores the naming convention suffixes you are using (eg. MaleGiven, FemaleGiven, Family). 
All the remaining entries should follow the pattern where  the entry is named: <name_group><name_subgroup> -- eg. americanMaleGiven.

Example
```
americanMaleGiven=[James,John,Robert,Michael,William,David,Richard,Charles,Joseph
americanFemaleGiven=[Mary,Patricia,Linda,Barbara,Elizabeth,Jennifer,Maria,Susan
americanFamily=[Abell,Ackworth,Adams,Addicock,Alban,Aldebourne,Alfray,Alicock
chineseMaleGiven=[Aiguo,An,Angúo,Bai,Bingwen,Bo,Bohai,Bojing,Bolin,Boqin
chineseFemaleGiven=[Ai,An,Baozhai,Bi,Biyu,Bo,Changchang,Changying,Chao-xing
chineseFamily=[Lǐ,Wáng,Zhāng,Liú,Chén,Yáng,Huáng,Zhào,Zhōu,Wú,Xú,Sūn,Zhū
germanMaleGiven=[Abelard,Adie,Adler,Alaric,Albert,Albrecht,Alger
germanFemaleGiven=[Adalgisa,Adelaide,Adolfina,Aemilia,Alberta
germanFamily=[Abel,Aber,Achen,Ackert,Adelberg,Ahlgrim,Aller
```
