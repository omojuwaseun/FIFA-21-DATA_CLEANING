## FIFA-21-DATA_CLEANING

![fifa_image](https://user-images.githubusercontent.com/119857809/227741417-2090d9d1-30e1-4080-898d-e161f95cf2dd.png)


### CLEANING  FIFA-21 DATASET USING MICROSOFT POWER QUERY

 I joined a data cleaning challenge that was hosted in the tech space on twitter, and this project was aimed at transforming the messy data into a clean usable one that would be useful for future analysis. I cleaned this data using the various tools available on the power query editor and this documentation describes how it was achieved

#### Data cleaning description and aim
The raw fifa dataset was gotten from kaggle, and the data contains 18,979 rows and 77 columns. It contains details and information about players and also their abilities
The aim of this challenge is to improve the quality by making sure the data is complete, accurate and clean before any analysis is done with it

### Special characters
After importing this dataset into the query editor, i ensured that the file origin was in UTF-8 encoding, and this automatically removed the special characters and replaced it with the correct letters.

### Name, Long_Name,ID
The dataset had no duplicates, so beginning with the id,name and long_name column, i ensured they had the right data type and was left in its original state

### Photo_Url, Player_Url
these columns contained metadata about the players which includes a link to their pictures and websites. i deleted these columns since they wouldnt be needed in the analysis phase

### Potential analysis(POT) and Overall analysis(OVA)
in the data dictionary provided, the columns were advides to be in percentages and this was done by dividing the column by 100, and then creating a new column where   the datatype was changed to percentage and then renamed appropriately

![pot before](https://user-images.githubusercontent.com/119857809/227742839-d5d27cdb-875d-48e1-899c-50534d393383.jpg), 
![pot after](https://user-images.githubusercontent.com/119857809/227742848-57ffab90-7710-4551-9683-8338b0c3cd7b.jpg)


### Contract 
the contract column had data in different formats and these inconsistencies needed to be fixed. To do this, i created the agreement  using conditional statements.

#### The contract start and end date columns
this was done by splitting of columns by delimeter(-) which was formally(~), and this splitting displays only the year information, which is as a result of the information given in the dataset, In order to be able extract more information from this column, i created three new columns that might be useful when we get to the analysis phase: Agreement, Contract start, Contract end

#### Agreement
to create this column, i used a conditionnal statement with two clauses and an else statement that stated:

clause 1: if Contract equals Free, output Free

Else If: if Contract contains Loan, Output Loan

Else: Contract

this provides information on the type of agreement the players have with their football clubs 

![contract before](https://user-images.githubusercontent.com/119857809/227742950-9af0422d-9546-4530-839c-0023a5a109d2.jpg),
![contract after](https://user-images.githubusercontent.com/119857809/227742959-9c55a944-73ce-4450-bef4-38eee024ad0b.jpg)

###  Position
some players had 2 or more positions that they played and the best way to handle this column was by keeping the first position in the column
this was done by splitting delimeter after which i kept the first column

![positions before](https://user-images.githubusercontent.com/119857809/227743151-3c50f9b1-15e6-409a-9b4a-06435089c62f.jpg)
![positions](https://user-images.githubusercontent.com/119857809/227743157-2547641c-c0c0-495f-b0d4-1fa4e9a80785.jpg)

### Weight
According to the data dictionary, this column had to be in lbs, so to do this i created a custom column which i renamed weight in lbs and used the M language that interpretes that if the weight column has kg in it, it should multiply by 2.205 which is the conversion rate to lbs else it should leave it as it is 

``` if Text.Contains([Weight],"kg") then 
Number.From(Text.BeforeDelimiter([Weight], "kg")) * 2.205
else Text.BeforeDelimiter([Weight],"lbs"))
```
![weight before](https://user-images.githubusercontent.com/119857809/227744759-db63bd32-2554-476c-83f9-9add4b5f73f1.jpg)
![weight in lbs](https://user-images.githubusercontent.com/119857809/227744763-2e291a50-6e84-4d6b-a68c-a5ac71c05c07.jpg)


###  Height
The majority of the values in this column displays height in centimeter 150cm. while others uses feet and inches  5'10" and this column needed to be in cm,and to do this i created a custom column and renamed  to Height in cm, the M-language was also used here

```` cm = if Text.Contains([Height], "cm") then Number.From(Text.BeforeDelimiter([Height], "cm")) else null,
    ft = if Text.Contains([Height], "'") then Number.From(Text.BeforeDelimiter([Height], "'")) else null,
    inch = if Text.Contains([Height], """") then Number.From(Text.BetweenDelimiters([Height], "'", """")) else null,
    Result = if cm <> null then cm else if ft <> null and inch <> null then (ft * 30.48) + (inch * 2.54) else null
in
    Result)
````
![height before](https://user-images.githubusercontent.com/119857809/227744808-922b8d78-0adf-4f81-ba7b-540ed1d3a328.jpg), ![height after](https://user-images.githubusercontent.com/119857809/227744811-3bdc4827-eedc-43f0-aaac-78b06c303c12.jpg)


### Value, Wage, Release clause
these columns had similar inconsistencies, they had the prefix Euros, and also has the suffix M and K which stands for million amd thousands. To adjust this, i removed the euros sign in these columns by replacing the value with nothing and then created a column for each of them where i used the M-language to say that if the value contained 'M' it should multiply by 1000000 but if it had 'K' it should multiply by 1000, then multiply it by 1.07 which is the conversion rate to dollars

#### value
   ``` (if Text.Contains([Value], "M") then
Number.From(Text.BeforeDelimiter([Value], "M")) * 1000000
else Number.From(Text.BeforeDelimiter ([Value],"K")) * 1000) * 1.07)
```
#### wage
``` ( if Text.Contains([Wage],"K") then 
Number.From( Text.BeforeDelimiter ([Wage], "K")) * 1000
else Number.From( [Wage])) * 1.07)
```
#### release clause
``` ( if Text.Contains ([Release Clause], "M") then 
Number.From( Text.BeforeDelimiter ([Release Clause], "M")) * 1000000 
else Number.From( Text.BeforeDelimiter([Release Clause],"K")) * 1000 ) * 1.07)
```
i also corrected the datatype accordingly

![wage value before](https://user-images.githubusercontent.com/119857809/227745037-742d944a-3ffa-4d47-b817-f38720043031.jpg)
![wage value after](https://user-images.githubusercontent.com/119857809/227745043-4789594e-7e16-4c96-94f1-8a8738cc2fa8.jpg)

### IR,SM, W/F
These columns had the star symbol in each row which represented their ratings and this was removed using the replace function and the data type was changed to numeric.

![ir,sm,wf before](https://user-images.githubusercontent.com/119857809/227745205-6885adc8-19c2-4ca9-bb55-d8856c96049c.jpg)
![ir,sm,wf after](https://user-images.githubusercontent.com/119857809/227745674-292cfe34-7676-48a6-9a20-e9201ac32f53.jpg)



### Hits
the same approach used in the values column was applied here, by creating a custom column and writing m-language 
where i multiplied values that had k in them by 1000 and then the appropriate datatype was selected 

![hits before](https://user-images.githubusercontent.com/119857809/227745251-f42bdb94-c776-4c5e-88a2-ae8ca0d37eda.jpg)
![hits after](https://user-images.githubusercontent.com/119857809/227745253-d6cd6198-20fe-4f4a-9af3-4b29b5796ec5.jpg)

### Conclusion
the fifa dataset was very messy, but participating in this challenge was a good way to improve my skills and learn more
The dataset has been transformed and is ready for analysis.











