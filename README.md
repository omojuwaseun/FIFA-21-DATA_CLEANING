## FIFA-21-DATA_CLEANING

![fifa_image](https://user-images.githubusercontent.com/119857809/227741417-2090d9d1-30e1-4080-898d-e161f95cf2dd.png)


### CLEANING  FIFA-21 DATASET USING MICROSOFT POWER QUERY

 I joined a data cleaning challenge that was hosted in the tech space on twitter, and this project was aimed at transforming the messy data into a clean usable one that would be useful for future analysis. I cleaned this data using the various tools available on the power query editor and this documentation describes how it was achieved

#### Data cleaning description and aim
The raw fifa dataset was gotten from kaggle, and the data contains 18,979 rows and 77 columns. It contains details and information about players and also their abilities
The aim of this challenge is to improve the quality by making sure the data is complete, accurate and clean before any analysis is done with it

#### Special characters
After importing this dataset into the query editor, i ensured that the file origin was in UTF-8 encoding, and this automatically removed the special characters and replaced it with the correct letters.

#### Name, Long_Name,ID
The dataset had no duplicates, so beginning with the id,name and long_name column, i ensured they had the right data type and was left in its original state

#### Photo_Url, Player_Url
these columns contained metadata about the players which includes a link to their pictures and websites. i deleted these columns since they wouldnt be needed in the analysis phase

![pot before](https://user-images.githubusercontent.com/119857809/227742839-d5d27cdb-875d-48e1-899c-50534d393383.jpg), 
![pot after](https://user-images.githubusercontent.com/119857809/227742848-57ffab90-7710-4551-9683-8338b0c3cd7b.jpg)


#### Potential analysis(POT) and Overall analysis(OVA)
in the data dictionary provided, the columns were advides to be in percentages and this was done by dividing the column by 100, and then creating a new column where   the datatype was changed to percentage and then renamed appropriately

#### Contract 
the contract column had data in different formats and these inconsistencies needed to be fixed. To do this, i created the agreement  using conditional statements.


##### The contract start and end date columns
this was done by splitting of columns by delimeter(-) which was formally(~), and this splitting displays only the year information, which is as a result of the information given in the dataset

##### Agreement
to create this column, i used a conditionnal statement with two clauses and an else statement that stated:

clause 1: if Contract equals Free, output Free
Else If: if Contract contains Loan, Output Loan
Else: Contract
this provides information on the type of agreement the players have with their football clubs 



