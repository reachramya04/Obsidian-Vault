# Introduction and Types of Data - Understanding Data 

## Data 
Data is the facts and figures collected , analyzed and summarized for interpretation and presentation.


## Structured and Unstructured Data 
For the information in a database to be useful , the data collected must have a structure.
A structured collection of data is also called a Dataset.

When the data is scattered about with no structure , the information is of very little use.

**Example:** An SQL Table is a structured data.
Comments on a youtube video is an unstructured data.


## Dataset
A structured collection of data is called a Dataset.
Each Variable must have its own column and each observation/case is a row/record.

### Variables and Cases
![[Pasted image 20220906225559.png|600]]
#### Variables 
A characterstic or attribute that varies across all units.

It is the column of the table. It must have a fixed unit for all its entries.
The data within a variable can be of same type i.e. it can be of same units.

**Example:** Id , Name , SurName , Age

#### Cases
A unit from which data is collected.

It is the records of the table. For a record to be considered a case/observation one of its variables must be unique when compared to other records.

**Example:** Jodie , Jayden , Grace

#### Null Values in a Dataset 
![[Pasted image 20220906230345.png|400]]

Sometimes there might be null values within a dataset.
It is to be noted that null values are different from records having values as 0.

When the value of the variable is 0 , it means that the it is defined as nothing for that specific record.
But when the value is null or ----- or NA(Not Available) , it means that data for that specific record is not available.