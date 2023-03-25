## FIFA-21-DATA_CLEANING

![fifa_image](https://user-images.githubusercontent.com/119857809/227741417-2090d9d1-30e1-4080-898d-e161f95cf2dd.png)


CLEANING  FIFA-21 DATASET USING MICROSOFT POWER QUERY

 I joined a data cleaning challenge that was hosted in the tech space on twitter, and this project was aimed at transforming the messy data into a clean usable one that would be usable for future analysis. I cleaned this data using tools available on the power query editor and this documentation describes how it was acheived

#### Data cleaning description and aim
The raw fifa dataset was gotten from kaggle, and the data contains 18,979 rows and 77 columns. It contains details and information about players and also their abilities
The aim of this challenge is to improve the quality by making sure the data is complete, accurate and clean before any analysis is done with it

#### Special characters
After importing this dataset into the query editor, i ensured that the file origin was in UTF-8 encoding, this automatically removed the special characters and replaced it the correct letters.

#### Name, Long_Name,ID
The dataset had no duplicates, so beginning with the id,name and long_name column, i made sure they had the right datatype

#### Photo_Url, Player_Url
these columns contained metadata about the players which includes a link to their pictures and websites. i deleted these columns since they wouldnt be needed in the analysis phase

#### 
