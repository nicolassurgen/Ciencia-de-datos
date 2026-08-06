Eee ee i: SQL for Data Scientists 

WILEY 

## **SQL for Data Scientists** 



<!-- Start of picture text -->
a<br>a<br><!-- End of picture text -->

WILEY 

Copyright © 2021 by John Wiley & Sons, Inc. All rights reserved. 

Published by John Wiley & Sons, Inc., Hoboken, New Jersey. Published simultaneously in Canada. 

ISBN: 978- 1- 119- 66936- 4 ISBN: 978- 1- 119- 66937- 1 (ebk) ISBN: 978- 1- 119- 66939- 5 (ebk) 

No part of this publication may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning, or otherwise, except as permitted under Section 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the appropriate per- copy fee to the Copyright Clearance Center, Inc., 222 Rosewood Drive, Danvers, MA 01923, (978) 750- 8400, fax (978) 750- 4470, or on the web at www.copyright.com. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 111 River Street, Hoboken, NJ 07030, (201) 748- 6011, fax (201) 748- 6008, or online at http://www.wiley.com/go/permission. 

**Limit of Liability/Disclaimer of Warranty:** While the publisher and author have used their best efforts in preparing this book, they make no representations or warranties with respect to the accuracy or completeness of the contents of this book and specifically disclaim any implied warranties of merchantability or fitness for a particular purpose. No warranty may be created or extended by sales representatives or written sales materials. The advice and strategies contained herein may not be suitable for your situation. You should consult with a professional where appropriate. Neither the publisher nor author shall be liable for any loss of profit or any other commercial damages, including but not limited to special, incidental, consequential, or other damages. 

For general information on our other products and services or for technical support, please contact our Customer Care Department within the United States at (800) 762- 2974, outside the United States at (317) 572- 3993 or fax (317) 572- 4002. 

Wiley also publishes its books in a variety of electronic formats. Some content that appears in print may not be available in electronic formats. For more information about Wiley products, visit our web site at www.wiley.com. 

###### **Library of Congress Control Number:** 2021941400 

**Trademarks:** WILEY and the Wiley logo are trademarks or registered trademarks of John Wiley & Sons, Inc. and/or its affiliates, in the United States and other countries, and may not be used without written permission. All other trademarks are the property of their respective owners. John Wiley & Sons, Inc. is not associated with any product or vendor mentioned in this book. 

Cover image: © filo/Getty Images Cover design: Wiley 

_In my data science career talks, I warn about tech industry gatekeepers. This book is dedicated to the gate- openers._ 

## **About the Author** 

**Renée M. P. Teate** is the Director of Data Science at HelioCampus, leading a team that builds predictive models for colleges and universities. She has worked with data professionally since 2004, in roles including relational database design, data- driven website development, data analysis and reporting, and data science. With degrees in Integrated Science and Technology from James Madison University and Systems Engineering from the University of Virginia, along with a varied career working with data at every stage in a number of systems, she considers herself to be a “data generalist.” 

Renée regularly speaks at technology and higher ed conferences and meetups, and writes in industry publications about her data science work and about navigating data science career paths. She also created the “Becoming a Data Scientist” podcast and @BecomingDataSci Twitter account, where she’s known to her over 60k followers as “Data Science Renee.” She always tells aspiring data scientists to learn SQL, since it has been one of the most valuable and enduring skills needed throughout her career. 

**vii** 

## **About the Technical Editor** 

- **Vicki Boykis** is a machine learning engineer, currently working with recommen dation systems. She has over a decade of experience in analytics and databases across numerous industries including social media, telecom, and healthcare, and has worked with Postgres, SQL Server, Oracle, and MySQL. She has previously taught courses in object- oriented programming (OOP) for Python and MySQL for massive open online courses (MOOCs). She has a BS in Economics with Honors from Penn State University and an MBA from Temple University in Philadelphia. 

**ix** 

## **Acknowledgments** 

When I first started this book in Fall 2019, I was new to the book authoring and publication process, and I couldn’t have anticipated how everything around us would change due to a deadly pandemic and political upheaval. I want to first acknowledge the healthcare and other essential workers who risked their lives during this era of COVID- 19. Nothing any of us have accomplished throughout this time would have been possible without your selfless efforts saving lives and allowing some of us to work safely from home. I also want to thank those who continue fighting for equality in the face of injustice. You inspire me and give me hope. 

As a first- time book author, the process of transferring my knowledge and experience to the page, and bringing this book to completion, has been a major learning experience. I would like to thank the team at Wiley for taking the chance on me and for all of your work, especially project editor Kelly Talbot for guiding me through this process, improving my content, and eventually getting me across the finish line! 

I was so excited when I found out that Vicki Boykis, whose writing about our industry is fascinating and insightful, would be my technical editor. Her thoughtful feedback was invaluable. I truly appreciate her sticking with me throughout this extended process. 

I would also like to thank my family and teachers, who encouraged my interest in computers and technology from a young age and fostered my love of reading, and my friends and mentors who have helped me continue to progress in my education and my career since. Those who have had an impact on me are too numerous to list, but know that I acknowledge your role in helping me get to where I am today. My parents and sister, my husband and step- children, my teachers and managers, my colleagues and friends, your time and energy and patience is so appreciated. 

**xi** 

**xii Acknowledgments** 

And I want to give heartfelt thanks to my husband and my step- son, Tony and Anthony Teate, for always believing in me, giving invaluable feedback, and bearing with me during this extended project. Tony has been a vital part of my “data science journey” from the very beginning, and I’m fittingly wrapping up this long phase of it on his birthday (Happy Birthday, Sweetheart!). The love and support the two of you have shown me is beyond measure. I love you. 

Before I close, I want to give shout- outs to two special communities. First, one that might be a bit unexpected: the vegetable gardening community on Instagram. Growing a garden in my backyard while enjoying your company online honestly helped me get through some of the difficult aspects of writing this book, especially during a pandemic. The fictional Farmer’s Market database used in every example was inspired by you. 

And last but not least, to the data science communities in my local area (Harrisonburg and Charlottesville, Virginia— data science isn’t only done in big cities!) and online, plus those of you reading this book. I feel blessed to be a part of such a vibrant professional community, and honored that you value my experience and advice. Thank you to everyone who has been a part of my data career to date, and who has let me know I have been a part of yours. 

—   Renée M. P. Teate 

## **Contents at a Glance** 

|**Introduction**||**xix**|
|---|---|---|
|**Chapter 1**|**Data Sources**|**1**|
|**Chapter 2**|**The SELECT Statement**|**15**|
|**Chapter 3**|**The WHERE Clause**|**31**|
|**Chapter 4**|**CASE Statements**|**49**|
|**Chapter 5**|**SQL JOINs**|**61**|
|**Chapter 6**|**Aggregating Results for Analysis**|**79**|
|**Chapter 7**|**Window Functions and Subqueries**|**97**|
|**Chapter 8**|**Date and Time Functions**|**113**|
|**Chapter 9**|**Exploratory Data Analysis with SQL**|**127**|
|**Chapter 10**|**Building SQL Datasets for Analytical Reporting**|**143**|
|**Chapter 11**|**More Advanced Query Structures**|**159**|
|**Chapter 12**|**Creating Machine Learning Datasets Using SQL**|**173**|
|**Chapter 13**|**Analytical Dataset Development Examples**|**191**|
|**Chapter 14**|**Storing and Modifying Data**|**229**|
|**Appendix**|**Answers to Exercises**|**239**|
|**Index**||**255**|



**xiii** 

## **Contents** 

|**Introduction**||**xix**|
|---|---|---|
|**Chapter 1**|**Data Sources**|**1**|
||Data Sources|1|
||Tools for Connecting to Data Sources and Editing SQL|2|
||Relational Databases|3|
||Dimensional Data Warehouses|7|
||Asking Questions About the Data Source|9|
||Introduction to the Farmer’s Market Database|11|
||A Note on Machine Learning Dataset Terminology|12|
||Exercises|13|
|**Chapter 2**|**The SELECT Statement**|**15**|
||The SELECT Statement|15|
||The Fundamental Syntax Structure of a SELECT Query|16|
||Selecting Columns and Limiting the Number||
||of Rows Returned|16|
||The ORDER BY Clause: Sorting Results|18|
||Introduction to Simple Inline Calculations|20|
||More Inline Calculation Examples: Rounding|22|
||More Inline Calculation Examples: Concatenating||
||Strings|24|
||Evaluating Query Output|26|
||SELECT Statement Summary|29|
||Exercises Using the Included Database|30|
|**Chapter 3**|**The WHERE Clause**|**31**|
||The WHERE Clause|31|
||Filtering SELECT Statement Results|32|



**xv** 

**xvi Contents** 

||Filtering on Multiple Conditions|34|
|---|---|---|
||Multi-Column Conditional Filtering|40|
||More Ways to Filter|41|
||BETWEEN|41|
||IN|42|
||LIKE|43|
||IS NULL|44|
||A Warning About Null Comparisons|44|
||Filtering Using Subqueries|46|
||Exercises Using the Included Database|47|
|**Chapter 4**|**CASE Statements**|**49**|
||CASE Statement Syntax|50|
||<br>Creating Binary Flags Using CASE|52|
||<br>Grouping or Binning Continuous Values Using CASE|53|
||Categorical Encoding Using CASE<br>|56|
||CASE Statement Summary|59|
||<br>Exercises Using the Included Database|60|
|**Chapter 5**|**SQL JOINs**|**61**|
||Database Relationships and SQL JOINs|61|
||A Common Pitfall when Filtering Joined Data|71|
||<br>JOINs with More than Two Tables|74|
||Exercises Using the Included Database|76|
|**Chapter 6**|**Aggregating Results for Analysis**|**79**|
||GROUP BY Syntax|79|
||<br>Displaying Group Summaries|80|
||Performing Calculations Inside Aggregate Functions|84|
||MIN and MAX|88|
||COUNT and COUNT DISTINCT|90|
||Average|91|
||Filtering with HAVING|93|
||CASE Statements Inside Aggregate Functions|94|
||<br>Exercises Using the Included Database|96|
|**Chapter 7**|**Window Functions and Subqueries**|**97**|
||ROW NUMBER|98|
||RANK and DENSE RANK|101|
||NTILE|102|
||Aggregate Window Functions|103|
||<br>LAG and LEAD|108|
||Exercises Using the Included Database|111|
|**Chapter 8**|**Date and Time Functions**|**113**|
||Setting datetime Field Values|114|
||EXTRACT and DATE_PART|115|



**Contents xvii** 

||DATE_ADD and DATE_SUB|116|
|---|---|---|
||DATEDIFF|118|
||TIMESTAMPDIFF|119|
||Date Functions in Aggregate Summaries and<br>Window Functions|119|
||Exercises|126|
|**Chapter 9**|**Exploratory Data Analysis with SQL**|**127**|
||Demonstrating Exploratory Data Analysis with SQL|128|
||Exploring the Products Table|128|
||Exploring Possible Column Values|131|
||Exploring Changes Over Time|134|
||Exploring Multiple Tables Simultaneously|135|
||Exploring Inventory vs. Sales|138|
||Exercises|142|
|**Chapter 10**|**Building SQL Datasets for Analytical Reporting**|**143**|
||Thinking Through Analytical Dataset Requirements<br>Using Custom Analytical Datasets in SQL:<br>|144<br>|
||CTEs and Views|149|
||Taking SQL Reporting Further|153|
||Exercises|157|
|**Chapter 11**|**More Advanced Query Structures**|**159**|
||UNIONs|159|
||Self- Join to Determine To- Date Maximum|163|
||Counting New vs. Returning Customers by Week|167|
||Summary|171|
||Exercises|171|
|**Chapter 12**|**Creating Machine Learning Datasets Using SQL**|**173**|
||Datasets for Time Series Models<br>|174|
||Datasets for Binary Classifcation|176|
||Creating the Dataset|178|
||Expanding the Feature Set|181|
||Feature Engineering|185|
||Taking Things to the Next Level|189|
||Exercises|189|
|**Chapter 13**|**Analytical Dataset Development Examples**|**191**|
||What Factors Correlate with Fresh Produce Sales?|191|
||How Do Sales Vary by Customer Zip Code,<br>Market Distance, and Demographic Data?|211|
||How Does Product Price Distribution Affect<br>Market Sales?|217|
|**Chapter 14**|**Storing and Modifying Data**|**229**|
||Storing SQL Datasets as Tables and Views|229|
||Adding a Timestamp Column|232|



**xviii Contents** 

||Inserting Rows and Updating Values in<br>Database Tables|233|
|---|---|---|
||Using SQL Inside Scripts|236|
||In Closing|237|
||Exercises|238|
|**Appendix**|**Answers to Exercises**|**239**|
|**Index**||**255**|



## **Introduction** 

#### **Who I Am and Why I’m Writing About This Topic** 

When I was first brainstorming topics for this book, I used two questions to narrow down my list: “Who is my audience?” and “What topic do I know well enough to write a book that would be worth publishing for that audience?” 

The first question had an easy initial answer: I already have an audience of data- science- learning Twitter followers with whom I share resources and advice on “Becoming a Data Scientist” that I could keep in mind while narrowing down the topics. 

So then I was left to figure out what I know that I could teach to people who want to become data scientists. 

I have been designing and querying relational databases professionally for about 17 years: first as a database and web developer, then as a data analyst, and for the last 5 years, as a data scientist. SQL (Structured Query Language) has been a key tool for me throughout— whether I was working with MS Access, MS SQL Server, MySQL, Oracle, or Redshift databases, and whether I was summarizing data into reporting views in a data mart, extracting data to use in a data visualization tool like Tableau, or preparing a dataset for a machine learning project. 

Since SQL is a tool I have used throughout my career, and because creating and retrieving datasets for analysis has been such an integral part of my job as a data scientist, I was surprised to learn that some data scientists don’t know SQL or don’t regularly write SQL code. But in an informal Twitter poll I conducted, which received responses from 979 data scientists, 19% of them reported wanting to learn, or learn more, SQL (74% reported already using SQL professionally). Additionally, 55% of 713 respondents who were working toward becoming data 

**xix** 

**xx Introduction** 

scientists said they wanted to learn, or learn more, SQL. So, my target audience had an interest in this topic. 

According to an analysis of online job postings conducted by Jeff Hale of Towards Data Science, SQL is in the top three technology skills that data scientist jobs require. (See towardsdatascience.com/the- most- in- demand- skillsfor- data- scientists- 4a4a8db896db.) In an Indeed BeSeen article, Joy Garza lists SQL as one of the top- five in- demand tech skills for data scientists. (See https://web.archive.org/web/20200624031802/https://www.beseen.com/ blog/talent/data-scientist-skills/.) 

After learning how many working and prospective data scientists wanted to learn SQL, and how much of a need there is in the industry for people who know how to use it, SQL dataset development started to move to the top of the list of topics I could share my knowledge of with others. 

There are many SQL books on the market that can be used to learn query syntax and advanced SQL functions— after all, the language has been around for 45 years and has been standardized since the late 1980s— but I hadn’t found any definitive resources to refer people to when they asked me if I knew of any books that taught how to use SQL to construct datasets for machine learning, so I decided to write this book to cover SQL from a data scientist’s point of view. 

So, my goal in writing this book is not only to teach you how to write SQL code but to teach you how to think about summarizing data into analytical datasets that can be used for reports and machine learning: to use SQL like a data scientist does. Like I do. 

#### **Who This Book Is For** 

_SQL for Data Scientists_ is designed to be a learning resource for anyone who wants to become (or who already is) a data analyst or data scientist, and wants to be able to pull data from databases to build their own datasets without having to rely on others in the organization to query the source system and transform it into flat files (or spreadsheets) for them. 

There are plenty of SQL books out there, but many are either written as syntax references or written for people in other roles that create, query from, and maintain databases. However, this book is written from the perspective of a data scientist and is aimed at those who will primarily be extracting data from existing databases in order to generate datasets for analysis. 

I won’t assume that you’ve ever written SQL queries before, and we’ll start with the basics, but I do assume that you have some basic understanding of what databases are and a general idea of how data might be used in reports, analyses, and machine learning algorithms. This book is meant to fill in the steps between finding a database that contains the data you need and starting the analysis. I aim to teach you how to think about structuring datasets for analysis and how to use SQL to extract the data from the database and get it into that form. 

**Introduction xxi** 

#### **Why You Should Learn SQL if You Want to Be a Data Scientist** 

If you can use SQL to pull your own datasets, you don’t have to rely on others in your organization to pull it for you, enabling you to work more efficiently. Requesting datasets usually involves a process of filling out a form or ticket describing in detail what data you need, waiting for your request to be fulfilled, then often clarifying your request after seeing the initial results, and then waiting again for modifications. If you can edit your own queries, you can not only design and retrieve your own datasets but then also adjust calculations or add fields as needed. 

Additionally, running a SQL query that writes to a database table or exports to a file— effectively snapshotting the data in the form you need it in for your analysis— means you don’t have to retrieve and reprocess the data in your machine learning script every time you run your code, speeding up the usually iterative model development process. 

Some summaries and calculations can be done more efficiently in SQL than in other types of code, as well, so even if you are running the queries “live” each time you run your script, you may be able to lower the computational cost of your code by doing some of the transformations in SQL. 

Finally, because it is a high- demand tech skill in data scientist job postings, learning SQL will increase your marketability and value to employers. 

#### **What I Hope You Gain from This Book** 

My goal is that by the time you finish reading this book and practicing the queries within (ideally both on the provided example database and on another database of your choosing, so you have to modify the example queries and apply them in another context), you will be able to think through the process of creating an analytical dataset and develop the SQL code necessary to generate your intended output. 

I hope that even if you end up needing to use a SQL function that’s not covered in this book, you will have gained enough baseline knowledge from the book to go look it up online and determine how to best use it in the query you are developing. 

I also hope that this book will help you feel confident that you can pull your own data at work and get it into the form you need it in for your report or model without having to wait on others to do it for you. 

**xxii Introduction** 

#### **Conventions** 

This book uses MySQL version 8.0–style SQL. No matter what type of database system you use (MS SQL Server, Redshift, PostgreSQL, Oracle, etc.), the query design concepts and syntax are very similar, when not identical across platforms. So, if you work with a database system other than MySQL, you might have to search for the equivalent code syntax for a few functions in the book, but the overall dataset design concepts are platform- independent, and the SQL keywords are cross- platform standards. 

When you see code displayed in the following style: 

###### SELECT * FROM Product 

that means it is a complete SQL query that you can use to select data from the Farmer’s Market database described in Chapter 1, “Data Sources.” If you’re reading the printed version of this book, you can go to the book’s website to get digital versions of the queries that you can copy and paste to try them out yourself. 

Reserved SQL keywords like SELECT will appear in all- uppercase throughout the book, and column names will appear in all- lowercase. This isn’t a requirement of SQL syntax (neither are line breaks), but is a convention used for readability. 

Be aware that the Farmer’s Market database will continue to evolve, and I will likely continue adding rows to its tables after this book goes to print, so the data values you see in the output when you run the queries yourself may not exactly match the screenshots included in the printed book. 

#### **Reader Support for This Book** 

##### **Companion Download Files** 

As you work through the examples in this book, you may choose either to type in all the code manually or to use the source code files that accompany the book. All the source code used in this book, along with the Farmer’s Market database, is available for download from both sqlfordatascientists.com and www.wiley.com/go/sqlfordatascientists. 

##### **How to Contact the Publisher** 

If you believe you’ve found a mistake in this book, please bring it to our attention. At John Wiley & Sons, we understand how important it is to provide our customers with accurate content, but even with our best efforts an error may occur. 

In order to submit your possible errata, please email it to our Customer Service Team at wileysupport@wiley.com with the subject line “Possible Book Errata Submission”. 

**Introduction xxiii** 

##### **How to Contact the Author** 

I’m known as “Data Science Renee” on Twitter, and my username is @becomingdatasci. I’m happy to interact with readers via social media, so feel free to tweet me your questions and suggestions. 

Thank you for giving me the chance to help guide you through the topic of _SQL for Data Scientists_ . Let’s dive in! 

###### **<mark>C H A P T E R</mark>** 

**1** 

## **Data Sources** 

As a data analyst or data scientist, you will encounter data from many sources— from databases to spreadsheets to Application Programming Interfaces (APIs)— which you are expected to use for predictive modeling. Understanding the source system your data comes from, how it was initially gathered and stored, and how frequently it is updated, will take you a long way toward an effective analysis. In my experience, issues with a predictive model can often be traced back all the way to the source data or the query that first pulls the data from the source. Exploring the data available for your analysis starts with exploring the structure of the source database. 

#### **Data Sources** 

Data can be stored in many forms and structures. Examples of _unstructured_ data include text documents or images stored as individual files in a computer’s file system. In this book, we’ll be focusing on _structured_ data, which is typically organized into a tabular format, like a spreadsheet or database table containing limited-length text or numeric values. 

Many software applications enable the organization of data into structured forms. One example you are likely familiar with is Microsoft Excel, for creating and maintaining spreadsheets. Excel also includes some analysis capabilities, such as pivot tables for summarizing spreadsheets and data visualization tools 

**1** 

**2 Chapter 1** ■ **Data Sources** 

for plotting data points from a spreadsheet. Some functions in Excel allow you to connect data in one spreadsheet to another, but in order to create a true relational database model and define rules for how the data tables are interconnected, Microsoft offers a relational database application called Access. 

My first experiences with relational database design were in MS Access, and the basic Structured Query Language (SQL) concepts I learned in order to query data from an Access database are the same concepts I have used throughout my career—in increasingly complex ways. I have since extracted data from other Relational Database Management Systems (RDBMSs) such as MS SQL Server, Oracle Database, MySQL, and Amazon Redshift. Though the syntax for each can differ slightly, the general concepts, many of which you will learn in this book, are consistent across products. 

SQL-style RDBMSs were first developed in the 1970s, and the basic database design concepts have stood the test of time; many of the database systems that originated then are still in use today. The longevity of these tools is another reason that SQL is so ubiquitous and so valuable to learn. 

As a professional who works with data, you will likely encounter several of the following popular Relational Database Management Systems: 

- Oracle 

- MySQL 

- MS SQL Server 

- PostgreSQL 

- Amazon Redshift 

- IBM DB2 

- MS Access 

- SQLite 

- Snowflake 

You will also likely work with data retrieved from other types of files at some point, such as CSV text files, JSON retrieved via API, XML in a NoSQL database, Graph databases with special query languages, key-value stores, and so on. However, relational SQL databases still dominate the industry for structured data storage and are the most likely database systems you will encounter on the job. 

#### **Tools for Connecting to Data Sources and Editing SQL** 

When you start an analysis project, the first step is often connecting to a database on a server. This is generally done through a SQL Integrated Development Environment (IDE) or with code that connects to the database without a graphical 

**Chapter 1** ■ **Data Sources** 

**3** 

user interface (GUI) to run queries that extract the data and store it in a structure that you can work with downstream in your analysis, such as a dataframe. 

The IDE referenced for demonstration purposes throughout this book is MySQL Workbench Community Edition, which was chosen because we’ll be querying a MySQL database in the examples. MySQL is open source under the GPL license, and MySQL Workbench CE is free to download. 

Many other IDEs will allow you to connect to databases and will perform syntax-highlighting of SQL (highlighting keywords to make it easier to read and to spot errors). All major database systems support Open Database Connectivity (ODBC), which uses drivers to standardize the interfaces between software applications and databases. Whoever has granted you permission to access a database should give you documentation on how to securely connect to it via your selected IDE. 

You can also connect to a database directly from code such as Python or R. Search for your preferred language and the type of database (for example, “R SQL Server” or “Python Redshift”) and you will find packages or add-ons that enable you to embed SQL queries in your code and return results in the form of a dataframe or other data structure. The database system’s official documentation will also provide information about connecting to it from other software and from within your code. Searching “MySQL connector” brings up a list of drivers for use with different languages, for example. 

If you are writing code in a language like Python and will be passing a SQL statement to a function as a string, where it won’t be syntax highlighted, you can write SQL in a free text tool that performs SQL syntax highlighting, such as Notepad++, or in a SQL IDE, and then paste the final result into your code. 

#### **Relational Databases** 

If you have never explored a database, you can think of a database table like a well-defined spreadsheet, with row identifiers and named column headers. Each table may store different subsets and types of data at different levels of detail. 

An _entity_ is the “thing” (object or concept) that the table represents and captures data for. If there is a table that contains data about books, the entity is “Books,” and the “Book table” is the data structure that contains information about the Book entity. Some people use the terms _entity_ and _table_ interchangeably. 

You may see me using the terms _row_ and _record_ interchangeably in this book: a record in a database is like a row in a table and displayed the same way. Some people call a database row a _tuple_ . 

You may also see me using the terms _column_ , _field_ , and _attribute_ as synonyms. A column header in a spreadsheet is the equivalent of an attribute name in a table. Each column in a database table stores data about an attribute of the entity. 



<!-- Start of picture text -->
Column<br>or<br>Attribute<br>or<br>Field<br>ISBN Title Author<br>Row or Record > 978-1-119-66936-4 SQL for Data Scientists Renée M. P. Teate<br>978-1-119-00206-2 Storytelling with Data Cole Nussbaumer Knaflic<br><!-- End of picture text -->



<!-- Start of picture text -->
Patients Appointments<br>Patient Patient Patient Phone Patient Appointment Appointment Doctor Name<br>Name Birthdate Number Name Time Reason<br><!-- End of picture text -->



<!-- Start of picture text -->
Patient Name* > Patient Name**<br>Patient Birthdate Appointment Time |<br>Patient Phone Number Appointment Reason<br>Doctor Name<br><!-- End of picture text -->



<!-- Start of picture text -->
Pe<br><!-- End of picture text -->

~~Pe~~ 



<!-- Start of picture text -->
1<br>Patient ID* Appointment ID*<br>Patient First Name Patient ID**<br>Patient Last Name Appointment Time<br>Patient Birthdate Appointment Reason<br>Patient Phone Number Doctor Name<br>Patients<br>Patient Patient First Patient Last Patient Patient Phone<br>ID Name Name Birthdate Number<br>Appointments<br>Appointment Patient Appointment Time Appointment Reason Doctor Name<br>ID ID<br><!-- End of picture text -->



<!-- Start of picture text -->
Books Books-Authors Junction JAuthors<br>ISBN* 1 co 1<br>Title AuthorISBN** ID** oo AuthorAuthor ID*Full Name<br>Publisher<br>Publication Year<br><!-- End of picture text -->

**Chapter 1** ■ **Data Sources 7** 

In the ERD shown in Figure 1.5 you can see that the ISBN, which is the primary key in the Books table, and the Author ID, which is the primary key in the Authors table (denoted by asterisks) are both foreign keys in the Books-Authors Junction table (denoted by double asterisks). Each pairing of ISBN and Author ID in the junction table would be unique, so the pair of fields can be considered a multi-column primary key in the Books-Authors Junction table. 

By setting up this database relationship so that we don’t end up with multiple rows per book in the Books table or multiple authors listed per book in the Authors column of the Books table and have a junction table that only contains the identifiers matching up the related tables, we are reducing the amount of redundant data stored in the database and clarifying how the entities are related in real life. 

The idea of not storing redundant data in a database unnecessarily is known as database _normalization_ . In the book database example, we only have to store each author’s full name once, no matter how many books they have written. In the doctor’s office example, there’s no need to store a patient’s phone number repeatedly in the Appointments table, because it’s already stored in the related “patient directory” table, and can be found by connecting the two tables via the Patient ID (we will cover SQL JOINs, which are used to merge data from multiple tables, in Chapter 5, “SQL JOINs”). Normalization can reduce the amount of storage space a database requires and also reduce the complexity of updating data, since each value is stored a minimal number of times. We won’t go into all of the details of normalization here, but if you are interested in learning more about it, research “relational database design.” 

#### **Dimensional Data Warehouses** 

_Data warehouses_ often contain data from multiple underlying data sources. They can be designed in a normalized relational database form, as described in the previous section, or using other design standards. They may contain both “raw data” extracted from other databases directly, and “summary” tables that are combined or transformed versions of that raw data (for example, the analytical datasets you will learn to build in this book could be permanently stored as tables in a data warehouse, to be referenced by multiple reports). Data warehouses can contain historical data logs with past and current records, tables that are updated in real time as the source systems are updated, or snapshots of data to preserve it as it existed at a past moment in time. 

Often, data warehouses are designed using dimensional modeling techniques. We won’t go in-depth into the details of dimensional modeling here, but one concept you are likely to come across when querying tables in data warehouses is a “star schema” design that divides the data into facts and dimensions. 

**8 Chapter 1** ■ **Data Sources** 

The way I think of facts and dimensions is that a record in a _fact table_ contains the “metadata” of an entity, as well as any _measures_ (which are usually numeric values) you want to track and later summarize. A _dimension_ is property of that entity you can group or “slice and dice” the fact records by, and a _dimension table_ will contain further information of that property. 

So, for example, a transactional record of an item purchased at a retail store is a _fact_ , containing the timestamp of the purchase, the store number, order number, customer number, and the amount paid. The store the purchase was made at is a _dimension_ of the item purchase _fact_ , and the associated store _dimension table_ would contain additional information about the store, such as its name. You could then query both the fact and the dimension tables to get a summary of purchases by store. 

If we transformed our doctor’s office database into a star schema, we might have an appointments fact table capturing the occurrence of every appointment, which patient it was for, when it was booked, the reason for the appointment, which doctor it was with, and when it is scheduled to occur. We might also have a date dimension and a time dimension, storing the various properties of each appointment date and time (such as year or day of week) and appointmentbooking date and time. 

This would allow us to easily count up how many appointments occurred per time period or determine when the highest volume of appointment-booking calls take place, by grouping the “transactional” fact information by different dimensions. 

Figure 1.6 depicts an example dimensional data warehouse design. Can you see why this design is called a star schema? 



<!-- Start of picture text -->
Dim Patient Dim Date<br>Fact<br>Dim Doctor Appointment Dim Time<br>Dim<br>Appointment<br>Reason<br><!-- End of picture text -->

**Figure 1.6** 

There might also be an appointment history log in this data warehouse, with a record of each time the appointment was changed. That way, not only could we tell when the appointment is supposed to take place, but how many times it was modified, whether it was initially assigned to another doctor, etc. 

**Chapter 1** ■ **Data Sources 9** 

Note that when compared to a normalized relational database, a dimensional model stores a lot more information. Appointment records will appear multiple times in an appointment log table. There may be a record for every calendar date in the date dimension table, even if no appointments are scheduled for that date yet, and the list of dates might extend for decades into the future! 

If you’re designing a database or data warehouse, you need to understand these concepts in much more detail than we’ll cover here. But in order to query the database to build an analytical dataset, you primarily need to understand the data warehouse table _grain_ (level of detail; what set of columns makes a row unique) and how the tables are related to one another. Once you have that information, querying a dimensional data warehouse with SQL is much like querying a relational database with SQL. 

#### **Asking Questions About the Data Source** 

Once you find out what type of data source you’re working with and learn about the schema design and the relationships between the database tables, there is still a lot of information you should gather about the tables you’ll be querying before you dive into writing any SQL. 

If you are lucky enough to have access to subject matter experts (SMEs) who know the details of why the database was designed the way it is, how the data is collected and updated, and what to expect in terms of the frequency and types of data that may be updating as you work with the database, stay in communication with them throughout the data exploration and query development process. These might be database administrators (DBAs), ETL engineers (the people who extract, transform, and load data from a source system into a data warehouse), or the people who actually generate or enter the data into the source system in the first place. If you spot some values that don’t seem to make sense, you can sometimes look in a data dictionary to learn more (if one exists and is correct), but often going directly to the SMEs to get the details is the best approach. If your questions are easily answered by existing documentation, they will point you to it! 

Here are some example questions you might want to ask the SMEs as you’re first learning about the data source: 

- “Here are the questions I’m being asked to answer in my analysis. Which tables in this database should I look in first for the relevant data? And is there an entity-relationship diagram documenting the relationships between them that I can reference?” 

These questions are especially helpful for large data warehouses with a lot of tables, where being pointed in the right direction from the start can save a lot of time searching for the data you need. 

**10 Chapter 1** ■ **Data Sources** 

- “What set of fields make up the primary key for this table?” Or, “What is the grain of this fact table?” 

   - Understanding the level of detail of each table is important in order to know how to filter, group, and summarize the data in the table, and join it to other tables. 

- “Are these records imported directly from the source system, or have they been transformed or merged in some way before being stored in this table?” 

   - This is helpful to know when debugging data that doesn’t look like you expected. If the database is “raw” data from the source system, you might talk to those entering the data to learn more about it. If it has gone through a transformation or includes data from several different tables in the system of origin, then the first stop to understand a value would likely be the ETL engineers who programmed the code that modified it. 

- “Is this a static snapshot table, or does it update regularly? At what frequency does it update? And are older records expired and kept as new data is added, or is the existing record overwritten when changes occur?” If a table you’re querying contains “live” data that is being updated as you work, and you are using it to perform calculations or as an input to a machine learning algorithm, you may want to make a copy of it to use while working. That way, you know that changes in the calculations or model output are due to changes in your code, and not due to data that is changing as you debug. 

For datasets updated on a nightly basis, you might want to know what time they refresh, so you can schedule other things that depend on it, like an extract refresh, to occur after the table gets the latest data. 

   - If old records are maintained in the table as a log, you can use the expiration date to filter out old records if you only want the latest ones, or keep past records if you’re reporting on historical trends. 

- “Is this data collected automatically as events occur, or are the values entered by people? Do we have documentation on the interface that they can see with the data entry form field labels?” 

   - Data entered by people may be more prone to error because of manual entry, but the people doing the data entry are often extremely valuable to talk to if you want to understand the business processes that generated the data. You can ask them why certain values were selected, what might trigger an update of a record, or what automated processes are kicked off when they make a change or process a batch. 

It’s a good idea to check to see how the values in each field are distributed: What is the range of possible values? If a column contains categorical 

**Chapter 1** ■ **Data Sources 11** 

values, how many rows fall into each category? If the column contains continuous or discrete numeric values, what is the shape of the statistical distribution? I find that it helps to visualize the data at this exploratory stage, called Exploratory Data Analysis (EDA). Histograms are especially useful for this purpose. 

Additionally, you might explore the data broken down by time period (such as by fiscal year) to see if those distributions change over time. If you find that they do, you may find out by talking to the SMEs that there is a point at which old records stop being updated, a business process changed, or past values get zeroed out in certain cases, for example. Knowing how their data entry forms look can also help with communication with SMEs about the data, because they may not know the field names in the underlying database but will be able to describe the data using the labels they can see on the front-end interface. 

Knowing the type of database is also important for writing more efficient queries, but that is something you are likely to know from the start, as you will probably need that information in order to connect to it. In some database systems, limiting the number of rows returned will make a query run faster. However, in “columnar” database systems like Redshift, even when limiting results to a single row, returning data from all columns may take longer to complete than summarizing all of the values in a single column across thousands of rows because of how the data is physically stored and compiled behind the scenes before being returned to you. 

Additionally, you will need to know the type of database in order to look up SQL syntax details in the official documentation, since syntax can differ slightly between database systems. 

#### **Introduction to the Farmer’s Market Database** 

The MySQL database we’ll be using for example queries throughout much of this book serves as a tracking system for vendors, products, customers, and sales at a fictional farmer’s market. This relational database contains information about each day the farmer’s market is open, such as the date, the hours, the day of the week, and the weather. There is data about each vendor, including their booth assignments, products, and prices. We’re going to pretend that (unlike at many real farmer’s markets) vendors use networked cash registers to ring up individual items, and customers scan farmer’s market loyalty cards with every transaction, so we have detailed logs of their purchases (we know who purchased which items and exactly when). 

The Farmer’s Market database was designed to allow for demonstration of a variety of queries, including those a data analyst might write to answer business 



<!-- Start of picture text -->
(i<br>1 market_date DATE<br> market_day VARCHAR(45)<br>> market_veek VARCHAR(45) 4<br>© market_year VARCHAR(45) + product_id INT(11)<br>> market_start_time VARCHAR(45)  catoners4Ne(31) vendor.id INT(11)<br>) market_end_time VARCHAR(45) © customer_first_name VARCHAR(45) market_date DATE<br>©>2 specal_nctesmarket_seasonmarket_min_temp7 BLOB VARCHAR(45) VARCHAR(200) A ©ae, customer_last_name canton5p VARCHARLAS)VARCHAR(45) < customer_id©>quantitycost_to_customer_per_qty;  DECIMAL(16,2)INT(11)  DEGIMAL(16,2) r<br>© market_max_temp VARCHAR(45) Lai 1 transaction_tme TIME 1 product_category.id<br>© market_snow_fag INT(11) ‘booth_number INT(11) - ae<br>Indexes market_date DATE<br>Indexes<br>t<br>a = =<br>- ® vendor_id INT(11)  market_date DATE ©<br>* booth number INT(I1) © vendor_name VARCHAR(45) © quantity DEGIMAL(10,0) © preduct_name<br>berth erin evel VCAES) © vendor_type VARCHAR (45) G vendor_jid INT(11) © product_size<br>® booth_description VARCHAR(255) © vendor_owner_first_name VARCHAR(45) product_id INT(11) product_categor_id<br>© booth. type VARCHAR(45) © verdor_owner_last_name VARCHAR(45) © ofiginal_price DECIMAL(10,0) © product_aty_type<br>mae Indexes Indexes Indexes<br><!-- End of picture text -->



<!-- Start of picture text -->
INT(11)<br> VARCHAR(45)<br> VARCHAR(45)<br> INT(11)<br>VARCHAR(45)<br><!-- End of picture text -->

**Chapter 1** ■ **Data Sources 13** 

In this special use case, the set of values in each row can be used as inputs to train a model, and that row is often called a “training example” (or “instance” or “data point”). And each input column is a “feature” (or “input variable”). A machine learning algorithm might rank important features, letting you know which attributes are most useful to the model for making its prediction. The column that contains the output that the model is trying to predict is called the “target variable.” 

By the end of this book, you will have learned how to convert “rows and columns” in database tables into “training examples” with “features” for a predictive model to learn from. 

#### **Exercises** 

1. What do you think will happen in the described Books and Authors database depicted in Figure 1.5 if an author changes their name? Which records might be added or updated, and what might be the effect on the results of future queries based on this data? 

2. Think of something in your life that you could track using a database. What entities in this database might have one-to-many relationships with one another? Many-to-many? 

###### **<mark>C H A P T E R</mark>** 



<!-- Start of picture text -->
2<br><!-- End of picture text -->

## **The SELECT Statement** 

Before we can discuss designing analytical datasets, you first need to understand the syntax of Structured Query Language (SQL), so the next several chapters will cover SQL basics. Throughout the book, you will see many variations on the themes introduced here, combining these basic concepts with increasing complexity, because even the most complex SQL queries boil down to the same basic concepts. 

#### **The SELECT Statement** 

The majority of the queries in this book will be SELECT statements. A SELECT statement is SQL code that retrieves data from the database. When used in combination with other SQL keywords, SELECT can be used to view data from a set of columns in a database table, combine data from multiple tables, filter the results, perform calculations, and more. 

**~~NOTE~~ You’ll often see the word** SELECT **capitalized in SQL code, and I chose to follow that formatting standard in this book, because** SELECT **is a reserved SQL** **_keyword_ , meaning it is a special instructional word that the code interpreter uses to execute your query. Capitalizing it visually differentiates the keyword from other text in your query, such as field names.** 

**15** 

**16 Chapter 2** ■ **The SELECT Statement** 

#### **The Fundamental Syntax Structure of a SELECT Query** 

SQL SELECT queries follow this basic syntax, though most of the clauses are optional: 

SELECT [columns to return] FROM [schema.table] WHERE [conditional filter statements] 

GROUP BY [columns to group on] HAVING [conditional filter statements that are run after grouping] 

ORDER BY [columns to sort on] 

The SELECT and FROM clauses are generally required, because those indicate which columns to select and from what table. The words in brackets are placeholders, and as you go through the next several chapters of this book, you will learn what to put in each section. 

#### **Selecting Columns and Limiting the Number of Rows Returned** 

The simplest SELECT statement is 

SELECT * FROM [schema.table] 

where [schema.table] is the name of the database schema and table you want to retrieve data from. 

**~~NOTE~~ In Chapter 5, “SQL JOINs,” you’ll learn the syntax for pulling data from multiple tables at once.** 

For example, 

SELECT * FROM farmers_market.product 

can be read as “Select everything from the product table in the farmers_market schema.” The asterisk really represents “all columns,” so technically it’s “Select all columns from the product table in the farmers_market schema,” but since there are no filters in this query (no WHERE clause, which you’ll learn about in Chapter 3, “The WHERE Clause”), it will also return all rows, hence “everything.” 

There is another optional clause I didn’t include in the basic SELECT syntax in the previous section: the LIMIT clause. (The syntax is different in some database systems. See the note about the TOP keyword and WHERE clause.) I frequently use LIMIT while developing queries. LIMIT sets the maximum number of rows 

|product_id|product_name|product_size|product_category_id|product_qty_type|
|---|---|---|---|---|
|1|Habanero Peppers<br>- Organic|medium|sf|lbs|
|Z<br>|Jalapeno Peppers<br>- Organic<br><br>|small<br>|a |<br>|lbs<br>|
|3|Poblano Peppers<br>- Organic|large|af|unit|
|4|Banana Peppers<br>-<br>Jar|8 oz|3|unit|
|5|Whole Wheat<br>Bread|1.5<br>lbs|3|unit|



product_id product_name 1 Habanero Peppers - Organic 2 Jalapeno Peppers - Organic 3 Poblano Peppers - Organic 7 Banana Peppers - Jar 5 Whole Wheat Bread 



<!-- Start of picture text -->
market_date vendor_id booth_number<br>2019-03-13 4 2<br>2019-83-89 3 1<br>2019-03-82 4 7<br>2019-83-62 1 2<br>2019-03-13 8 6<br><!-- End of picture text -->



<!-- Start of picture text -->
product_id product_name<br>7 Apple Pie<br>7 Banana Peppers - Jar<br>8 Cherry Pie<br>6 Cut Zinnias Bouquet<br>18 Eges<br><!-- End of picture text -->



<!-- Start of picture text -->
product_id product_name<br>11 Pork Chops<br>18 Eggs<br>9 Sweet Potatoes<br>8 Cherry Pie<br>y 4 Apple Pie<br><!-- End of picture text -->



<!-- Start of picture text -->
market_date vendor_id booth_number<br>2019-03-02 1 2<br>2019-83-82 =| 1<br>2019-03-02 4 iF<br>2019-83-82 7 11<br>2019-03-02 8 6<br><!-- End of picture text -->

|market_date|customer_id|vendor_id|quantity|cost_to_customer_per_qty|
|---|---|---|---|---|
|2019-@3-@2|4|8|2.08|4.28|
|2019-83-62|18|8|1.08|4.08|
|2019-@3-@9|12|8|1.08|4.08|
|2019-83-09|5|9|1.08|16.08|
|2019-@3-89|aE|9|1.00|18.68|
|2019-03-02|2|-|4.68|2.08|
|2019-03-82|3|a|8.48|2.08|
|2019-83-62|4|4|1.48|2.08|
|2019-@3-@9|4|4|9.98|2.08|
|2019-83-02|1|1|1.08|5.50|



|7<br>| market_date<br>|customer_id<br>|vendor_id<br>|quantity<br>|cost_to_customer_per_qty <br>|ag<br>|
|---|---|---|---|---|---|
||2019-@3-02<br>|4<br>|8<br>|2.00<br>|4.08<br>|“8.0000<br>|
||2019-03-02|1e|8|1.08|4.28|4.0808|
|<br>|<br>2019-83-89<br>|12<br>|8<br>|1.08<br>|4.08<br>|4.0808<br>|
||2019-03-09|5|9|1.08|16.08|16.8008|
||2019-@3-@9<br>|1<br>|9<br>|1.00<br>|18.00<br>|18.0000<br>|
||2019-03-e2|2|o|4.68|2.080|9.2000|
|2019-03-02<br>|3<br>|><br>|8.48<br>|2.08<br>|16.8008<br>|
||2019-@3-02|4|o|1.48|2.08|2.8000|
||<br>2019-83-09<br>|4<br>|-<br>|9.98<br>|2.08<br>|19.8800<br>|
||2@19-@3-@2|i|1|1.08|5.58|5.5008|



|| market_date<br>|customer_id<br>|vendor_id<br>|price<br>|
|---|---|---|---|
|| 2019-03-02<br>|4<br>|8<br>|8.8080<br>|
||2019-03-@2|18|8|4.0808|
|<br>2019-83-89|12|8|4.0000|
|2019-83-69|5|9|16.0808|
|2019-@3-89<br>|Z<br>|9<br>|18.8008<br>|
|| 2019-03-02|2|4|9.2080|
|| 2019-@3-@2<br>|3<br>|os<br>|16.8000<br>|
|neae|**4**|4|2.808**0**|
|| <sup>2019-83-69</sup><br>||o<br>|19.80 8<br>|
||2@19-@3-e2|1|1|5.5000|



|market_date|customer_id|vendor_id|price|
|---|---|---|---|
|2019-03-82|4|8|8.08|
|2019-83-02|18|8|4.08|
|2019-@3-@9|12|8|4.08|
|2019-@3-69|5|9|16.00|
|2019-03-09|Zz|9|18.00|
|2019-83-62|2|-|9.28|
|2019-83-82|3|o|16.88|
|2019-83-62|4|4|2.88|
|2019-83-89|4|4|19.80|
|2019-83-62|1|1|5.58|





<!-- Start of picture text -->
1customer_id Janecustomer_first_name Connorcustomer_last_name 22801customer_zip|<br>2 Manuel Diaz 22803<br>3 Bob Wilson 22803<br>4 Deanna Washington 22801<br>5 Abigail Harris 22801<br><!-- End of picture text -->



<!-- Start of picture text -->
customer_id customer_name<br>la Jane Connor<br>2 Manuel Diaz<br>3 Bob Wilson<br>4 Deanna Washington<br>5 Abigail Harris<br><!-- End of picture text -->



<!-- Start of picture text -->
customer_id customer_name<br>7 Jessica Armenta<br>6 Betty Bullard<br>1 Jane Connor<br>2 Manuel Diaz<br>10 Russell Edwards<br><!-- End of picture text -->



<!-- Start of picture text -->
customer_id customer_name<br>F 4 ARMENTA, JESSICA<br>6 BULLARD, BETTY<br>1 CONNOR, JANE<br>2 DIAZ, MANUEL<br>18 EDWARDS, RUSSELL<br><!-- End of picture text -->

**26 Chapter 2** ■ **The SELECT Statement** 

**~~NOTE~~ Note that we did not sort on the new derived column alias** customer_ name **here, but on columns that exist in the** customer **table. In some cases (depending on what database system you’re using, which functions are used, and the execution order of your query) you can’t reuse aliases in other parts of the query. It is possible to put some functions or calculations in the ORDER BY clause, to sort by the resulting value. Some other options for referencing derived values will be covered in later chapters.** 

#### **Evaluating Query Output** 

When you are developing a SQL SELECT statement, how do you know if the result will include the rows and columns you expect, in the form you expect? 

As previously demonstrated, one method is to run the query with a LIMIT each time you make a modification. This gives a quick preview of the first _x_ number of rows to ensure the changes you expect to see are returned, and you can inspect the column names and format of a few output values to verify that they look the way you intended. 

However, you still might want to confirm how many rows would have been returned if you hadn’t placed the LIMIT on the results. Similarly, there’s the concern that your function might not perform as expected on some values that didn’t appear in your limited results preview. 

I therefore use the query editor to help me review the results of my query a bit further. This method doesn’t provide a full quality control of the output (which should be done before putting any query into production), but it can give me a sanity check that the output looks correct enough for me to continue on with my work. To demonstrate, we’ll use the “rounded price” query from the earlier “More Inline Calculation Examples: Rounding” section. 

First, I remove the LIMIT. Note that your query editor might have a built-in limit (such as 2000 rows) to prevent you from generating a gigantic dataset by accident, so you might need to go into the settings and turn off any pre-set row limits to actually return the full dataset. Figure 2.15 shows the “Don’t Limit” option available in MySQL Workbench, under the Query menu. 

Then, I’ll run the query to generate the output for inspection: 

SELECT 

market_date, customer_id, vendor_id, ROUND(quantity * cost_to_customer_per_qty, 2) AS price FROM farmers_market.customer_purchases 



<!-- Start of picture text -->
Query Database Server Tools Scripting Help<br>| Execute (All or Selection) Ctrl+Shift+Enter<br>| Execute (All or Selection) to Text<br>Execute Current Statement Ctrl+Enter<br>Execute Current Statement (Vertical Text Output)Ctrl+Alt+Enter<br>Explain Current Statement Ctrl+Alt+X<br>Stop<br>Stop Script Execution on Errors<br>Collect Performance Schema Stats a=<br>Reconnect to Server Limitto 50 rows<br>New Tab to Current Server Ctrl+Shift+T Limitto 100 rows<br>¥  Auto-Commit Transactions Limitto 200 rows<br>Commit Transaction Limitto 300 rows<br>| Rollback Transaction Limitto 400 rows<br>Commit Result Edits Limitto 500 rows<br>Discard Result Edits Limitto 1000 rows<br>Export Results Limit to 2000 rows<br>—_—_CS.S Ss Limitto 5000 rows<br>Limitto 10000 rows<br>Limitto 50000 rows<br><!-- End of picture text -->

|| R|esult<br>Grid|fH|4FiterRows:||||Export:fy<br>|wrapCellContent:i|
|---|---|---|---|
||<br>market_date|<br>customer_id|<br>    <br>vendor_id<br>price|
|>|2019-83-82|4|8<br>8.08|
||2019-83-82|18|8<br>4.00|
||2019-83-89|12|8<br>4.08|
||2019-83-89|5|9<br>16.08|
||2019-83-89|1|9<br>18.08|
||2019-83-89|12|9<br>54.00|
||2019-83-82|2|4<br>9.20|
||2019-83-82|3|4<br>16.88|
||2019-03-82|=|4<br>2.80|
||2019-03-09|7|4<br>19.88|
||2019-03-82|1|EE<br>5.50|
||2019-03-02|Es|1<br>15.08|
||2019-83-89|1|1<br>11.08|
||nain<br>arzan|oA|.<br>©<br>cA|
|Res|ult 30<br>x|||
|Out|put|||
|Gl|Action Output|.||
||=<br>Time|Action|Message|
|rv}|1 01:17:34|SELECT<br>market_d|ate.<br>customer_id.<br>vendor_id.<br>©ROUND(quantity<br>*cost_to_customer_per_aty. 2)... 21 row(s)retumed|





<!-- Start of picture text -->
market_date customer_id vendor_id price<br>2019-@3-@2 4 8 8.08<br>2019-83-02 18 & 4.08<br>2019-83-02 2 4 9.28<br>2019-03-02 3 4 16.88<br>2019-@3-@2 4 4 2.88<br>2019-83-02 1 ms 5.58<br>2019-83-02 1 1 15.68<br>2019-83-02 1 i 28.48<br>2019-83-89 12 8 4.08<br>2019-@3-@9 5 9 16.08<br>2019-83-69 1 9 18.88<br>2019-@3-@9 4 4 19.88<br>2019-83-89 1 1 11.00<br>2019-@3-@9 4 1 5.58<br>2019-83-69 12 1 10.88<br>2019-@3-@9 4 7 6.08<br>2019-83-89 7 7 6.08<br>2019-83-89 12 - 6.08<br>2019-83-69 1 7 12.65<br>2019-@3-@9 4 Z 225<br><!-- End of picture text -->

|| market_date|customer_id|vendor_id|price|
|---|---|---|---|
|2019-03-82|1|z|5.58|
|2019-03-02|1|5 ||15.08|
|2019-83-89|e ||a3|11.00|
|2019-83-89|4|=|5.58|
|2019-03-82|1|a|28.48|
|2019-83-89|12|Zz|18.88|
|2019-03-02|2|4|9.28|
|2019-03-82|2)|4|16.88|
|2019-83-02|4|4|2.88|
|2019-83-89|4|4|19.88|
|2019-83-89|4|7|6.88|
|2019-@3-@9|7|y|6.08|
|2019-83-89|12|7|6.08|
|2019-83-89|1|7|12.65|
|2019-83-89|4|7|1.73|
|2019-83-02|4|8|8.80|
|2019-03-02|1é|8|4.08|
|2019-83-89|12|8|4.08|
|2019-@3-@9|5|9|16.88|
|2019-83-89|s E|9|18.08|



|vendor_id|vendor_name|vendor_type|vendor_owner_first_name|vendor_owner_last_name|
|---|---|---|---|---|
|3|Hernandez Salsa & Veggies|Fresh Variety: Veggies & More|Maria|Hernandez|
|4|Mountain View Vegetables|Fresh Variety: Veggies & More|Joseph|Yoder|
|6|Seashell Clay Shop|Arts & Jewelry|Karen|Soula|
|7|Mother's Garlic & Greens|Fresh Variety: Veggies & More|Vera|Gordon|
|8|Marco's Peppers|Fresh Focused|Marco|Bokashi|
|9|Annie's Pies|Prepared Foods|Annie|Aquinas|
|16|Mediterranean Bakery|Prepared Foods|Kani|Hardi|
|11|Fields of Corn|Fresh Focused|Samuel|Smith|



|vendor_name|vendor_id|vendor_type||
|---|---|---|---|
|Annie's Pies|9|Prepared Foods||
|Chris's Sustainable Eggs & Meats|1|Eggs & Meats||
|Fields of Corn|11|Fresh Focused||
|Hernandez Salsa & Veggies|3|Fresh Variety:|Veggies & More|
|Marco's Peppers|8|Fresh Focused||
|Mediterranean Bakery|16|Prepared Foods||
|Mother's Garlic & Greens|7|Fresh Variety:|Veggies & More|
|Mountain View Vegetables|4|Fresh Variety:|Veggies & More|
|Seashell Clay Shop|6|Arts & Jewelry||



###### **<mark>C H A P T E R</mark>** 

# **3** 

## **The WHERE Clause** 

Now that you have the basic idea of how SQL queries look and have learned how to return the columns of data that you want from a single database table, we can talk about how to filter that result to include only the rows that you want returned. 

#### **The WHERE Clause** 

The WHERE clause is the part of the SELECT statement in which you list conditions that are used to determine which rows in the table should be included in the results set. In other words, the WHERE clause is used for filtering. 

If you have programmed in other languages, you have likely encountered other conditional statements such as “IF” statements, which use boolean logic (think “AND” or “OR”) to determine what action to take, based on whether certain conditions are met. SQL uses boolean logic to check the available data against conditions in your WHERE clause to determine whether to include each row in the output. 

I use the WHERE clause in almost every query I write as a data scientist to accomplish things like narrowing down categories of records to be displayed in a report, or filtering a dataset to a particular date range from the past that will be used to train a predictive model. 

**31** 



<!-- Start of picture text -->
product_id product_name product_category_id<br>3 Habanero Peppers - Organic 1<br>2 Jalapeno Peppers - Organic 1<br>3 Poblano Peppers - Organic 1<br>9 Sweet Potatoes z<br>12 Baby Salad Lettuce Mix - Bag 1<br><!-- End of picture text -->

market_date customer_id vendor_id product_id quantity price |2019-@3-@2 a . 9 1.48 2.8008 2019-83-02 4 8 ~ 2.08 8.0088 2019-83-89 o ES 18 1.08 5.5008 2019-83-89 4 4 9 9.98 19.8008 2019-83-89 o 7 12 2.08 6.0000 

**34 Chapter 3** ■ **The WHERE Clause** 

**Table 3.1** 

|**MARKET_**<br>**DATE**|**CUSTOMER_**<br>**ID**|**VENDOR_ID**|**PRODUCT_**<br>**ID**|**QUANTITY**|**PRICE**|**CONDITION:**<br>**CUSTOMER_**<br>**ID = 4**|
|---|---|---|---|---|---|---|
|2019-03-02|3|4|4|8.4|16.80|FALSE|
|2019-03-02|1|1|11|1.7|20.40|FALSE|
|2019-03-02|**4**|4|9|1.4|2.80|**TRUE**|
|2019-03-02|**4**|8|4|2.0|8.00|**TRUE**|
|2019-03-09|5|9|7|1.0|16.00|FALSE|
|2019-03-09|**4**|1|10|1.0|5.50|**TRUE**|
|2019-03-09|**4**|4|9|9.9|19.80|**TRUE**|
|2019-03-09|**4**|7|12|2.0|6.00|**TRUE**|
|2019-03-09|**4**|7|13|0.3|1.72|**TRUE**|
|2019-03-16|3|4|9|5.5|11.00|FALSE|
|2019-03-16|3|9|8|1.0|18.00|FALSE|



#### **Filtering on Multiple Conditions** 

You can combine multiple conditions with boolean operators, such as “AND,” “OR,” or “AND NOT” between them in order to filter using multiple criteria in the WHERE clause. 

Clauses with OR between them will jointly evaluate to TRUE, meaning the row will be returned, if _any_ of the clauses are TRUE. Clauses with AND between them will only evaluate to TRUE in combination if _all_ of the clauses evaluate to TRUE. Otherwise, the row will not be returned. Remember that NOT flips the following boolean value to its opposite (TRUE becomes FALSE, and vice versa). See Table 3.2. 

**Table 3.2** 

|**CONDITION 1**<br>**EVALUATES TO**|**BOOLEAN**<br>**OPERATOR**|**CONDITION 2**<br>**EVALUATES TO**|**ROW RETURNED?**|
|---|---|---|---|
|TRUE|OR|FALSE|_TRUE_|
|TRUE|OR|TRUE|_TRUE_|
|FALSE|OR|FALSE|_FALSE_|
|TRUE|AND|FALSE|_FALSE_|
|TRUE|AND|TRUE|_TRUE_|
|TRUE|AND NOT|FALSE|_TRUE_|



**Chapter 3** ■ **The WHERE Clause 35** 

|**CONDITION 1**|**BOOLEAN**|**CONDITION 2**||
|---|---|---|---|
|**EVALUATES TO**|**OPERATOR**|**EVALUATES TO**|**ROW RETURNED?**|
|FALSE|AND NOT|TRUE|_FALSE_|
|FALSE|AND NOT|FALSE|_FALSE_|
|FALSE|OR NOT|FALSE|_TRUE_|



So if the WHERE clause lists two conditions with OR between them, like “WHERE customer_id = 3 OR customer_id = 4,” then each condition will be evaluated for each row, and rows where the customer_id is either 3 or 4 (either condition is met) will be returned, as shown in Table 3.3 (some columns have been removed for readability). 

**Table 3.3** 

|**MARKET_**<br>**DATE**|**CUS**<br>**_ID**|**TOMER**|**VENDOR**<br>**_ID**|**PRICE**|**CONDITION:**<br>**CUSTOMER_**<br>**ID = 3**|**OR**|**CONDITION:**<br>**CUSTOMER_**<br>**ID = 4**|**ROW**<br>**RETURNED?**|
|---|---|---|---|---|---|---|---|---|
|2019-03-02||**3**|4|16.80|**TRUE**|_OR_|FALSE|**_TRUE_**|
|2019-03-02||1|1|20.40|FALSE|_OR_|FALSE|_FALSE_|
|2019-03-02||**4**|4|2.80|FALSE|_OR_|**TRUE**|**_TRUE_**|
|2019-03-02||**4**|8|8.00|FALSE|_OR_|**TRUE**|**_TRUE_**|
|2019-03-09||5|9|16.00|FALSE|_OR_|FALSE|_FALSE_|
|2019-03-09||**4**|1|5.50|FALSE|_OR_|**TRUE**|**_TRUE_**|
|2019-03-09||**4**|4|19.80|FALSE|_OR_|**TRUE**|**_TRUE_**|
|2019-03-09||**4**|7|6.00|FALSE|_OR_|**TRUE**|**_TRUE_**|
|2019-03-09||**4**|7|1.72|FALSE|_OR_|**TRUE**|**_TRUE_**|
|2019-03-16||**3**|4|11.00|**TRUE**|_OR_|FALSE|**_TRUE_**|
|2019-03-16||**3**|9|18.00|**TRUE**|_OR_|FALSE|**_TRUE_**|



Because there is an OR between the two conditions, only one of the conditions has to evaluate to TRUE in order for a row to be returned. 

In fact, if there is a long list of conditions, with OR between all of them, only one condition in the entire list has to evaluate to TRUE per row in order for the row to be returned, because it can be read as “Either [Condition 1] is TRUE OR [Condition 2] is TRUE OR [Condition 3] is TRUE,” etc. So, only if _all_ items in the list of “OR conditions” evaluate to FALSE is a row not returned. 

|market_date|customer_id|vendor_id|product_id|quantity|price|
|---|---|---|---|---|---|
|2019-@3-@2|3|7|9|8.48|16.8008|
|2019-83-62|o|.|9|1.48|2.8008|
|2019-83-82|=|8|=|2.88|8.8008|
|2019-83-89|o|1|18|1.08|5.5000|
|2019-83-89|-|4|9|9.98|19.8800|
|2019-83-89|os|7|12|2.08|6.8008|
|2019-83-89||7|13|6.38|1.7258|
|2019-83-16|3|.|9|5.50|11.0008|
|2019-83-16|3|9|8|1.08|18.0888|





**Chapter 3** ■ **The WHERE Clause 37** 

|**MARKET_**|**CUSTOMER**|**VENDOR**||**CONDITION:**<br>**CUSTOMER_**||**CONDITION:**<br>**CUSTOMER_**|**ROW**|
|---|---|---|---|---|---|---|---|
|**DATE**|**_ID**|**_ID**|**PRICE**|**ID = 3**|**AND**|**ID = 4**|**RETURNED?**|
|2019-03-09|**4**|1|5.50|FALSE|_AND_|**TRUE**|_FALSE_|
|2019-03-09|**4**|4|19.80|FALSE|_AND_|**TRUE**|_FALSE_|
|2019-03-09|**4**|7|6.00|FALSE|_AND_|**TRUE**|_FALSE_|
|2019-03-09|**4**|7|1.72|FALSE|_AND_|**TRUE**|_FALSE_|
|2019-03-16|**3**|4|11.00|**TRUE**|_AND_|FALSE|_FALSE_|
|2019-03-16|**3**|9|18.00|**TRUE**|_AND_|FALSE|_FALSE_|



The correct way to read a query with the conditional statement “WHERE customer_id = 3 AND customer_id = 4” is “Return each row where the customer ID is 3 and the customer ID is 4.” But there is only a single customer_id value per row, so it’s impossible for the customer_id to be both 3 and 4 at the same time, therefore no rows are returned! 

Some people make the mistake of reading the logical AND operator the way we might request in English, “Give me all of the rows with customer IDs 3 and 4,” when what we really mean by that phrase is “Give me all of the rows where the customer ID is either 3 or 4,” which would require an OR operator in SQL. 

When the AND operator is used, _all_ of the conditions with AND between them must evaluate to TRUE for a row in order for that row to be returned in the query results. 

One example where you could use AND in a WHERE clause referring to only a single column is when you want to return rows with a range of values. If someone requests “Give me all of the rows with a customer ID greater than 3 and less than or equal to 5,” the conditions would be written as “WHERE customer_id > 3 AND customer_id <= 5,” and would evaluate as shown in Table 3.5. 

Because of the AND, both conditions must evaluate to TRUE in order for a row to be returned. 

Let’s try it in SQL, and see the output in Figure 3.4: 

###### SELECT 

market_date, customer_id, vendor_id, product_id, 



|market_date|customer_id|vendor_id|product_id|quantity|price|
|---|---|---|---|---|---|
|2019-83-82|=|4|9|1.48|2.8008|
|2019-83-82||8|-|2.08|8 .e800|
|2019-83-89||1|18|1.08|5.5000|
|2019-83-89|=|ae|9|9.98|19.8088|
|2019-83-89|-|7|12|2.08|6.2008|
|2019-83-89|ae|7|a|@.38|1.7258|
|2019-83-89|5|9|7|1.08|16.0008|





<!-- Start of picture text -->
| product_id product_name<br>la Banana Peppers - Jar<br>|5 Whole Wheat Bread<br>\6 Cut Zinnias Bouquet<br>r7 AppleEggs Pie<br><!-- End of picture text -->



<!-- Start of picture text -->
product_id product_name<br>l4 Banana Peppers - Jar<br>5 Whole Wheat Bread<br>6 Cut Zinnias Bouquet<br>7 Apple Pie<br><!-- End of picture text -->

market_date customer_id vendor_id price 2019-83-89 4 7 6.8088 2019-83-89 4 7 1.7250 



<!-- Start of picture text -->
2 Manuel Diaz<br>17 Carlos Diaz<br><!-- End of picture text -->



<!-- Start of picture text -->
9 8 2019-83-82<br>9 & 2019-83-89<br><!-- End of picture text -->



<!-- Start of picture text -->
vendor_id booth_number market_date<br>7 11 2019-83-02<br>7 at 2019-83-89<br>7 11 2019-83-13<br><!-- End of picture text -->



<!-- Start of picture text -->
customer_id customer_first_name customer_last_name<br>17 Carlos Diaz<br>2 Manuel Diaz<br>18 Russell Edwards<br>3 Bob Wilson<br><!-- End of picture text -->

customer_id customer_first_name customer_last_name 13 Jeremy Gruber 18 Jeri Mitchell 



<!-- Start of picture text -->
product_id product_name product_size product_category_id product_qty_type<br>14...14 + +46—RedRed  PotatoesPotatoes ©=5=5©)—<~<3Wd rr 1 (<t;t;t””””CtCQTttt”~OOOO oespO<br><!-- End of picture text -->



<!-- Start of picture text -->
product_id product_name product_size product_category_id product_qty_type<br>14 Red Potatoes (ae 1<br>15 Red Potatoes - Small 1 coy<br><!-- End of picture text -->



<!-- Start of picture text -->
market_date transaction_time customer_id vendor_id quantity<br>2019-83-89 08:42:08 | 7 2.28<br>2019-@3-2@ 8:25:08 1 rj 3.18<br><!-- End of picture text -->

market_date transaction_time customer_id vendor_id quantity 

|market_date|transaction_time|customer_id<br>vendor_id|quantity|
|---|---|---|---|
|2019-83-89|08:42:08|1<br>7|2.28|
|2019-63-89|08:43:68|1<br>7||
|2019-83-28|08:25:08|EE<br>7|3.18|



|market_date|market_rain_flag|
|---|---|
|2019-83-28|1|
|2019-83-23<br>2019-83-30|a 3<br>1|





<!-- Start of picture text -->
market_date customer_id vendor_id price<br>2019-83-28 7 7 9.8088<br>2019-03-23 4 Fé 9.0086<br>2019-@3-30 12 7 3.0088<br>2019-83-20 1 7 17.8258<br>2019-@3-23 4 7 13.8800<br><!-- End of picture text -->

###### **<mark>C H A P T E R</mark>** 

# **4** 

## **CASE Statements** 

In Chapters 2, “The SELECT Statement,” and 3, “The WHERE Clause,” you learned how to specify which columns and rows you want to pull from a database table into your dataset. We used the WHERE clause to filter rows using conditional statements that must evaluate to TRUE in order for a row to be returned. 

But what if, instead of using conditional statements to filter rows, you want a column or value in your dataset to be based on a conditional statement? For example, instead of filtering your results to purchases over $50, say you just want to return all rows and create a new column that flags each purchase as being above or below $50? Or, maybe the machine learning algorithm you want to use can’t accept a categorical string column as an input feature, so you want to encode those categories into numeric values. These are a version of what SQL developers call “derived columns” or “calculated fields,” and creating new columns that present the values differently is what data scientists call “feature engineering.” This is where CASE statements come in. 

**~~NOTE~~ If you’re familiar with other scripting languages like Python that use “if” statements, you’ll find that SQL handles conditional logic somewhat similarly, just with different syntax.** 

**49** 

**50 Chapter 4** ■ **CASE Statements** 

#### **CASE Statement Syntax** 

You use conditional reasoning in your daily life any time you think “If [one condition] is true, then [take this action]. Otherwise, [take this other action].” “If the weather forecast predicts it will rain today, then I’ll take an umbrella with me. Otherwise, I’ll leave the umbrella at home.” In SQL, the code to delineate this type of logic is called a CASE statement, which uses the following syntax: 

CASE WHEN [first conditional statement] THEN [value or calculation] WHEN [second conditional statement] THEN [value or calculation] ELSE [value or calculation] END 

This statement indicates that you want a column to contain different values under different conditions. If we put the umbrella example into this form: 

CASE WHEN weather_forecast = 'rain' THEN 'take umbrella' ELSE 'leave umbrella at home' END 

the WHENs are evaluated in order, from top to bottom, and the first time a condition evaluates to TRUE, the corresponding THEN part of the statement is executed, and no other WHEN conditions are evaluated. 

To illustrate, consider this nonsense query: 

SELECT CASE WHEN 1=1 THEN 'Yes' WHEN 2=2 THEN 'No' END 

This query will always evaluate to “Yes,” because 1=1 is always TRUE, and therefore the 2=2 conditional statement is never evaluated, even though it is also true. 

The ELSE part of the statement is optional, and that value or calculation result is returned if none of the conditional statements above it evaluate to TRUE. If the ELSE is not included and none of the WHEN conditionals evaluate to TRUE, the resulting value will be NULL. 

You should always alias columns that contain CASE statements so the resulting column headers are readable, as demonstrated in the queries in this chapter. 

vendor_type Arts & Jewelry Eggs & Meats Fresh Focused Fresh Variety: Veggies & More Prepared Foods 

|vendor_id|vendor_name|vendor_type||vendo|r_type_condensed|
|---|---|---|---|---|---|
|1|Chris's Sustainable Eggs & Meats|Eggs & Meats||Other||
|3|Herndndez Salsa & Veggies|Fresh Variety:|Veggies & More|Fresh|Produce|
|=|Mountain View Vegetables|Fresh Variety:|Veggies & More|Fresh|Produce|
|6|Seashell Clay Shop|Arts & Jewelry||Other||
|7|Mother's Garlic & Greens|Fresh Variety:|Veggies & More|Fresh|Produce|
|8|Marco's Peppers|Fresh Focused||Fresh|Produce|
|9|Annie's Pies|Prepared Foods||Other||
|18|Mediterranean Bakery|Prepared Foods||Other||
|ae|Fields of Corn|Fresh Focused||Fresh|Produce|



market_date market_day 2019-83-82 Saturday 2019-83-89 Saturday 2019-@3-13 Wednesday 2019-@3-16 Saturday 2019-83-28 Wednesday 

market_date weekend_flag 2019-83-62 1 2019-03-69 1 2019-@3-13 @ 2019-03-16 1 2019-03-20 8 

|market_date<br>|customer_id|vendor_id|price|price_over_5@|
|---|---|---|---|---|
||<br>2019-@3-02|-|8|8.08|@|
|2019-03-82|18|8|4.08|@|
|2019-83-89|12|8|4.08|@|
|2019-03-89|5|9|16.00|@|
|2019-83-69|1|9|18.00|@|
|2019-@3-@9|12|9|54.00|1|
|2019-83-02|2|-|9.28|@|
|2019-03-82|3|a|16.80|@|
|2019-03-62|4|4|2.88|@|
|2019-83-89|4|4|19.88|@|



|market_date|customer_id|vendor_id|price|price_bin|
|---|---|---|---|---|
|2019-03-82|4|8|8.08|$5-$9.99|
|2019-83-82|18|8|4.08|Under $5|
|2019-83-89|12|8|4.08|Under $5|
|2019-03-89|5|9|16.06|$10-$19.99|
|2019-83-89|1|9|18.00|$10-$19.99|
|2019-83-89|12|9|54.08|$28 and Up|
|2019-@3-@2|2|4|9.28|$5-$9.99|
|2019-83-82|||4|16.86|$10-$19.99|
|2019-83-62|4|os|2.88|Under $5|
|2019-83-89|4|4|19.86|$10-$19.99|



|market_date|customer_id|vendor_id|price|price_bin_lower_end|
|---|---|---|---|---|
|2019-@3-@2|4|8|8.08|5|
|2019-83-02|16|8|4.08|e|
|2019-83-89|12|8|4.08|e|
|2019-83-89|5|9|16.08|18|
|2019-83-89|£|9|18.08|18|
|2019-83-89|12|9|54.08|28|
|2019-@3-@2|2|4|9.20|5|
|2019-83-82|3|4|16.88|18|
|2019-83-82|i|4|2.88|e|
|2019-83-89|4|4|19.88|18|



**56 Chapter 4** ■ **CASE Statements** 

your query if you were building it to be used in a report, because the price_bin column is a more explanatory label for the bin, but will sort alphabetically instead of in bin value order. With both available to use in your report, you could use the numeric version of the column to sort the bins correctly, and the string version to label the bins. 

Remember that because neither of the preceding queries included an ELSE inside the CASE statement, the output will be NULL if the quantity field is blank or the calculation can’t be completed with the available values for whatever reason. 

If there is a mis-entered price, or perhaps a record of a refund, and the value in the price column turns out to be negative in one row, what do you think will happen? In the preceding queries, the first condition is “less than 5,” so negative values will end up in the “Under $5,” or 0, bin. Therefore, the name price_bin_lower_end is a misnomer, since 0 might not actually represent the lowest value possible in the first bin. It’s important when writing CASE statements for analytical purposes to determine what the result will be if there end up being unexpected values in any of the referenced database fields. 

#### **Categorical Encoding Using CASE** 

When developing datasets for machine learning, you will often need to “encode” categorical string variables as numeric variables, in order for a mathematical algorithm to be able to use them as input. 

If the categories represent something that can be sorted in a rank order, it might make sense to convert the string variables into numeric values that represent that rank order. For example, the vendor booths at the farmer’s market are rented out at different costs, depending on their size and proximity to the entrance. These booth price levels are labeled with the letters “A,” “B,” and “C,” in order by increasing price, which could be converted into either numeric values 1, 2, 3 or the actual booth prices. The following CASE statement converts the booth price levels into numeric values, and the results are shown in Figure 4.8: 

SELECT booth_number, booth_price_level, CASE WHEN booth_price_level = 'A' THEN 1 WHEN booth_price_level = 'B' THEN 2 WHEN booth_price_level = 'C' THEN 3 END AS booth_price_level_numeric FROM farmers_market.booth LIMIT 5 



<!-- Start of picture text -->
booth_number booth_price_level booth_price_level_numeric<br>ZA1<br>2A 1<br>3B2<br>=e 3<br>5 c 3<br><!-- End of picture text -->



<!-- Start of picture text -->
1vendorid Cheda"svendor_naeSustadeabia fgg: & meets Eggsvender& autatype .wander type_arte_eealry 7wandor_typeeggemests ®vendortyee_frech_tocered ®vasdor_type_frech_variety .verdor_type_preperes<br>3 Nerndnder Salsa & Veggies Fresh Variety: Veggies & More @ . ® 1 *<br>4 Mewetain view vegetusier Frags vaedety: veggies & mare © 8 ® a .<br>4 ‘Seashell Clay Sop Arte & Jewelry 1 . ® a *<br>? Menner's Garlic & Greens Frags viedety: Veggies & mace © 8 ® a .<br>4 Merco"s Peppers Fresh Focused ® a 1 2 *<br>9 Anade's Pies Peepaces Fosas ® 8 ® 8 i<br>w Meaiterransan Bakery Prepared Foods . 2 2 a 1<br>1 Fields of Coon Feeuh Focused ® 8 1 a *<br><!-- End of picture text -->

|customer_id|customer_location_type|
|---|---|
|1|Local|
|2|Not<br>Local|
|3|Not<br>Local|
|7|Local|
|5|Local|
|6|Local|
|7|Not<br>Local|
|8|Not<br>Local|
|9|Local|
|18|Local|





<!-- Start of picture text -->
booth_number booth_price_level_A booth_price_level_B booth_price_level_C<br>1|@e<br>21 @ @<br>3e1e<br>at) @ 1<br>5 @ @ a!<br><!-- End of picture text -->



<!-- Start of picture text -->
C H A P T E R<br><!-- End of picture text -->

**5** 

## **SQL JOINs** 

Now that you have learned how to select the data you want from a database table and filter to the rows you want, you might wonder what to do if the data you need exists across multiple related tables in the database. For example, one analytical question mentioned in Chapter 1, “When is each type of fresh fruit or vegetable in season, locally?” requires data from the product_category table (to filter to the categories with fresh fruit and vegetables), the product table (to get details about each specific item, including product names and quantity types), and the vendor_inventory table (to find out when vendors were selling these products). This is where SQL JOINs come in. 

#### **Database Relationships and SQL JOINs** 

In Chapter 1, “Data Sources,” we introduced different types of database relationships and the entity-relationship diagram (ERD). The type of relationship between database tables, and the key fields that connect them, give us information we need to combine them using a JOIN statement in SQL. 

Let’s say we wanted to list each product name along with its product category name. Since only the ID of the product category exists in the product table, and the product category’s name is in the product_category table, we have to combine the data in the product and product_category tables together in order to generate this list. 

**61** 

product_id* product_category 1 Co | product_name product_category_id* a product_category_id** product_category_name product size product_qty_type 

product_category product product_category_id* 1 product_id* product_category_name co | product_name product_category_id** 



<!-- Start of picture text -->
duct cat duct cat product. product. product_name product.<br>Proguct_category.product_category_id* Productproduct_category_name_category- product_id product_category_id**<br>Organic<br>a CC<br><!-- End of picture text -->

###### Left Join 

All rows from the “left table”, and only rows from the “right table” with matching values in the specified fields 



<!-- Start of picture text -->
product. product. product. product_category. product_category.<br>product_id product_name product_category_id product_category_id product_category_name<br>[2 [steno Pevners-Orgnic |? | | Fresh Frits Vegetables |<br>[4 | Bananarenpers-Jor_ [2 | [| Package Prepared Food |<br>5 | whotewheat@read [3 [| achat Prepared Food |<br>J [curziniassoumser [5 | [S| Pam Flowers<br>[337 [antec|_|Pact Prepared Food|<br>[9 [Handmade| pobysaladtetucommxcanste vee[2 | [2me |feFresh ruits 8 egetabes |<br><!-- End of picture text -->

|product.<br>product_id<br><br>|product.<br>product_name<br>|product.<br>product_category_id<br><br>|product_category.<br>product_category_id<br>|product_category.<br>product_category_name<br>|
|---|---|---|---|---|
|[2<br>[s<br><br>|tenoPevners-Orgnic<br>||?<br>|<br><br>||<br>|FreshFritsVegetables|<br>|
|[4<br>|<br><br>|<br>Bananarenpers-Jor_[<br>|<br><br>2<br>| <br>|<br>[|<br>|<br>PackagePreparedFood|<br>|
|5<br><br><br>|<br>|whotewheat@read<br>|<br>3<br><br>|<br>[|<br>|<br>achatPreparedFood|<br>|
|J<br><br><br><br>|<br>[curziniassoumser[<br>|5<br>| <br>|<br>[S|<br>|<br> PamFlowers<br><br>|
|7<br><br><br><br>|<br>[antec|<br>|<br>_<br>|<br><br> <br>|<br>|<br> <br>|
|||<br>|<br><br>|<br>  <br>|
|[9<br>[H|pobysaladtetucommx<br>andmadecanste|2| <br>vee|[2<br>|<br>me|<br>Freshruits8egetabes|<br>fe|





<!-- Start of picture text -->
product_id product_name product_size product_category_id product_qty_type product_category_id product_category_name<br>1 Habanero Peppers - Organic medium 1 lbs a Fresh Fruits & Vegetables<br>2 Jalapeno Peppers - Organic small 1 lbs 1 Fresh Fruits & Vegetables<br>3 Poblano Peppers - Organic large 1 unit 1 Fresh Fruits & Vegetables<br>4 Banana Peppers - Jar 8 oz 3 unit 3 Packaged Prepared Food<br>5 Whole Wheat Bread 1.5 lbs 3 unit 3 Packaged Prepared Food<br>6 Cut Zinnias Bouquet medium 5 unit 5 Plants & Flowers<br>7 Apple Pie 1e"" 3 unit 3 Packaged Prepared Food<br>8 Cherry Pie 1e"" 3 unit 3 Packaged Prepared Food<br>9 Sweet Potatoes medium 1 lbs 1 Fresh Fruits & Vegetables<br>18 Eggs 1 dozen 6 unit 6 Eggs & Meat (Fresh or Frozen)<br><!-- End of picture text -->

|product_id|product_name|product_prod_cat_id|category_prod_cat_id|product_category_name|
|---|---|---|---|---|
|la|Habanero Peppers - Organic|1|1|Fresh Fruits & Vegetables|
|\2|JalapenoPeppers<br>-Organic|1|1|FreshFruits&Vegetables|
|3|<br> <br>Poblano Peppers<br>- Organic|1|1|<br>Fresh Fruits & Vegetables|
|\4|BananaPeppers<br>-Jar|3|3|PackagedPreparedFood|
||5|<br> <br>WholeWheatBread|3|3|<br>PackagedPreparedFood|
|\6|<br>CutZinniasBouquet|5|5|<br>Plants&Flowers|
|\7|<br>ApplePie|3|3|<br>PackagedPreparedFood|
|8|<br>CherryPie|3|3|<br>PackagedPreparedFood|
|9|<br>Sweet Potatoes|1|1|<br>Fresh Fruits & Vegetables|
|\1e|Eggs|6|6|Eggs&Meat(FreshorFrozen)|
|11|Pork Chops|6|6|<br>Eggs & Meat<br>(Fresh or Frozen)|
|}12|BabySaladLettuceMix<br>-Bag|1|1|FreshFruits&Vegetables|
|13|<br> <br>Baby Salad Lettuce Mix|1|1|<br>Fresh Fruits & Vegetables|





<!-- Start of picture text -->
| product_id product_name product_category_id product_category_name<br>18 Eggs 6 Eggs & Meat (Fresh or Frozen)<br>11 Pork Chops 6 Eggs & Meat (Fresh or Frozen)<br>13 Baby Salad Lettuce Mix 1 Fresh Fruits & Vegetables<br>12 Baby Salad Lettuce Mix - Bag 1 Fresh Fruits & Vegetables<br>1 Habanero Peppers - Organic 1 Fresh Fruits & Vegetables<br>2 Jalapeno Peppers - Organic 1 Fresh Fruits & Vegetables<br>3 Poblano Peppers - Organic 1 Fresh Fruits & Vegetables<br>9 Sweet Potatoes a | Fresh Fruits & Vegetables<br>7 Apple Pie 3 Packaged Prepared Food<br>4 Banana Peppers - Jar 3 Packaged Prepared Food<br>8 Cherry Pie 3 Packaged Prepared Food<br>5 Whole Wheat Bread 3 Packaged Prepared Food<br>6 Cut Zinnias Bouquet 5 Plants & Flowers<br><!-- End of picture text -->

Right Join All rows from the “right table”, and only rows from the “left table” with matching values in the specified fields 

|product.<br>product.<br>product.<br>product_category.<br>product_category.|
|---|
|product_id<br>product_name<br>product_category_id<br>product_category_id<br>product_category_name|



###### Inner Join 

Only rows from the “right table” and “left table” where values in the specified fields have matches in both tables 

product. product. product. product_category. product_category. product_id product_name product_category_id product_category_id product_category_name fa EDBanana Peppers Reppes=- JarCen **ee ee** FreshPackaged Fruits Prepared & VegetablesFood is Cut Zinnias Bouquet ee ee Plants & Flowers aus HE Ee Le Packaged Prepared Food Baby Salad Lettuce Mix ee ee Fresh Fruits & Vegetables 



<!-- Start of picture text -->
customer_id customer_first_name customer_last_name customer_zip product_id vendor_id market_date customer_id quantity cost_to_cust: transacti®<br>5 Abigail Harris 22801 7 9 2019-@3-@9 & 1.08 16.00 10:41:08<br>6 Betty Bullard 22801 oa oo os os om os oa<br>7 Jessica Armenta 22803 12 7 2019-03-09 7 2.00 3.00 11:40:00<br>8 Norma Valenzuela 22803 sesae el os os ons ous ous<br>9 Janet Forbes 22801 brut | Pui | bruit | pris | privis | previ | brut |<br>1e Russell Edwards 22801 4 8 2019-@3-02 10 1.00 4.00 9:12:00<br>11 Richard Paulson 22801 om os oa om cs oa oa<br>12 Jack Wise 22803 4 8 2019-03-09 12 1.00 4.00 13:03:00<br>12 Jack Wise 22803 8 9 2019-83-89 12 3.08 18.00 13:18:08<br>12 Jack Wise 22803 11 1 2019-03-09 12 @.98 12.08 13:10:00<br>12 Jack Wise 22803 12 7 2019-83-69 12 2.08 3.08 13:00:08<br>13 Jeremy Gruber 22803 cas cans cans om a om cms<br>14 William ones 22RA1 coy coy Coa oa a oe — > =<br><!-- End of picture text -->

|customer_id<br>|customer_first_name<br>|customer_last_name<br>|customer_zip<br>|
|---|---|---|---|
|l6|Betty|Bullard|22801|
|8|Norma|Valenzuela|22883|
|9|Janet|Forbes|22801|
|11|Richard|Paulson|22801|
|13|Jeremy|Gruber|22803|
|14|William|Lopes|22801|
|15|Darrell|Messina|22801|



|customer_id|customer_firs|t_name<br>customer_last_name|customer_zip|product_id<br>vendor_id<br>market_date|customer_id<br>quantity|cost_to_c|ust: transacti®|
|---|---|---|---|---|---|---|---|
|4|Deanna|Washington|22801|4<br>8<br>2019-03-02|4<br>2.08|4.08|10:22:08|
|16|Russell|Edwards|22801|o<br>8<br>2019-03-02|16<br>1.08|4.00|09:12:60|
|12|Jack|Wise|22803|4<br>8<br>2019-03-09|12<br>1.08|4.08|13:03:00|
|5|Abigail|Harris|22801|.<br>2019-83-89|5<br>1.08|16.00|10:41:00|
|1|Jane|Connor|22801|8<br>9<br>2019-83-09|1<br>1.08|18.08|08:25:00|
|12|Jack|Wise|22803|8<br>9<br>2019-03-89|12<br>3.00|18.00|13:18:00|
|2|Manuel|Diaz|22803|9<br>4<br>2019-03-02|2<br>4.68|2.00|10:53:00|
|KY|Bob|Wilson|22803|s<br>4<br>2019-03-02|3<br>8.48|2.00|11:39:00|
|4|Deanna|Washington|22801|9<br>4<br>2019-03-02|4<br>1.48|2.08|10:31:00|
|4|Deanna|Washington|22801|9<br>4<br>2019-83-89|4<br>9.98|2.08|13:02:06|
|1|Jane|Connor|22801|1¢e<br>a:<br>2019-03-02|1<br>1.08|5.58|08:59:08|
|1|Jane|Connor|22801|1e<br>1<br>2019-03-02|1<br>3.00|5.00|09:31:00|
|1|Jane|Connor|22801|1e<br>1<br>2019-@3-@9|1<br>2.08|5.58|08:30:00<br>|<br>>|



|| customer_id|customer_firs|t_name customer_last_name|customer_zip|market_date|
|---|---|---|---|---|
|1|Jane|Connor|22801|2019-83-89|
|1|Jane|Connor|22801|2019-03-89|
|1|Jane|Connor|22801|2019-83-89|
|2|Manuel|Diaz|22803|2019-93-13|
|2|Manuel|Diaz|22883|2019-@3-13|
|3|Bob|Wilson|22803|2619-03-16|
|3<br>|Bob<br>|Wilson<br>|22803<br>|2019-83-16<br>|
|4|Deanna|Washington|22801|2819-@3-@89|
|4<br>|Deanna<br>|Washington<br>|22801<br>|2819-83-89<br>|
|4<br>|Deanna<br>|Washington<br>|22801<br>|2019-@3-@9<br>|
|4|Deanna|Washington|22801|2019-83-89|
|5|Abigail|Harris|22801|2019-83-89|
|7|Jessica|Armenta|22883|2019-83-89|
|16|Russell|Edwards|22801|2019-03-16|
|12|Jack|Wise|22803|2019-03-89|
|12|Jack|Wise|22803|2019-83-89|
|12<br>|Jack<br>|Wise<br>|22803<br>|2019-83-16<br>|
|12|Jack|Wise|22803|2019-83-89|





<!-- Start of picture text -->
| customer_id customer_first_name customer_last_name customer_zip market_date<br>1 Jane Connor 22801 2619-83-89<br>1 Jane Connor 22801 2619-83-89<br>1 Jane Connor 22801 2019-83-89<br>2 Manuel Diaz 22803 2019-83-13<br>2 Manuel Diaz 22883 2019-83-13<br>3 Bob Wilson 22803 2019-@3-16<br>3 Bob Wilson 22883 2019-83-16<br>4 Deanna Washington 22801 2019-83-89<br>4 Deanna Washington 22801 2019-83-89<br>4 Deanna Washington 22801 2019-83-89<br>4 Deanna Washington 228@1 2019-83-89<br>5 Abigail Harris 22801 2019-83-69<br>6 Betty Bullard 22801<br>7 Jessica Armenta 22883 2019-83-89<br>8 Norma Valenzuela 22803 com<br>9 Janet Forbes 22801<br>18 Russell Edwards 22801 2019-83-16<br>a1 Richard Paulson 22801<br>12 Jack Wise 22883 2619-83-89<br>12 Jack Wise 22803 2019-83-69<br>12 Jack Wise 22883 2019-03-16<br><!-- End of picture text -->

|| customer_id|customer_first|_name|customer_last_name|customer_zip|
|---|---|---|---|---|
|1|Jane||Connor|22801|
|2|Manuel||Diaz|22803|
|3<br>|Bob<br>||Wilson<br>|22883<br>|
|4|Deanna||Washington|22801|
|5|Abigail||Harris|22801|
|6|Betty||Bullard|22801|
|7|Jessica||Armenta|22803|
|8|Norma||Valenzuela|22803|
|9|Janet||Forbes|22801|
|16|Russell||Edwards|22801|
|11|Richard||Paulson|22801|
|12|Jack||Wise|22803|
|13|Jeremy||Gruber|22803|
|14|William||Lopes|22801|
|15|Darrell||Messina|22801|





<!-- Start of picture text -->
ul<br>vendor_id INT{11)<br>market_cate DATE<br>Indexes<br>m<br>~<br>© booth _number INTU11) pimneigaate 2<br>= > vendor_name VARCHARI45)<br>» booth_price_level VARCHAR(45) > vendor_pyp2 VARCHARL4S)<br>Shoe peas CR)  vendor_owner_first_name VARCHAR(45)<br>© booth_rype VARCHAR45) ® vendor_owner_last_name VARCHAR(45)<br>Indexes<br><!-- End of picture text -->

|booth_number|booth_type|market_date|vendor_id|vendor_name|vendor_type|
|---|---|---|---|---|---|
|1|Standard|2019-03-02|3|Hernandez Salsa & Veggies|Fresh Variety:<br>Veggies & More|
|1|Standard|2019-83-89|3|Hernandez Salsa & Veggies|Fresh Variety: Veggies & More|
|1|Standard|2019-03-13|3|Hernandez Salsa & Veggies|Fresh Variety:<br>Veggies & More|
|“4|Standard|2019-83-82|1|Chris'sSustainableEggs&Meats|Eggs&Meats|
|2|Standard|2019-83-89|1|<br>Chris's Sustainable Eggs & Meats|<br>Eggs & Meats|
|Z|Standard|2019-@3-13|4|Mountain View Vegetables|Fresh Variety: Veggies & More|
|3|Small|||||
|4|Small|||||
|5|Small|||||
|6|Small|2019-@3-@2|8|Marco's Peppers|Fresh Focused|
|6|Small|2019-83-89|8|Marco's Peppers|Fresh Focused|
|6|Small|2019-03-13|8|Marco's Peppers|Fresh Focused|
|7|Standard|2019-03-82|4|Mountain View Vegetables|Fresh Variety:<br>Veggies & More|
|7|Standard|2019-@3-89|4|Mountain View Vegetables|Fresh Variety: Veggies & More|
|8|Small|2019-03-82|9|Annie's Pies|Prepared Foods|
|8|Small|2019-03-89|9|Annie's Pies|Prepared Foods|
|8|Small|2019-@3-13|1@|Mediterranean Bakery|Prepared Foods|



###### Table LEFT JOINed to a table on the RIGHT 

side of an existing LEFT JOIN 

All rows from the “left table”, only rows from the “middle table” with matching values in the specified fields of the “left table”, and only rows from the “right table” with matching values in the specified fields of the “middle table”. 





<!-- Start of picture text -->
Two Tables LEFT JOINed to a Table<br>All rows from the “left table”, and only rows from each “right table”<br>with matching values in the specified fields of the “left table”.<br>_- =- - - “ --<br>Neagle- cis“7-7<br>er23¢- XN-<br>‘<br>ae N N<br>N <sN<br>nN N<br>Sy<br>Nes<br>Sys<br><N<br>S|<br><!-- End of picture text -->

**Chapter 5** ■ **SQL JOINs 77** 

2. Is it possible to write a query that produces an output identical to the output of the following query, but using a LEFT JOIN instead of a RIGHT JOIN? 

SELECT * FROM customer AS c RIGHT JOIN customer_purchases AS cp ON c.customer_id = cp.customer_id 

3. At the beginning of this chapter, the analytical question “When is each type of fresh fruit or vegetable in season, locally?” was asked, and it was explained that the answer requires data from the product_category table, the product table, and the vendor_inventory table. What type of JOINs do you expect would be needed to combine these three tables in order to be able to answer this question? 

###### **<mark>C H A P T E R</mark>** 

# **6** 

## **Aggregating Results for Analysis** 

SQL starts becoming especially powerful for analysis when you use it to aggregate data. By using the GROUP BY statement, you can specify the level of summarization and then use aggregate functions to summarize values for the records in each group. 

Data analysts can use SQL to build dynamic summary reports that can be automatically updated as the database is updated with new data, by simply triggering a refresh that reruns the query. Dashboards and reports built using software like Tableau and Cognos often rely on SQL queries to get the data they need from the underlying database in an aggregated form that can be used for reporting, which we’ll cover in Chapter 10, “Building Analytical Reports with SQL.” Data scientists can use SQL to summarize data at the level of granularity needed for training a classification model, which we’ll get into in more depth in Chapter 12, “SQL for Machine Learning.” 

But it all starts with basic SQL aggregation. 

#### **GROUP BY Syntax** 

You saw this basic SQL SELECT query syntax in Chapter 2, “The SELECT Statement.” Two sections of this query that we haven’t yet covered, which are both related to aggregation, are the GROUP BY and HAVING clauses: 

SELECT [columns to return] 

**79** 

**80 Chapter 6** ■ **Aggregating Results for Analysis** 

FROM [table] 

WHERE [conditional filter statements] GROUP BY [columns to group on] HAVING [conditional filter statements that are run after grouping] ORDER BY [columns to sort on] 

The GROUP BY keywords are followed by a comma- separated list of column names that indicate how you want to summarize the query results. 

Using what you’ve learned so far without grouping, you might write a query like the following to get a list of the customer IDs of customers who made purchases on each market date: 

SELECT market_date, customer_id FROM farmers_market.customer_purchases ORDER BY market_date, customer_id 

However, this approach would result in one row per item each customer purchased, displaying duplicates in the output, because you’re querying the customer_purchases table with no grouping specified. 

To instead get one row per customer per market date, you can group the results by adding a GROUP BY clause that specifies that you want to summarize the results by the customer_id and market_date fields: 

SELECT market_date, customer_id FROM farmers_market.customer_purchases GROUP BY market_date, customer_id ORDER BY market_date, customer_id 

You can also accomplish the same result by using SELECT DISTINCT to remove duplicates, but here we are using GROUP BY with the intention of adding summary columns to the output. 

#### **Displaying Group Summaries** 

Now that you have grouped the data at the desired level, you can add aggregate functions like SUM and COUNT to return summaries of the customer_purchases data per group. This query uses the COUNT() function to count the rows in the customer_purchases table per market date per customer. The output of this query is shown in Figure 6.1. 

|market_date|customer_id|items_purchased|
|---|---|---|
|2019-03-62|ai|3|
|2019-83-62|2|if|
|2019-03-62|3|i|
|2019-83-62|4|2|
|2019-03-02|16|1|
|2019-83-89|1|4|
|2619-63-69|4|5|
|2019-83-69|5|1|
|2619-03-69|7|1|
|2019-03-69|12|4|



|market_date|customer_id|items_purchased|
|---|---|---|
|2019-03-62|a!|5.76|
|2019-83-62|2|4.68|
|2019-03-62|3|8.40|
|2019-83-62|4|3.48|
|2019-03-62|16|1.66|
|2019-83-69|a||5.20|
|2019-63-69|4|13.20|
|2019-03-69|=|1.08|
|2619-03-69|7|2.80|
|2019-03-69|12|6.96|





<!-- Start of picture text -->
|<br><!-- End of picture text -->

|market_date|customer_id|different_products_purchased|
|---|---|---|
|2019-03-62|1|2|
|| <sup>2019-03-82</sup>|2|i|
|2619-63-62|3|1|
|| <sup>2019-03-62</sup>|4|2|
|2619-63-62|16|1|
|| <sup>2019-03-69</sup>|1|3|
|2619-63-69|4|4|
|| 2019-83-69|=||i|
|2619-63-69|7|1|
|2019-63-69|i?|4|



|market_date|customer_id|items_purchased|different_products_purchased|
|---|---|---|---|
|2019-83-62|1|5.708|2|
|2019-83-62|2|4.68|at|
|2019-03-62|3|6.48|al|
|2019-63-02|4|3.48|2|
|2019-03-62|18|1.60|a|
|2019-83-69|a!|5.28|3|
|2019-03-69|4|13.28|4|
|2019-83-69|5|1.08|a|
|2019-03-69|7|2.08|1|
|2019-03-69|12|6.99|4|



|market_date|customer_id|vendor_id|price|
|---|---|---|---|
|2019-03-82|3|4|16.8000|
|2019-03-16|3|4|11.0008|
|2019-03-16|3|9|18.0008|





<!-- Start of picture text -->
3 2019-83-62 16.8000<br><!-- End of picture text -->



<!-- Start of picture text -->
customer_id vendor_id total_spent<br>3 4 27.8000<br>3 | 15.8080<br><!-- End of picture text -->



<!-- Start of picture text -->
customer_id total_spent<br>1 108.3756<br>z 25.4088<br>3 45.8008<br>4 66.6256<br>5 16.8808<br>cu 15.0008<br>18 8.8888<br>12 95.8008<br><!-- End of picture text -->

|customer_first_name|customer_last_name|customer_id|vendor_name|vendor_id<br>price|
|---|---|---|---|---|
|Bob|Wilson|3|Mountain View Vegetables|4<br>11.0008|
|Bob|Wilson|3|Annie's<br>Pies|9<br>18.2008|



|customer_first_name<br>customer_last_name|customer_id<br>vendor_name<br>vendor_id<br>total_spent|
|---|---|
|Bob<br>Wilson|3<br>Mountain View Vegetables<br>4<br>27.88|
|Bob<br>Wilson|3<br>Annie's Pies<br>9<br>18.00|



|customer_first_name|customer_last_name|customer_id|vendor_name|vendor_id|total_spent|
|---|---|---|---|---|---|
|Jane|Connor|a ||Annie's Pies|9|18.00|
|Bob|Wilson|3|Annie's Pies|9|18.08|
|Abigail|Harris|5|Annie's Pies|9|16.00|
|Jack|Wise|12|Annie's Pies|9|72.08|



|market_date|quantity|vendor_id|product_id|original_price|
|---|---|---|---|---|
|2019-83-69|10.88|9|5|5.68|
|2019-83-38|17.68|7|13|6.08|
|2019-93-23|5.88|7|13|6.88|
|2019-83-02|13.00|1|1e|6.08|
|2019-83-69|17.80|1|1¢e|6.88|
|2019-83-09|8.08|7|13|6.68|
|2019-83-20|13.80|r J|13|6.88|
|2019-03-62|28.08|1|11|12.06|
|2019-83-89|18.88|a|il|12.80|
|2019-03-20|15.00|at|abs|13.06|





<!-- Start of picture text -->
minimum_price maximum_price<br>/2.00 15.08<br><!-- End of picture text -->

|product_category_name|product_category_id|minimum_price|maximum_price|
|---|---|---|---|
|Fresh Fruits & Vegetables|1|2.08|6.80|
|Packaged Prepared Food|3|4.00|15.08|
|Eggs & Meat<br>(Fresh or Frozen)|6|6.08|13.88|





<!-- Start of picture text -->
market_date product_count<br>2019-03-62 4<br>2019-03-69 9<br>2019-93-13 2<br>2619-03-16 3<br>2019-03-28 3<br>2019-03-23 2<br>2019-03-38 2<br><!-- End of picture text -->



<!-- Start of picture text -->
vendor_id different_products_offered<br>12<br>41<br>72<br>81<br>9 |<br><!-- End of picture text -->

|vendor_id|different_products_offered|average_product_price|
|---|---|---|
|1|2|9.888000|
|4|i|2.088088|
|7|2|4.580808|
|8|i|4,000800|
|9|3|14.758808|



|vendor_id|different_products_offered|value_of_inventory|inventory_item_count|average_item_price|
|---|---|---|---|---|
|1|2|636.0000|68.00|9.35|
|4|1|258.0008|129.88|2.08|
|7|2|185.2000|27.08|3.89|
|8|1|408.0000|100.08|4.00|
|9|3|418.2000|38.08|13.67|



|vendor_id|different_products_offered|value_of_inventory|inventory_item_count|average_item_price|
|---|---|---|---|---|
|4|1|258.8008|129.00|2 .88808000|
|8|z|400.2000|108.88|4.08800000|



|2019-83-02|8|1¢e|a|1.00|Banana Peppers<br>- Jar|8 oz|unit|
|---|---|---|---|---|---|---|---|
|2019-83-89|8|12|4|1.08|Banana Peppers<br>- Jar|8 oz|unit|
|2019-83-13|8|2|4|2.08|Banana Peppers<br>- Jar|8 oz|unit|
|2019-@3-16|8|1e@|=|1.08|Banana Peppers<br>- Jar|8 oz|unit|
|2019-83-62|4|2|9|4.68|Sweet Potatoes|medium|lbs|
|2019-03-02<br>|4<br>|3<br>|9<br>|8.48<br>|Sweet Potatoes<br>|medium<br>|lbs<br>|
|2019-@3-@2<br>|4<br>|4<br>|9<br>|1.48<br>|Sweet Potatoes<br>|medium<br>|lbs<br>|
|2019-03-89|4|4|9|9.98|Sweet Potatoes|medium|lbs|
|2019-03-13|4|2|9|4.10|Sweet Potatoes|medium|lbs|
|2019-@3-16|4|3|9|5.50|Sweet Potatoes|medium|lbs|
|2019-03-62<br>|Zz<br>|a |<br>|10<br>|1.08<br>|Eggs<br>|1 dozen<br>|unit<br>|
|2019-03-02|1|1|1e|3.08|Eges|1 dozen|unit|
|2019-83-89|1|1|1e|2.08|Eggs|1 dozen|unit|
|2019-83-09|1|4|18|1.08|Eggs|1 dozen|unit|
|2019-83-02|1|1|11|1.78|Pork Chops|1 1b|lbs|
|2019-83-89|1|12|11|8.98|Pork Chops|1 1b|lbs|



|market_date|vendor_id|customer_id|produc|t_id<br>quantity_units|quantity_lbs|quantity_other|product_qty_type|
|---|---|---|---|---|---|---|---|
|2019-@3-62|8|a|4|2.08|8|@|unit|
|2019-83-82|8|18|4|1.08|e|@|unit|
|2019-83-89|8|12|4|1.08|e|@|unit|
|2019-03-13|8|2|4|2.08|e|e|unit|
|2019-03-16|8|16|4|1.00|e|@|unit|
|2019-@3-62|4|2|9|e|4.68|@|lbs|
|2019-03-82|4|3|9|@|8.48|e|lbs|
|2019-83-02|4|4|9|e|1.48|@|lbs|
|2019-83-89|4|4|9|e|9.98|@|lbs|
|2019-03-13|4|2|9|e|4.18|e|lbs|
|2019-83-16|4|a|9|e|5.58|@|lbs|
|2019-@3-02|1|1|18|1.08|@|@|unit|
|2019-83-02|a §|1|18|3.00|e|@|unit|
|2019-83-89|Z|at|10|2.08|@|@|unit|
|2019-83-89|Z|4|18|1.00|e|@|unit|
|2019-03-62|1|1|att|e|1.78|e|lbs|
|2019-83-09|ui|12|an|e|8.98|e|lbs|



|market_date|custome|r_id<br>qty_units_purchased|aqty_lbs_purchased|qty_other_purchased|
|---|---|---|---|---|
||2@19-@3-@2|1|4.08|1.78|8.08|
|2019-83-82|2|@.00|4.68|@.08|
|2019-83-82|3|@.80|8.48|@.80|
|2019-83-82|4|2.08|1.48|@.08|
|2019-83-82|1@|1.00|8.08|8.08|
|2019-83-89|1|2.08|2.28|@.00|
|2019-@3-89|4|3.00|18.28|6.08|
|2019-83-89|7|2.00|8.08|@.08|
|2019-83-89|12|3.08|6.98|8.08|
|2019-83-13|2|2.08|4.18|2.00|
|2019-83-16|3|@.80|5.58|8.08|
|2019-83-16|1¢@|1.00|8.08|@.08|
|2019-83-20|1|@.00|3.10|@.80|
|2019-83-28|7|3.08|2.08|@.08|
|2019-@3-23|=|3.00|2.48|8.08|



**<mark>C H A P T E R</mark> 7** 

## **Window Functions and Subqueries** 

All of the functions that have been covered in this book so far, like ROUND(), return one value in each row of the results dataset. When GROUP BY is used, the functions operate on multiple values in an aggregated group of records, summarizing across multiple rows in the underlying dataset, like AVG(), but each value returned is associated with a single row in the results. 

_Window functions_ operate across multiple records, as well, but those records don’t have to be grouped in the output. This gives the ability to put the values from one row of data into context compared to a group of rows, or partition, enabling an analyst to write queries that answer questions like: If the dataset were sorted, where would this row land in the results? How does a value in this row compare to a value in the prior row? How does a value in the current row compare to the average value for its group? 

So, window functions return group aggregate calculations alongside individual row- level information for items in that group, or partition. They can also be used to rank or sort values within each partition. 

One use for window functions in data science is to include some information from a past record alongside the most recent detail record related to an entity. For example, we could use window functions to get the date of the first purchase a person made at the farmer’s market, to be returned alongside their detailed purchase records, which could then be used to determine how long they had been a customer at the time each purchase was made. 

**97** 

**98 Chapter 7** ■ **Window Functions and Subqueries** 

#### **ROW NUMBER** 

Based on what you’ve learned in previous chapters, if you wanted to determine how much the most expensive product sold by each vendor costs, you could group the records in the vendor_inventory table by vendor_id, and return the maximum original_price value using the following query: 

SELECT vendor_id, MAX(original_price) AS highest_price FROM farmers_market.vendor_inventory GROUP BY vendor_id ORDER BY vendor_id 

But this just gives you the price of the most expensive item per vendor. If you wanted to know which item was the most expensive, how would you determine which product_id was associated with that MAX(original_price) per vendor? 

There is a window function that enables you to rank rows by a value— in this case, ranking products per vendor by price— called ROW_NUMBER(). This approach will allow you to maintain the detail- level information that you would otherwise lose by aggregating like we did in the preceding query: 

SELECT vendor_id, market_date, product_id, original_price, 

ROW_NUMBER() OVER (PARTITION BY vendor_id ORDER BY original_price DESC) AS price_rank 

FROM farmers_market.vendor_inventoryORDER BY vendor_id, original_price DESC 

Let’s break that syntax down a bit. I would interpret the ROW_NUMBER() line as “number the rows of inventory per vendor, sorted by original price, in descending order.” The part inside the parentheses says how to apply the ROW_NUMBER() function. We’re going to PARTITION BY vendor_id (you can think of this like a GROUP BY without actually combining the rows, so we’re telling it how to split the rows into groups, without aggregating). Then within the partition, the ORDER BY indicates how to sort the rows. So, we’ll sort the rows by price, high to low, within each vendor_id partition, and number each row. That means the highestpriced item per vendor will be first, and assigned row number 1. 

You can see in Figure 7.1 that for each vendor, the products are sorted by original_price, high to low, and the row numbering column is called price_ rank. The row numbering starts over when you get to the next vendor_id, so the most expensive item per vendor has a price_rank of 1. 

|vendor_id|market_date|product_id|original_price|price_rank|
|---|---|---|---|---|
|j1|2019-03-02|11|12.00|2|
|}1|2019-63-09|11|12.00|3|
|j1|2019-03-02|14|6.80|4|
|}1|2019-63-09|16|6.08|5|
|4|2019-03-16|9|2.80|4|
||4|2019-63-02|9|2.00|1|
|4<br>|2019-83-09<br>|9<br>|2.00<br>|2<br>|
|4|2019-93-13|9|2.00|3|
|7|2019-83-89|13|6.00|1|
|r|2019-83-26|13|6.80|2|
||7|2019-83-23|13|6.60|3|
|| <sup>F |</sup>|2019-83-38|i3|6.80|4|
|<br>7<br>|2019-83-20<br>|12<br>|3.68<br>|6<br>|
||7|2619-63-23|a2|3.80|Z|
|r|2019-83-30|12|3.68|8|
|i|2019-83-69|12|3.80|5|



|vendor_id|market_date|product_id|original_price|price_rank|
|---|---|---|---|---|
|2|2019-43-26|11|13.00|1|
||4|2@19-@3-@2|9|2.00|1|
||7|2019-83-89|13|6.060|1|
||8|2019-03-02|4|4.88|1|
|9|2019-83-89|7|18.66|1|





<!-- Start of picture text -->
1° SELECT * FROM " "<br>outer" query<br>2—-<br>3 FSS' SELECTaaaWe " er '|<br>4 H Inner query :<br>5S !1H1 vi.vendor_id,vi.market_date,vi.product_id, 11<br>7 ' vi.original_price,re “ae " '1<br>8 1 ROW_NUMBER() OVER (PARTITION BY vendor_id ORDER BY original_price DESC) AS price_rank |<br>- - 4<br>9 FROM farmers_market.vendor_inventory vi !<br>1@ |PaORDER BY vi.vendor_ida rrrren| 1H|<br>il ) x " t "<br>12 WHERE x.price rank = 1 outer query<br><!-- End of picture text -->

**Chapter 7** ■ **Window Functions and Subqueries 101** 

If we didn’t use a subquery, and had attempted to filter based on the values in the price_rank field by adding a WHERE clause to the first query with the ROW_ NUMBER function, we would get an error. The price_rank value is unknown at the time the WHERE clause conditions are evaluated per row, because the window functions have not yet had a chance to check the entire dataset to determine the ranking. If we tried to put the ROW_NUMBER function in the WHERE clause, instead of referencing the price_rank alias, we would get a different error, but for the same reason. 

You will see the subquery format throughout this chapter, because if you want to do anything with the results of most window functions, you have to allow them to calculate across the entire dataset first. Then, by treating the results like a table, you can query from and filter by the results returned by the window functions. 

Note that you can also use ROW_NUMBER without a PARTITION BY clause, to number every record across the whole result (instead of numbering per partition). If you were to use the same ORDER BY clause we did earlier, and eliminate the PARTITION BY clause, then only one item with the highest price in the entire results set would get the price_rank of 1, instead of one item per vendor. 

#### **RANK and DENSE RANK** 

Two other window functions are very similar to ROW_NUMBER and have the same syntax, but provide slightly different results. 

The RANK function numbers the results just like ROW_NUMBER does, but gives rows with the same value the same ranking. If we run the same query as before, but replace ROW_NUMBER with RANK, we get the output shown in Figure 7.4. 

SELECT vendor_id, market_date, product_id, original_price, RANK() OVER (PARTITION BY vendor_id ORDER BY original_price DESC) AS price_rank FROM farmers_market.vendor_inventory ORDER BY vendor_id, original_price DESC 

If we used subquery structure and embedded this query inside another SELECT statement like we did previously, and filtered to price_rank = 1, multiple rows per vendor would be returned. 

Notice in Figure 7.4 that the ranking for vendor_id 1 goes from 1 to 2 to 4, skipping 3. That’s because there’s a tie for second place, so there’s no third place. If you don’t want to skip numbers like this in your ranking when there is a tie 

|vendor_id<br>|market_date<br>|product_id<br>|original_price<br>|price_rank<br>|
|---|---|---|---|---|
|1|-2019-@3-2@|11|13.00|1|
|1<br>|2019-03-02<br>|11<br>|12.80<br>|2<br>|
|1|2019-@3-@9|11|12.00|2|
|i|2019-03-62|16|6.68|4|
|1|2019-03-09|16|6.08|4|
|4|2019-03-16|9|2.08|ak|
|4|2019-@3-@2|a|2.08|1|
|4|2019-03-69|9|2.08|1|
|4|2619-63-13|9|2.08|i|
|Z|2019-03-69|13|6.68|a|
|Fi|2019-83-28|13|6.88|i|
|7|2019-03-23|13|6.08|1|
|Z|2019-03-38|13|6.88|i|
|7|2019-03-26|12|3.08|5|
|Fi|2019-93-23|12|3.08|5|
|7|2019-03-38|12|3.08|5|
|7|2019-03-69|12|3.808|5|



**Chapter 7** ■ **Window Functions and Subqueries 103** 

product_id, original_price, NTILE(10) OVER (ORDER BY original_price DESC) AS price_ntile FROM farmers_market.vendor_inventory ORDER BY original_price DESC 

If the number of rows in the results set can be divided evenly, the results will be broken up into _n_ equally sized groups, labeled 1 to _n_ . If they can’t be divided up evenly, some groups will end up with one more row than others. 

Note that the NTILE is only using the count of rows to split the groups (or to split the partition into groups, if you specify a partition), and is not using a field value to determine where to make the splits. Therefore, it’s possible that two rows with the same value specified in the ORDER BY clause (two products with the same original_price, in this case) will end up in two different NTILE groups. 

You can sort on additional fields if you want a little more control over how the rows are split into NTILE groups. But if you want to ensure that all items with the same price are grouped together, for example, then it would make more sense to use RANK than NTILE, because in that case, you aren’t looking for evenly sized groupings. 

#### **Aggregate Window Functions** 

You learned about aggregate SQL functions like SUM() in Chapter 6, “Aggregating Results for Analysis,” and in this chapter you have learned about window functions that partition the results set. Can you imagine how they might be used together? It turns out that you can use most aggregate functions across partitions like the window functions, returning an aggregate calculation for a partition on every row in that partition (or, for the whole results set, if you don’t use the PARTITION BY clause). One way this approach can be used is to compare each row’s value to the aggregate value for that grouped category. 

For example, what if you are a farmer selling products at the market, and you want to know which of your products were above the average price per product on each market date? (Remember that because of the way our database is designed, this isn’t a true average for the full inventory, because we’re not multiplying by a quantity, but you can think of it as the average display price in a product catalog.) We can use the AVG() function as a window function, partitioned by market_date, and compare each product’s price to that value. First, let’s try using AVG() as a window function. The output of the following query is shown in Figure 7.5: 

SELECT vendor_id, market_date, 

_Continues_ 

|vendor_id<br>|market_date<br>|product_id<br>|original_price<br>|average_cost_product_by_market_date<br>|
|---|---|---|---|---|
|I|2019-@3-@2|4|4.08|6.988080|
|4|2019-83-82|9|2.08|6.980000|
|1|2019-83-02|18|6.08|6.900080|
|1|2019-03-82|11|12.00|6.980000|
|8|2019-83-89|=|4.08|8.222222|
|9|2019-03-89|5|5.08|8.222222|
||9|2019-83-89|7|18.00|8.222222|
||9|2019-83-89|8|18.00|8.222222|
|4|2019-83-89|9|2.08|8.222222|
|z|2019-83-89|18|6.88|8.222222|
|1|2019-83-89|11|12.08|8.222222|
|7|2019-03-89|12|3.08|8.222222|
|7|2019-83-89|13|6.08|8.222222|
|8|2019-03-13|7|4.08|3.888080|
|4|2019-83-13|9|2.00|3.808080|



|vendor_id|market_date|product_id|original_price|average_cost_product_by_market_date|
|---|---|---|---|---|
|ES|2019-83-82|ate I|12.08|6.08|
|1|2019-83-89|sal|12.00|8.22|
|1|2019-83-28|11|13.08|7.33|



|[vendor_id|marketdate|productid|originel_price|_vendor_product_count_per_narket_aete||
|---|---|---|---|---|
|<br>1|<br>2019-83-62|<br>11|<br>12.00|<br>2|
|1|2019-83-82|18|6.808|2|
|1|2019-83-89|11|12.00|2|
|1|2019-83-89|18|6.80|2|
|1|2019-83-28|11|13.00|1|
|4|2019-83-82|9|2.08|i|
|4|2019-83-89|9|2.00|1|
|4|2019-83-13|9|2.08|1|
|4|2019-83-16|9|2.08|1|





<!-- Start of picture text -->
[vendor_id market date product id originel_price _vendor_product_count_per_narket_aete<br>1 2019-83-62 11 12.00 2<br>1 2019-83-82 18 6.808 2<br>1 2019-83-89 11 12.00 2<br>1 2019-83-89 18 6.80 2<br>1 2019-83-28 11 13.00 1<br>4 2019-83-82 9 2.08 i<br>4 2019-83-89 9 2.00 1<br>4 2019-83-13 9 2.08 1<br>4 2019-83-16 9 2.08 1<br><!-- End of picture text -->

|customer_id|market_date|vendor_id|product_id|price|running_total_purchases|
|---|---|---|---|---|---|
||10|2019-@3-@2|8|>|4.0008|29.9088|
|\1|2019-83-82|1|18|15.8000|44.9880|
||4|2019-@3-@2|8|=|8.20028|52.9088|
||4|2019-83-02|4|9|2.8008|55.7808|
||2|2019-03-02|4|9|9.2008|64.9808|
||3|2019-03-82|4|9|16.8800|81.7000|
|es|2019-83-89|9|8|18.9008|99.7080|
|j1|2019-83-89|1|18|11.9800|11@.7008|
|)1|2019-@3-@9|||13|12.6560|123.3508|
|j2|2019-83-89|7|13||123.3500|
||4|2019-@3-@9|7|13|1.7258|125.8758|
||4|2019-03-89|7|13||125.0758|
|5|2019-@3-@9|9|7|16.0008|141.8758|
|7|2019-83-69|7|12|6.0088|147.6758|



|\1|2019-03-69|9|8|18.8000|58.9000|
|---|---|---|---|---|---|
|\1|2019-@3-@9|1|18|11.0080|69.9080|
|)2|2019-03-69|7|13|12.6580|82.5500|
|1|2019-@3-@9|7|13||82.5580|
|\1|2019-03-20|7|13|17.8258|108.3758|
||2|2019-03-02|=|9|9.2088|9.2088|
||2|2019-@3-13|4|9|8.2000|17.4080|
|2|2019-@3-13|8|=|8.0008|25.4000|
|3|2019-@3-@2|4|9|16.8080|16.8080|
|3|2019-@3-16|9|8|18.0000|34.8080|
|| 3|2019-83-16|=|9|11.0000|45.8000|



|customer_id<br><br>|market_date<br>|vendor_id<br><br>|product_id<br><br>|price<br>|customer_spend_total<br>|
|---|---|---|---|---|---|
|fa<br>|"2019-03-89.|9<br>|rr<br>|“18.0000|100.3750|
|1|2019-03-02|1|16|5.5000|100.3750|
|1|2019-63-02|1|18|15.6@06|100.3758|
|1|2019-03-09|1|16|11.6088|100.3758|
|1|2019-@3-02|i|11|20.4000|108.3758|
|1<br>|2019-63-09<br>|Fi<br>|13<br><br>|12.6580<br>|100.3750<br>|
|ja|2@19-@3-@9|7|13<br>|coms|100.3750|
|1|2019-63-20|Zz|13|17.8250|106.3750|
|| <sup>2</sup>|2019-@3-13|8|4|8.9888|25.4808|
|2|2019-63-62|4|9|9.2006|25.4600|
|2|2019-03-13|4|9|8.20808|25.4808|
|3|2019-63-16|9|8|18.6080|45.3000|
|| <sup>3</sup>|2019-03-02|4|9|16.5000|45.6000|
|3|2019-63-16|4|9|11.6066|45.8000|



|market_date|vendor_id|booth_number|previous_booth_number|
|---|---|---|---|
|2019-64-83|3|a1|ones|
|2019-84-03|4|7||
|2019-84-83|7|11||
|2019-84-03|8|6||
|2019-04-83|9|8||
|2019-04-06|1|2|2|
|2019-84-06|3|1|1|
|2019-84-06|4|7|7|
|2019-84-06|7|11|11|
|2019-84-06|8|6|6|
|2019-84-06|9|8|8|
|2019-84-10|1|7|2|
|2019-84-18|3|1|1|
|2019-84-10|4|2|7|
|2019-84-10|7|11|11|
|2019-84-18|8|6|6|
|2019-84-18|9|8|8|



2619-64-18 4 

2 7 

|2019-03-62|61.7608|
|---|---|
|2019-03-09|171.4756|
|2619-63-13|16.2600|
||2@19-@3-16|51.0000|
|<br>2019-03-20|26.8258|
||2819-@3-23|22.8000|
|<br>2019-63-30|3.60080|



|market_date|market_date_total_sales|previous_market_date_total_sales|
|---|---|---|
|2019-03-82|81.7800|or|
|2019-@3-@9|171.4758|81.7000|
|2019-03-13|16.2008|171.4758|
|2619-63-16|51.8080|16.2000|
|2619-03-28|26.8258|51.8888|
|2019-63-23|22.5080|26.8250|
|2619-83-38|3.8888|22.8800|



**112 Chapter 7** ■ **Window Functions and Subqueries** 

   - b. Reverse the numbering of the query from a part so each customer’s most recent visit is labeled 1, then write another query that uses this one as a subquery and filters the results to only the customer’s most recent visit. 

2. Using a COUNT() window function, include a value along with each row of the customer_purchases table that indicates how many different times that customer has purchased that product_id. 

3. In the last query associated with Figure 7.14 from the chapter, we used LAG and sorted by market_date. Can you think of a way to use LEAD in place of LAG, but get the exact same output? 

###### **<mark>C H A P T E R</mark>** 

# **8** 

## **Date and Time Functions** 

Data scientists use date and time functions many different ways in our queries. We may use two dates to calculate a duration, for example. Many machine learning algorithms are “trained” to identify patterns in data from the past and use those patterns to predict future outcomes. In order to build a dataset for that purpose, we have to be able to filter queries by time range. 

Often, datasets that are built for predictive models include summaries of activities within dynamic date ranges— for example, a count of some activity occurrence during each of the past three months. Or, in the case of time- series analysis, an input dataset might include one row per time period (hour, day, week, month) with a count of something associated with each time period; for example, the number of patients a doctor sees per week. 

Many predictive models are time- bound. For example, the question “Will this first- time customer become a repeat customer?” will be further refined as “What is the likelihood that each first- time customer at today’s farmer’s market will return and make a second purchase within the next month?” To answer this question, we could create a dataset with a row for every customer, columns containing data values as of the time of their first purchase, and a binary “target variable” that indicates whether that customer made another purchase within a month of their first purchase date. 

Let’s look at some different ways to work with date and time values in our Farmer’s Market database. 

**113** 

|market_date<br>||market_start_time|market_end_time|market_start_datetime|market_end_datetime|
|---|---|---|---|---|
|2019-@3-02|8:68 AM|2:08 PM|2019-@3-@2 08:00:60|2019-@3-@2<br>14:00:00|
|2019-83-89|9:08 AM|2:06 PM|2019-83-89 09:00:00|2019-83-89 14:00:00|
|2019-@3-13|4:08 PM|7:06<br>PM|2019-@3-13<br>16:00:80|2019-@3-13<br>19:00:00|
|2019-63-16|8:00 AM|2:00 PM|2019-83-16 08:00:00|2019-83-16 14:00:00|
|2019-83-28|4:88 PM|7:08 PM|2019-@3-28@ 16:00:80|2019-@3-28@ 19:00:80|
|2019-83-23|8:08 AM|2:68 PM|2019-83-23 08:00:00|2019-83-23 14:00:08|
|2019-@3-27|4:08 PM|7:08 PM|2019-@3-27 16:00:00|2019-@3-27 19:00:80|
|2019-83-38|8:68 AM|2:60 PM|2019-83-38 08:00:00|2019-83-38 14:00:00|



**Chapter 8** ■ **Date and Time Functions 115** 

**~~NOTE~~ You can find the SQL date and time function documentation for any database system by searching the internet for “[database system] date and time functions.” For MySQL 8.0, you can find this documentation at** dev.mysql.com/doc/refman/ 8.0/en/date- and- time- functions.html **.** 

The combination of functions in the query associated with Figure 8.1 is taking each date and time string, concatenating them into a combined datetime string, and converting that to a datetime data type. So, the final market_start_datetime and market_end_datetime fields are actually stored as datetime values, which we can then use to perform calculations, like finding the difference between two datetimes. The STR_TO_DATE() function does the type conversion to a date, time, or datetime, depending on the input. It will return a NULL value if the input string isn’t formatted in a way it can interpret. 

You’ll notice that the dates in the final two columns in Figure 8.1 are formatted as YYYY- MM- DD, and the times are in 24- hour time (HH:MM:SS), which is one indication that the fields are datetimes (though I should note it would also be possible to format a string to look like a datetime using the DATE_FORMAT() function and a particular formatting string). 

#### **EXTRACT and DATE_PART** 

You will encounter datetime data types, such as timestamps, in the databases you work with and might only need a portion of the stored date and time value. For example, you might only want the month and day from a full date, in one field, with the year stripped out into a second field, to create a year- over- year comparison (to align and visualize daily totals from different years by month and day). 

Depending on the database system you are using, the function that retrieves different portions of a datetime value may be called EXTRACT (MySQL), DATE_ PART (Redshift), or DATEPART (Oracle and SQL Server). The example Farmer’s Market database is in MySQL, so these examples use EXTRACT(), but the concepts are the same for the other functions, even though the syntax will vary. The market_start_datetime field in Figure 8.2 is an example of a MySQL datetime type field. 

In addition to EXTRACT(), MySQL offers the functions DATE() and TIME() to extract the date and time parts of a datetime field, respectively (you put the datetime value inside the parentheses, and just the date or time portion is returned). 

Using datetime values established in the datetime_demo table created in the previous section, we can EXTRACT date and time parts from the fields. 

The following query demonstrates five different “date parts” that can be extracted from the datetime and results in the output shown in Figure 8.2. Using 



|market_start_datetime|mktsrt_date|mktsrt_time|
|---|---|---|
|2019-03-62 68:06:06|2019-63-02|68:66:68|



market_start_datetime mktstrt_date_plus_3@min 2019-63-02 98:00:00 2019-83-82 08:34:08 

market_start_datetime mktstrt_date_plus_3@days 2019-83-82 08:06:08 2019-84-61 98:06:08 

market_start_datetime mktstrt_date_plus_neg3@days mktstrt_date_minus_3@days 2019-@3-@2 98:00:00 2019-01-31 98:00:00 2019-81-31 98:90:00 



<!-- Start of picture text -->
first_market last_market days_first_to_last<br>2019-83-62 68:60:88 2019-93-36 68:00:06 28<br><!-- End of picture text -->

|market_start_datetime|market_end_datetime|market_duration_hours|market_duration_mins|
|---|---|---|---|
|2019-@3-@2 08:00:80|2019-@3-@2<br>14:00:00|6|368|
|2019-@3-@9 89:00:80|2019-@3-@9 14:00:08|5|308|
|2019-83-13<br>16:00:00|2019-83-13<br>19:00:00|3|188|
|2019-83-16 08:00:00|2019-83-16 14:00:00|6|368|
|2019-03-28 16:00:00|2019-@3-2@ 19:00:00|3|188|
|2019-03-23 08:00:00|2019-03-23 14:00:00|6|368|
|2019-@3-27<br>16:00:80|2019-83-27<br>19:00:06|3|188|
|2019-83-30 08:00:00|2019-83-30 14:00:00|6|368|





<!-- Start of picture text -->
Pe<br><!-- End of picture text -->

|customer_id|market_date|
|---|---|
|1|2019-83-09|
|1|2019-03-62|
|1|2019-83-02|
|1|2019-83-69|
|1|2019-83-02|
|nt|2619-03-69|
|1|2019-83-89|
|1|2019-03-20|



|customer_id<br>#irst_purchase|last_purchase|count_of_purchase_dates|
|---|---|---|
|1<br>2019-83-82|2019-83-28|3|



|customer_id|first_purchase|last_purchase|count_of_purchase_dates|days_between_first_last_purchase|
|---|---|---|---|---|
|la|2019-03-82|2019-83-28|3|18|
|2|2019-83-62|2019-83-13|2|11|
|3|2019-@3-@2|2019-03-16|2|14|
|4|2019-63-62|2019-83-23|3|21|
|5|2019-03-89|2019-83-89|a|@|
|7|2819-@3-@9|2019-83-20|2|11|
|1é|2019-@3-@2|2019-03-16|2|14|
|12|2019-83-69|2019-@3-3@|3|21|



|customer_id|market_date|purchase_number|next_purchase|
|---|---|---|---|
|la|2019-03-@2|1|2019-03-02|
|1|2019-83-62|1|2019-83-62|
|1|2019-03-02|1|2019-03-09|
|1|2019-93-89|4|2019-83-09|
|1|2019-93-99|4|2019-83-09|
|1|2019-83-09|4|2019-03-09|
|1|2019-83-99|4|2019-83-28|
|1|2019-93-20|8||



|customer_id|market_date|purchase_number|next_purchase|days_between_purchases|
|---|---|---|---|---|
|1|2019-83-82|1|2019-93-09|7|
|1|2019-03-09|2|2019-03-20|11|
|1|2019-93-28|3|||



|customer_id<br>|first_purchase<br>|second_purchase<br>|time_between_1st_2nd_purchase<br>|
|---|---|---|---|
|fa|2019-93-02|2@19-@3-@9|7|
|2|2019-03-02|2@19-@3-13|cf|
|3|2019-93-02|2019-83-16|14|
|4<br>|2019-93-02<br>|2019-93-99<br>|7<br>|
|5<br>|2019-03-09<br>|ee<br>|LEE<br>|
|7]|2019-93-09|2019-03-20|11|
|18|2019-93-02|2@19-@3-16|14|
|12|2019-93-09|2019-03-16|7|



customer_id market_count 



<!-- Start of picture text -->
5 a<br><!-- End of picture text -->

**126 Chapter 8** ■ **Date and Time Functions** 

#### **Exercises** 

1. Get the customer_id, month, and year (in separate columns) of every purchase in the farmers_market.customer_purchases table. 

2. Write a query that filters to purchases made in the past two weeks, returns the earliest market_date in that range as a field called sales_since_date, and a sum of the sales (quantity * cost_to_customer_per_qty) during that date range. 

   - Your final answer should use the CURDATE() function, but if you want 

   - to test it out on the Farmer’s Market database, you can replace your CURDATE() with the value ‘2019- 03- 31’ to get the report for the two weeks prior to March 31, 2019 (otherwise your query will not return any data, because none of the dates in the database will have occurred within two weeks of you writing the query). 

3. In MySQL, there is a DAYNAME() function that returns the full name of the day of the week on which a date occurs. Query the Farmer’s Market database market_date_info table, return the market_date, the market_day, and your calculated day of the week name that each market_date occurred on. Create a calculated column using a CASE statement that indicates whether the recorded day in the database differs from your calculated day of the week. This is an example of a quality control query that could be used to check manually entered data for correctness. 

# **<mark>C H A P T E R</mark> 9** 

## **Exploratory Data Analysis with SQL** 

Exploratory Data Analysis (EDA) is often discussed in a data science context as a first step in the predictive modeling process, when a data scientist explores what the data in a provided dataset looks like prior to using it to build a predictive model. The SQL we’ll be using in this chapter could be used at that point in the process, to explore an already- prepared dataset. But what if you don’t have a dataset to work with yet? 

Here we’ll show examples that could occur even earlier in the data pipeline, as we explore raw data straight from the database tables (as opposed to an already- aggregated dataset in which the raw data has been combined and transformed using SQL that is ready to be ingested into a model). If you are given access to a database for the first time, these are the types of queries you can run to familiarize yourself with the tables and data in it. 

There are of course many ways to conduct EDA, including in a Jupyter notebook with Python code, in a Tableau workbook, or using SQL. (I regularly do all three in my job as a data scientist.) In the later EDA, once a dataset has been prepared, the focus is often on distributions of values, relationships between columns, and identifying correlations between input features and the target variable (column with values to be predicted by the model). Here, we will use the types of queries we’ve covered so far in this book to explore some tables in the Farmer’s Market database, as a demonstration of a real EDA focusing on familiarizing ourselves with the data in the database for the first time. 

**127** 

**128 Chapter 9** ■ **Exploratory Data Analysis with SQL** 

#### **Demonstrating Exploratory Data Analysis with SQL** 

Let’s start with a real- world scenario for this example Exploratory Data Analysis: Let’s say the Director of the Farmer’s Market asks us to help them build some reports to use throughout the year, and gives us access to the database referenced in this book. They haven’t yet given us any specific report requirements, but they have told us that they’ll be asking questions related to general product availability and purchase trends, and have given us the E- R diagram found in Chapter 1, “Data Sources,” so we know the relationships between the tables. 

Based on the little information we have, we might guess that we should familiarize ourselves with the product, vendor_inventory, and customer_ purchases tables, because we’ve been told we’ll be building reports on “product availability” and “purchase trends.” 

Some sensible questions to ask via query are: 

- How large are the tables, and how far back in time does the data go? 

- What kind of information is available about each product and each purchase? 

- What is the granularity of each of these tables; what makes a row unique? 

- Since we’ll be looking at trends over time, what kind of date and time dimensions are available, and how do the different values look when summarized over time? 

- How is the data in each table related to the other tables? How might we join them together to summarize the details for reporting? 

#### **Exploring the Products Table** 

Some databases (like MySQL) offer a function called DESCRIBE [table name] or DESC [table name], or have a special schema to select from to list the columns, data types, and other settings for fields in tables, but this function isn’t available in every database system and doesn’t show a preview of the data, so we’ll take a more universal approach here to preview data in a table. 

Let’s start with the product table first. We’ll select everything in the table, to see what kind of data is in each column, but limit it to 10 rows in case it is a large table: 

SELECT * FROM farmers_market.product LIMIT 10 

The output from this query is shown in Figure 9.1. What do we notice in this output? We can see that there is a product_id, product_name, product_size, 

|product_id|product_name|product_size|product_category_id|product_qty_type|
|---|---|---|---|---|
|||Habanero Peppers<br>- Organic|medium|1|lbs|
|2|Jalapeno Peppers<br>- Organic|small|aE|lbs|
|3|Poblano Peppers<br>- Organic|large|x|unit|
|a|Banana Peppers<br>-<br>Jar|8 oz|3|unit|
|5|Whole Wheat<br>Bread|1.5 lbs|3|unit|
|6|Cut Zinnias Bouquet|medium|5|unit|
|7|Apple Pie|16"|3|unit|
|8|Cherry Pie|16"|3|unit|
|9|Sweet Potatoes|medium|1|lbs|
|1e|Eggs|1 dozen|6|unit|



|product_category_id|product_category_name|
|---|---|
|1|Fresh Fruits & Vegetables|
|2|Packaged Pantry Goods|
|3|Packaged Prepared Food|
|4|Freshly Prepared Food|
|5|Plants &<br>Flowers|
|6|Eggs & Meat<br>(Fresh or Frozen)|
|7|Non-Edible<br>Products|





<!-- Start of picture text -->
count(*)<br>23<br><!-- End of picture text -->

|| product_category_id<br>|product_category_name<br>|count_of_products<br>|
|---|---|---|
|la<br>|Fresh Fruits & Vegetables<br>|13<br>|
||2<br>|Packaged Pantry Goods<br>|1<br>|
||3<br>|Packaged Prepared Food<br>|4<br>|
|4|Freshly Prepared Food|a|
||S<br>|Plants & Flowers<br>|1<br>|
|6|Eggs & Meat (Fresh or Frozen)|2|
||7|Non-Edible Products|2|





<!-- Start of picture text -->
product_qty_type<br>lbs<br>unit<br>HULL<br><!-- End of picture text -->

|market_date|quantity|vendor_id|product_id|original_price|
|---|---|---|---|---|
|2019-07-83|7.38|7|a|6.99|
|2019-87-86|16.96|i|1|6.99|
|2019-87-16|13.08|7|af|6.99|
|2019-67-13|18.22|Fi|1|6.99|
|2019-07-17|16.59|7|a|6.99|
|2019-87-28|9.04|7|1|6.99|
|2019-67-24|16.66|7|1|6.99|
|2019-67-27|6.76|7|i|6.99|
|2019-67-31|11.23|7|1|6.99|
|2019-88-03|10.72|7|a ||6.99|





<!-- Start of picture text -->
? market_date DATE<br>© quantity DECIMAL (16,2)<br>vendor_id INT(11)<br>product_id INT(11)<br>© original_price DECIMAL(16, 2)<br>PRIMARY<br>#k_vendor_inventory_vendorimidx<br>fk_vendor_inventory_product1_idx<br><!-- End of picture text -->



<!-- Start of picture text -->
| min(market_date) max(market_date)<br>2019-04-83 2626-16-18<br><!-- End of picture text -->

|| vendor_id|min(market_date)|max(market_date)|
|---|---|---|
|7|2019-04-83|2620-10-18|
|8|2019-04-03|2020-16-16|
|4|2019-06-61|2020-09-38|



|market_year|market_month|vendors_with_inventory|
|---|---|---|
|2019|4|2|
|2019|=||-|
|2019|6|3|
|2019|7|3|
|2019|8|3|
|2019|9|3|
|2019|16|2|
|2019|11|2|
|2019|12|2|
|2028|>|2|
|2028|a|2|
|2028|5|2|
|2028|6|3|
|2626|ri|3|
|2028|8|3|
|2628|5|3|
|2028|18|2|



||market_date|quantity|vendor_id|product_id|original_price|
|---|---|---|---|---|
|<br>2619-65-15|36.88|7|4|4,08|
|2019-05-18|38.88|hy|4|4.08|
|2619-65-22|48.60|7|~|4,08|
|2019-95-25|38.08|7|4|4.08|
|2619-65-29|48.00|r,|-|4.60|
|2019-06-81|3@.08|un|4|4.08|
|2619-66-85|46.68|ry|-|4.60|
|2019-06-88|30.08|7|4|4.08|
|2619-66-12|36.88|7|4|4,08|
|2019-96-15|49.08|a|4|4.08|
|2619-66-19|406.00|7|-|4.80|
|2019-06-22|49.08|4|4|4.08|
|2019-86-26|40.00|7|-|4.80|
|2019-06-29|38.88|7|4|4.08|
|2619-67-83|7.38|7|1|6.99|
|2019-07-83|33.63|is|2|3.49|
|2619-67-83|76.08|7|3|9.58|
|2019-07-83|40.00|7|4|4.00|



||product_id|vendor_id|market_date|customer_id|quantity|cost_to_customer_per_qty|transaction_time|
|---|---|---|---|---|---|---|
|<br>1|rs|2019-07-83|2|2.77|6.99|18:11:00|
|||7|2019-07-83|14|@.99|6.99|17:32:00|
|1|Zz|2019-@7-@3|14|2.18|6.99|18:23:08|
|1|7|2019-07-83|15|1.53|6.99|18:41:08|
|a|Z|2019-@7-@3|16|2.02|6.99|18:18:00|
|1|ni|2019-87-83|17|4.75|6.99|17:27:08|
|1|a|2019-07-86|4|@.27|6.99|12:20:00|
|a|7|2019-07-06|12|3.60|6.99|09:33:08|
|1|7|2019-07-06|14|3.04|6.99|13:85:08|
|1|iz|2019-07-10|3|2.48|6.99|18:40:00|



||product_id|vendor_id|market_date|customer_id|quantity|cost_to_customer_per_qty|transaction_time|
|---|---|---|---|---|---|---|
|<br>4|7|2019-@4-@3|7|5.08|4.08|17:59:00|
|4|7|2019-04-83|4|1.08|4.08|18:09:00|
|4|7|2019-04-83|12|3.08|4.08|18:35:60|
|4|fy|2019-@4-@3|3|1.08|4.08|18:44:80|
|4|7|2019-@4-@3|6|4.08|4.08|18:49:60|
|4|Pi|2019-04-83|5|3.08|4.28|18:54:00|
|4|7|2019-@4-@3|16|2.08|4.08|18:58:00|
|4|y4|2019-04-06|12|5.00|4.08|08:12:00|
|4|<br>7|2019-04-06|12|5.08|4.08|08:41:00|
|4|7|2019-04-06|2|5.08|4.08|09:34:08|
|4|7|2019-04-86|5|1.00|4.08|11:51:00|
|4|7|2019-04-86|16|2.08|4.08|13:08:08|
|4|7|2019-04-86|16|5.00|4.08|13:12:00|
|4|7|2019-04-06|14|2.08|4.08|13:16:00|



||product_id|vendor_id|market_date|customer_id|quantity|cost_to_customer_per_qty|transaction_time|
|---|---|---|---|---|---|---|
|<br>4|Zz|2019-04-83|12|3.08|4.00|18:35:08|
|4|7|2019-04-86|12|5.00|4.08|08:12:08|
|4|Zz|2019-04-86|12|5.08|4.80|08:41:00|



|| market_date|vendor_id|product_id|quantity_sold|total_sales|
|---|---|---|---|---|
|2619-64-83|7|4|19.06|76.6080|
|2019-04-06|7|4|38.88|128.8008|
|2619-04-16|7|-|23.68|92.0086|
|2019-04-13|7|4|38.88|128.8808|
|2019-04-17|7|4|39.68|156.8606|
|2019-04-28|7|4|28.08|88.8880|
|2019-64-24|7|-|27.08|198.9800|
|2019-04-27|7|4|29.08|116.8808|
|2619-65-61|z|.|22.08|88.8880|
|2619-05-64|7|4|25.06|168.8008|
|2019-85-88|7|-|22.68|88.9880|
|2019-65-11|7|4|38.08|128.8008|
|2619-65-15|7|-|35.68|148.6808|
|2619-05-15|7|4|38.08|126.6008|



|| market_date|quantity|vendor_id|product_id|original_price|market_date|vendor_id|product_id|quantity_sold|total_sales|
|---|---|---|---|---|---|---|---|---|---|
|2019-04-83<br>|48.00<br>|7<br>|a<br>|4.08<br>|2019-84-63<br>|7<br>|4<br>|19.00<br>|76.8000<br>|
||2019-e4-03|16.00|8|5|6.58|2019-04-83|8|=||28.08|138.2000|
|2019-84-83<br>|8.08<br>|8<br>|7<br>|18.00<br>|2019-84-83<br>|8<br>|<br>7<br>|8.08<br>|144.0008<br>|
|||||||||||
|2019-04-86<br>|48.08<br>|7<br>|4<br>|4.08<br>|2019-04-86<br>|7<br>|4<br>|38.08<br>|128.2000<br>|
||2019-e4-06<br>|23.00<br>|8<br>|=<br>|6.58<br>|2019-04-86<br>|8<br>|5<br>|28.08<br>|138.0000<br>|
||2019-04-06<br>|8.00<br>|8<br>|7<br>|18.08<br>|2019-04-06<br>|8<br>|4<br>|7.08<br>|126.0000<br>|
||2019-04-06|8.08|8|8|18.08|2019-04-86|8|8|6.08|188.2000|
|| 2019-84-10<br>|38.08<br>|7<br>|oF<br>|4.08<br>|2019-64-18<br>|r 4<br>|4<br><br>|23.08<br>|92.0008<br>|
||2019-e4-10|23.00|8|5|6.58|2019-04-18|8|i<br>||25.00|162.5000|



**140 Chapter 9** ■ **Exploratory Data Analysis with SQL** 

We can also join in additional “lookup” tables to convert the various IDs to human- readable values, pulling in the vendor name and product names. 

Then, we can filter to vendor 7 and product 4 to get the information we were looking for earlier, comparing this vendor’s inventory of this product to the sales made at each market: 

SELECT vi.market_date, vi.vendor_id, v.vendor_name, vi.product_id, p.product_name, vi.quantity AS quantity_available, sales.quantity_sold, vi.original_price, sales.total_sales FROM farmers_market.vendor_inventory AS vi LEFT JOIN ( SELECT market_date, vendor_id, product_id, SUM(quantity) AS quantity_sold, SUM(quantity * cost_to_customer_per_qty) AS total_sales FROM farmers_market.customer_purchases GROUP BY market_date, vendor_id, product_id ) AS sales ON vi.market_date = sales.market_date AND vi.vendor_id = sales.vendor_id AND vi.product_id = sales.product_id LEFT JOIN farmers_market.vendor v ON vi.vendor_id = v.vendor_id LEFT JOIN farmers_market.product p ON vi.product_id = p.product_id WHERE vi.vendor_id = 7 AND vi.product_id = 4 ORDER BY vi.market_date, vi.vendor_id, vi.product_id 

Now we can see in a sample of this query’s output in Figure 9.17 that this vendor is called Marco’s Peppers, and the product we were looking at is jars of Banana Peppers. He brings 30–40 jars each time and sells between 1 and 40 jars per market (which we quickly determined by sorting the output in the SQL editor ascending and descending by the quantity_sold, but we could’ve also done by adding quantity_sold to the ORDER BY clause of the query and scrolling to the top and bottom of the output or surrounding this query with another query that calculated the MIN and MAX quantity_sold). 

|market_date|vendor_id|vendor_|name|product_id|product_name||quantity_available|quantity_|sold<br>original_price|total_sales|
|---|---|---|---|---|---|---|---|---|---|---|
|2019-84-83|7|Marco's|Peppers|4|BananaPeppers<br>|-Jar|40.00|19.08|4.08|76.0000|
|2019-04-06|7|<br>Marco's|<br> Peppers|4|<br><br>Banana Peppers|<br>- Jar|40.00|38.08|4.08|128.0008|
|2019-84-10|7|Marco's|Peppers|4|BananaPeppers<br>|-Jar|30.00|23.08|4.08|92.0000|
|2019-04-13|7|<br>Marco's|<br> Peppers|4|<br><br>Banana Peppers|<br>- Jar|30.00|38.08|4.08|120.0000|
|2019-04-17|7|Marco's|Peppers|4|Banana Peppers<br>|- Jar|40.00|39.08|4.08|156.0000|
|2019-04-20|7|Marco's|Peppers|4|Banana Peppers|- Jar|40.00|20.08|4.00|80.0000|
|2019-04-24|7|Marco's|Peppers|4|Banana Peppers<br>|- Jar|40.00|27.08|4.08|108.0000|
|2019-04-27<br>|7<br>|Marco's <br>|Peppers<br>|4<br>|Banana Peppers <br><br>|- Jar<br>|30.00<br>|29.08<br>|4.00<br>|116.0000<br>|
|2019-@5-@1<br>|7<br>|Marco's <br>|Peppers<br>|4<br>|Banana Peppers<br><br><br>|- Jar<br>|40.00<br>|22.08<br>|4.08<br>|88.0000<br>|
|2019-05-04<br>|7<br>|Marco's <br>|Peppers<br>|4<br>|Banana Peppers<br><br><br>|- Jar<br>|30.00<br>|25.08<br>|4.08<br>|108.0000<br>|
|2019-@5-08<br>|7<br>|Marco's <br>|Peppers<br>|4<br>|Banana Peppers<br><br>|Jar<br>|40.00<br>|22.00<br>|4.08<br>|88.0000<br>|
|2019-@5-11|7|Marco's|Peppers|4|Banana Peppers|- Jar|40.00|30.08|4.08|12@.000e|





<!-- Start of picture text -->
,<br>Marco's Peppers Inventory vs Sold<br>Market Date<br>2020<br>June July<br>Product Name | Wed3 | Sat6 | Wed10 | Sat13 | Wed17 | Sat20 | Wed24 | Sat27 | Wed1 | Sat4 | Wed8 | Sat11 | Wed15 | Sat18 | Wed22 | Sat25<br>ow7 5¢& 5€.s&a 7 7< 5oS 58 7oS5 5S .= 7o 5of<br>20 o—Mm>& ¢ B&Res FI °& °&<br>Banana &<br>Peppers - Jar 20 a o4 5 5<br>10 S s<br>on. LLi: S<br>40 3<br>8 » Rf<br>Boa ig |f ee<br>JalapenoOrganicPeppers - 8020 5ana8< mie o |g e 8 i”<a 7@8<br>s s Hi<br>0 ULL<br><!-- End of picture text -->



<!-- Start of picture text -->
Market Date<br>/x/2020 s/s1/2020<br>oe)<br>Vendor Name<br>Marco's Peppers +<br>| Wea29 | ProdetNeme<br>(All)<br>.8 BananaHabanero Peppers Peppers- Jar- Organic<br>S& JalapenoPoblano PeppersPeppers-- OrganicOrganic<br>Measure Names<br>Mi Quantity Available<br>i Quantity Sold<br>a<br>*<br>a<br>3.<br>iLE<br><!-- End of picture text -->



<!-- Start of picture text -->
Histogram: of ” "Banana Peppers - Jar” ” Sales Per Market<br>55<br>4<br>&4g 3<br>g<br>=<br>2<br>%<br>&z5 2<br>1<br>2 4 6 8 10 12 14 16 18 20 22 24 26 28 30 32 34 36 38 40<br>Quantity Sold Per Market<br><!-- End of picture text -->



<!-- Start of picture text -->
z/yeo18Market Date a2/a1/2019<br>_—D<br>Vendor Name<br>Product Name<br>(All)<br>Banana Peppers - Jar<br>Habanero Peppers - Organic<br>Jalapeno Peppers - Organic<br>Poblano Peppers- Organic<br>42<br><!-- End of picture text -->

# **<mark>C H A P T E R</mark> 10** 

## **Building SQL Datasets for Analytical Reporting** 

In previous chapters, we covered basic SQL SELECT syntax and started to use SQL to construct datasets to answer specific questions. In the data analysis world, being asked questions, exploring a database, writing SQL statements to find and pull the data needed to determine the answers, and conducting the analysis of that data to calculate the answers to the questions, is called _ad- hoc reporting_ . 

I often say in my data science conference presentations that the process depicted in Figure 10.1 is what is expected of any data analyst or data scientist: to be able to listen to a question from a business stakeholder, determine how it might be answered using data from the database, retrieve the data needed to answer it, calculate the answers, and present that result in a form that the business stakeholder can understand and use to make decisions. 

You now know enough SQL to answer some basic ad- hoc questions about what is occurring at the fictional farmer’s market using the demonstration database by filtering, joining, and summarizing the data. 

In the remaining chapters, we’ll take those skills to the next level and demonstrate how to think through multiple analysis questions, simulating what it might be like to write queries to answer a question posed by a business stakeholder. We’ll design and develop analytical datasets that can be used repeatedly to facilitate ad- hoc reporting, build dashboards, and serve as inputs into predictive models. 

**143** 

**144 Chapter 10** ■ **Building SQL Datasets for Analytical Reporting** 



<!-- Start of picture text -->
Business Question<br>Data Question<br>Data Answer<br>Business Answer<br><!-- End of picture text -->

**Figure 10.1** 

#### **Thinking Through Analytical Dataset Requirements** 

In this chapter, we’ll walk through some examples of designing reusable datasets that can be queried to build many report variations. An experienced analyst who goes through the steps in Figure 10.1 won’t only think about writing a query to answer the immediate question at hand but will think more generally about “Building Datasets for Analysis” (we’re finally getting to this book’s subtitle!) and designing SQL queries that combine and summarize data in a way that can then be used to answer many similar questions that might arise as offshoots of the original question. 

You can think of a dataset as being like a table, already summarized at the desired level of detail, with multiple measures and dimensions that you can break down those metrics by. An analytical dataset is designed for use in reports and predictive models, and usually combines data from several tables summarized at a granularity (row level of detail) that lends itself to multiple analyses. If the dataset is meant to be used in a visual report or dashboard, it’s a good idea to join in all fields that could be used for human- readable report labels (like vendor names instead of just IDs), measures (the numeric values you’ll want to summarize and report on, such as sales), and dimensions (for grouping and slicing and dicing the measures, like product category). 

Because I know that the first question I’m asked to answer with an ad- hoc query is almost never the only question, I will use any remaining project time to try to anticipate follow- up questions and design a dataset that may be useful for answering them. Adding additional relevant columns or calculations to a query also makes the resulting dataset reusable for future reporting purposes. 

Anticipating potential follow- up questions is a skill that analysts develop over time, through experience. For example, if the manager of the farmer’s market asked me “What were the total sales at the market last week?” I would expect to be asked more questions after delivering the answer to that one, such as, 

**Chapter 10** ■ **Building SQL Datasets for Analytical Reporting 145** 

“How many sales were at the Wednesday market versus the Saturday market last week?” or “Can you calculate the total sales over another time period?” or “Let’s track these weekly market sales over time,” or “Now that we have the total sales for last week, can we break this down by vendor?” Given time, I could build a single dataset that could be imported into a reporting system like Tableau and used to answer all of these questions. 

Since we’re talking about summary sales and time, I would first think about all of the different time periods by which someone might want to “slice and dice” market sales. Someone could ask to summarize sales by minute, hour, day, week, month, year, and so on. Then I would think about dimensions other than time that people might want to filter or summarize sales by, such as vendor or customer zip code. 

Whatever granularity I choose to make the dataset (at what level of detail I choose to summarize it) dictates the lowest level of detail at which I can then filter or summarize a report based on that dataset. So, for example, if I build a dataset that summarizes the data by week, I will not be able to produce a daily sales report from that dataset, because weeks are less granular than days. 

Conversely, the granularity I choose means I will always need to write summary queries for any question that’s at a higher level of aggregation than the dataset. For example, if I create a dataset that summarizes sales per minute, I will always have to use GROUP BY in the query, or use a reporting tool to summarize sets of rows, to answer any question that needs those minutes combined into a longer time period like hours or days. 

If you are developing a dataset for use in a reporting tool that makes aggregation simple, such as Tableau, you may want to keep it as granular as possible, so you can drill down to as small of a time period as is available in the data. In Tableau, measures are automatically summarized by default as you build a report, and you have to instead break down the summary measures by adding dimensions. Summarizing by date in Tableau is as simple as dragging any datetime value into a report and choosing at what timescale you want to view that date field, regardless of whether the underlying dataset has one row per day or one row per second. 

However, if you are primarily going to be querying the dataset with SQL, you will have to use GROUP BY and structure your queries to summarize at the desired level every time you use it to build a report. So, if you anticipate that you will frequently be summarizing by day, it would make sense to build a dataset that is already summarized to one row per day. You can always go back to the source data and write a custom query for that rare case when you’re expected to report on sales per hour, but reuse the pre- summarized daily sales dataset as a shortcut for the more common report requests in this case. 

Let’s say that for this example, I can safely assume that most reports will be summarized at the daily or weekly level, so I will choose to build a dataset that has one row per day. In each row, I can summarize not only the total daily 

|| market_date|vendor_id|sales|
|---|---|---|
|2019-04-03|Fi|76.06|
|2019-84-83|8|255.00|
|2019-04-06|Fy|1286.60|
|2019-84-86|8|292.08|
|2019-04-18|7|92.00|
|2619-84-18|8|214.88|
|2019-04-13|7|126.08|
|2619-64-13|8|264.56|
|2019-64-17|7|136.58|
|2019-64-17|8|261.00|
|2019-64-26|7|80.08|
|2019-64-28|8|218.50|



**Chapter 10** ■ **Building SQL Datasets for Analytical Reporting 147** 

SELECT market_date, vendor_id, ROUND(SUM(quantity * cost_to_customer_per_qty),2) AS sales FROM farmers_market.customer_purchases GROUP BY market_date, vendor_id ORDER BY market_date, vendor_id 

This is a good time to review whether my results will allow me to answer the other questions I assumed I might be asked in the future and to determine what other information might be valuable to add to the dataset for reporting purposes. Let’s go through each one: 

- **What were the total sales at the market last week?** There are multiple ways to accomplish this. A simple option is to filter the results by last week’s date range and sum the sales. If we wanted the report to update dynamically as data is added, always adding up sales “over the last week,” we could have our query subtract 7 days from the current date and filter to only sales in rows with a market_date value that occurred after that date. We have the fields necessary to accomplish this. 

- **How many of last week’s sales were at the Wednesday market versus the Saturday market?** In addition to the approach to answering the previous question, we can use the DAYNAME() function in MySQL to return the name of the day of the week of each market date. It might be a good idea to add the day of the week to the dataset so it’s easily accessible for report labeling and grouping. If we explore the market_date_info table, we’ll find that there is a field called market_day that already includes the weekday label of each market date, so there is actually no need to calculate it; we can join it in. 

- **Can we calculate the total sales over another time period?** Yes, we can filter the results of the existing query to any date range and sum up the sales. 

- **Can we track the weekly market sales over time?** We can use the MySQL functions WEEK() and YEAR() on the market_date field to pull those values into the dataset and group rows by week number (which could be especially useful for year over year comparisons) or by year and week (for a weekly summary time series). However, these values are also already in the market_date_info table, so we can join those in to allow reporting by that information. 



<!-- Start of picture text -->
| market_date market_day market_week market_year vendor_id vendor_name ___vendor_type__sales_|<br>2019-04-83 Wednesday 14 2019 7 Marco's Peppers Fresh Focused 76.08<br>2019-04-83 Wednesday 14 2019 8 Annie's Pies Prepared Foods 255.00<br>2019-04-86 Saturday 14 2019 7 Marco's Peppers Fresh Focused 126.08<br>2019-04-86 Saturday 14 2019 8 Annie's Pies Prepared Foods 292.00<br>2019-04-16 Wednesday 15 2019 7 Marco's Peppers Fresh Focused 92.08<br>2019-04-18 Wednesday 15 2019 8 Annie's Pies Prepared Foods 214.00<br>2019-04-13 Saturday 15 2019 7 Marco's Peppers Fresh Focused 128.08<br>2019-04-13 Saturday 15 2019 8 Annie's Pies Prepared Foods 204.5@<br>2019-04-17 Wednesday 16 2019 7 Marco's Peppers Fresh Focused 136.58<br>2019-04-17 Wednesday 16 2019 8 Annie's Pies Prepared Foods 281.00<br>2019-04-28 Saturday 16 2019 7 Marco's Peppers Fresh Focused 88.08<br>2019-84-28 Saturday 16 2019 8 Annie's Pies Prepared Foods 210.5@<br>2019-04-24 Wednesday 17 2019 7 Marco's Peppers Fresh Focused 188.08<br><!-- End of picture text -->

||market_date|market_day|market_week|market_year|vendor_id|vendor_name__|vendor_type_|sales_||
|---|---|---|---|---|---|---|---|
|<br>2019-04-83|<br>Wednesday|<br>14|<br>2019|<br>7|<br>Marco'sPeppers|FreshFocused|76.08|
|2019-04-83|Wednesday|14|2019|8|<br>Annie's Pies|<br>Prepared Foods|255.00|
|2019-04-86|Saturday|14|2019|7|Marco's Peppers|Fresh Focused|126.08|
|2019-04-86|Saturday|14|2019|8|Annie's Pies|Prepared Foods|292.00|
|2019-04-16|Wednesday|15|2019|7|Marco'sPeppers|FreshFocused|92.08|
|2019-04-18|Wednesday|15|2019|8|<br>Annie's Pies|<br>Prepared Foods|214.00|
|2019-04-13|Saturday|15|2019|7|Marco's Peppers|Fresh Focused|128.08|
|2019-04-13|Saturday|15|2019|8|Annie's Pies|Prepared Foods|204.5@|
|2019-04-17|Wednesday|16|2019|7|Marco's Peppers|Fresh Focused|136.58|
|2019-04-17|Wednesday|16|2019|8|Annie's Pies|Prepared Foods|281.00|
|2019-04-28|Saturday|16|2019|7|Marco's Peppers|Fresh Focused|88.08|
|2019-84-28|Saturday|16|2019|8|Annie's Pies|Prepared Foods|210.5@|
|2019-04-24|Wednesday|17|2019|7|Marco'sPeppers|FreshFocused|188.08|



**Chapter 10** ■ **Building SQL Datasets for Analytical Reporting** 

**149** 

#### **Using Custom Analytical Datasets in SQL: CTEs and Views** 

There are multiple ways to store queries (and the results of queries) for reuse in reports and other analyses. Some techniques, such as creating new database tables, will be covered in later chapters. Here, we will cover two approaches for more easily querying from the results of custom dataset queries you build: _Common Table Expressions_ and _views_ . 

Most database systems, including MySQL since version 8.0, support Common Table Expressions (CTEs), also known as “WITH clauses.” CTEs allow you to create an alias for an entire query, which allows you to reference it in other queries like you would any database table. 

The syntax for CTEs is: 

WITH [query_alias] AS 

( 

[query] 

), 

[query_2_alias] AS ( [query_2] ) 

SELECT [column list] FROM [query_alias] _..._ [remainder of query that references aliases created above] 

where “[query_alias]” is a placeholder for the name you want to use to refer to a query later, and “[query]” is a placeholder for the query you want to reuse. If you want to alias multiple queries in the WITH clause, you put each query inside its own set of parentheses, separated by commas. You only use the WITH keyword once at the top, and enter “[alias_name] AS” before each new query you want to later reference. (The AS is not optional in this case.) Each query in the WITH clause can reference any query that preceded it, by using its alias. 

Then below the WITH clause, you start your SELECT statement like you normally would, and use the query aliases to refer to the results of each of them. They are run before the rest of your queries that rely on their results, the same way they would be if you put them inside the SELECT statement as subqueries, which were covered in Chapter 7, “Window Functions Frequently Used by Data Scientists.” 

For example, if we wanted to reuse the previous query we wrote to generate the dataset of sales summarized by date and vendor for a report that summarizes 

|| market_year|market_week|weekly_sales|
|---|---|---|
|2619|14|743.08|
|2019|15|630.50|
|2619|16|788.08|
|2019|17|593.50|
|2619|18|742.08|
|2019|19|642.58|
|2619|28|585.508|
|2019|21|725.50|
|2619|22|621.60|
|2019|23|765.08|
|2619|24|646.20|
|2019|25|648.78|
|2619|26|679.20|



**Chapter 10** ■ **Building SQL Datasets for Analytical Reporting 151** 

Notice how the SELECT statement at the bottom references the sales_by_ day_vendor Common Table Expression using its alias, treating it just like a table, and even giving it an even shorter alias, s. You can filter it, perform calculations, and do anything with its fields that you would do with a normal database table. By using a WITH statement instead of a subquery, it keeps this query at the bottom cleaner and easier to understand. 

In most SQL editors, you can highlight the query within each set of parentheses to run just that code inside the WITH statement and view its results, so you know what data is available as you develop your SELECT query below the WITH statement. You can’t highlight only the SELECT statement at the bottom to run it alone, however, because it references sales_by_day_vendor, which is dynamically created by running the WITH statement above it along with it. 

Another approach allows you to develop SELECT statements that depend on a custom dataset in their own SQL editor window, or inside other code such as a Python script, without first including the entire CTE. This involves storing the query as a database _view_ . A view is treated just like a table in SQL, the only difference being that it has run when it’s referenced to dynamically generate a result set (where a table stores the data instead of storing the query), so queries that reference views can take longer to run than queries that reference tables. However, the view is retrieving the latest data from the underlying tables each time it is run, so you are working with the freshest data available when you query from a view. 

If you want to store your dataset as a view (assuming you have been granted database permissions to create a view in a schema), you simply precede your SELECT statement with “CREATE VIEW [schema_name].[view_name] AS”, replacing the bracketed statements with the actual schema name, and the name you are giving the view. 

This is one query in this book that you will not be able to test using an online SQL editor and the sample database, because you won’t have permissions to create a new database object there. The vw_ prefix in the following view name serves as an indicator when writing a query that the object you’re referencing is a view (stored query) and not a table (stored data): 

CREATE VIEW farmers_market.vw_sales_by_day_vendor AS SELECT 

cp.market_date, md.market_day, md.market_week, md.market_year, cp.vendor_id, v.vendor_name, v.vendor_type, ROUND(SUM(cp.quantity * cp.cost_to_customer_per_qty),2) AS sales 

_Continues_ 

|market_date|market_day|market_week|market_year|vendor_id|vendor_name|vendor_type|sales|
|---|---|---|---|---|---|---|---|
|2020-04-81|Wednesday|14|2028|7|Marco's Peppers|Fresh Focused|120.00|
|2020-04-04|Saturday|14|2028|7|Marco's Peppers|Fresh Focused|68.00|
|2020-04-88|Wednesday|15|2628|7|Marco's Peppers|Fresh Focused|100.00|
|202@-@4-11|Saturday|+5|202@|7|Marco's Peppers|Fresh Focused|160.00|
|2020-04-15|Wednesday|16|2628|7|Marco's Peppers|Fresh Focused|108.00|
|2020-04-18|Saturday|16|2028|r|Marco's Peppers|Fresh Focused|144.00|
|2020-04-22|Wednesday|17|2028|F i|Marco's Peppers|Fresh Focused|148.00|
|2020-04-25|Saturday|17|2028|rs|Marco's Peppers|Fresh Focused|148.00|
|2020-04-29|Wednesday|18|2026|7|Marco's Peppers|Fresh Focused|112.00|





<!-- Start of picture text -->
Year over Year Sales by Week<br>Date<br>2019 & $1,000<br>3 ~ TATOO LLL ELEC<br>2020 & $1,0$5 00 MTEL | I.<br>67 8 9 1011 12 13 1415 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52<br>Market Week #<br><!-- End of picture text -->



<!-- Start of picture text -->
Marco's Peppers Sales by Market Date<br>$160.00<br>$150<br>2% $100<br>nnoo<br>3<br>6<br>a<br>$68.00<br>$50<br>$0<br>So Tt oO t+ a i fon)<br>mM>uoa a atroaart-a a=r-a N=-a Nrtaa<br>Market Date [April 2020]<br><!-- End of picture text -->

**154 Chapter 10** ■ **Building SQL Datasets for Analytical Reporting** 

- What percentage of each vendor’s inventory is selling per time period? 

- Did the prices of any products change over time? 

- What are the total sales per vendor for the season? 

- How frequently do vendors discount their product prices? 

- Which vendor sold the most tomatoes last week? 

We can’t answer questions about any time periods shorter than a day, because the timestamp of the sale isn’t included. We also don’t have any detailed information about customers, but because we have date, vendor, and product dimensions, we can slice and dice different metrics by those values. 

We can add some calculated fields to the query for reporting purposes without pulling in any additional columns. The following query adds fields calculating the percentage of product quantity sold and the total discount and aliases them percent_of_available_sold and discount_amount, respectively. Let’s store this dataset as a view and use it to answer a business question: 

CREATE VIEW farmers_market.vw_sales_per_date_vendor_product AS SELECT vi.market_date, vi.vendor_id, v.vendor_name, vi.product_id, p.product_name, vi.quantity AS quantity_available, sales.quantity_sold, ROUND((sales.quantity_sold / vi.quantity) * 100, 2) AS percent_of_ available_sold, vi.original_price, (vi.original_price * sales.quantity_sold) - sales.total_sales AS discount_amount, sales.total_sales FROM farmers_market.vendor_inventory AS vi LEFT JOIN ( SELECT market_date, vendor_id, product_id, SUM(quantity) quantity_sold, SUM(quantity * cost_to_customer_per_qty) AS total_sales FROM farmers_market.customer_purchases GROUP BY market_date, vendor_id, product_id ) AS sales ON vi.market_date = sales.market_date AND vi.vendor_id = sales.vendor_id AND vi.product_id = sales.product_id LEFT JOIN farmers_market.vendor v ON vi.vendor_id = v.vendor_id 

7° peer s.market_cate, s.vendor_id, s.vender_rane, $.preduct_i4, $.product_nase, ROUNO(s.tetel_seles, 2) AS vender_product_seles_on_serket_date, AOUNO(SUM(#.total_sales) OVER (PARTITION BY market_date, venéor_{d), 2) AS verdor_total_seles_on_arket_date, ROWMO((s.totel_sales / Sun(s.total_sales) OVER (PARTITION BY market_éate, vendor_1¢)) * 100, 1) AS preduct_percent_ef_vendor_sales FROM farmers market vm_sales_per_datevendor product AS s ORDER GY market_date, vendori¢ < Rawat Grid 9 Pree Row | Gece: Gy | ver Catone narket_aate vendor_ié verdor_rane procuct_id product_neme verdor_prodact_sales_on_warket_dat« vendor_total_cales_on_sarket_éate product_percent_o#_vendor_cales 2020-04-22 7 Marco's Peppers 4 Banana Peppers - Jer 148.68 148.08 108.€ 2020-04-22 8 Annie's Pies 5 Wnole West Bread = 143.00 305.00 46.9 2020-08-22 & Annie's Pies 7 apple Pie 99.00 305.08 Pr 2020-04-22 8 Annie's Pies 8 Gerry Pie 72.00 305.00 23.6 

**156 Chapter 10** ■ **Building SQL Datasets for Analytical Reporting** 

In the next line of the SQL statement in Figure 10.8, we are summing up each vendor’s sales (of all of their products) on each market date, using a window function that partitions sales by market_date and vendor_id. (See Chapter 7 for more information about window functions.) Then we give that sum an alias of vendor_total_sales_on_market_date and round it to two decimal places. 

We now have the total sales for the vendor for the day on each row, and we already had the total sales of each product the vendor sold that day. The calculation in the next line is that first dollar amount divided by the second dollar amount, which calculates the percentage of the vendor’s sales on that market date represented by each product. 

In the pictured rows of output at the bottom of Figure 10.8, you can see that Marco’s Peppers is only selling one product on 4/22/2020, so the sales on that row represent 100% of Marco’s sales for the day. Annie’s Pies is selling three different products, and you can see in the final column what portion of Annie’s total sales was contributed by each product. 

We can write additional queries against this reusable dataset to build other reports in SQL, too. To use SQL to get the same data summary that is shown in Figure 9.18, which was grouped and visualized in Tableau, we can query the view as follows: 

SELECT market_date, vendor_name, product_name, quantity_available, quantity_sold FROM farmers_market.vw_sales_per_date_vendor_product AS s WHERE market_date BETWEEN '2020- 06- 01' AND '2020- 07- 31' AND vendor_name = 'Marco''s Peppers' AND product_id IN (2, 4) ORDER BY market_date, product_id 

A partial view of the output of this query is in Figure 10.9, and you can compare the numbers to those in the bar chart in Figure 9.18. One benefit of saving queries that generate summary datasets so they are available to reuse as needed, is that any tool you use to pull the data will be referencing the underlying data, table joins, and calculated values. As long as the data isn’t changing between the report generation times, everyone using the defined dataset can get the same results. 

|market_date|vendor_name|product_name|quantity_available|quantity_sold|
|---|---|---|---|---|
|2028-@7-@1|Marco's Peppers|Jalapeno Peppers<br>- Organic|24.17|21.24|
|2020-@7-@1|Marco's Peppers|Banana Peppers<br>- Jar|48.00|16.08|
|2020-07-84|Marco's Peppers|Jalapeno Peppers<br>- Organic|31.82|38.88|
|2020-07-84|Marco's Peppers|Banana Peppers<br>- Jar|48.008|15.00|
|2028-87-88|Marco's Peppers|Jalapeno Peppers<br>- Organic|28.19|13.79|
|2020-07-88|Marco's Peppers|Banana Peppers<br>- Jar|38.88|17.00|
|2020-07-11|Marco's Peppers|Jalapeno Peppers<br>- Organic|28.49|13.76|
|2020-67-11|Marco's Peppers|Banana Peppers<br>- Jar|48.08|11.68|
|2028-87-15|Marco's Peppers|Jalapeno Peppers<br>- Organic|29.75|21.31|
|2020-07-15|Marco's Peppers|Banana Peppers<br>- Jar|48.08|17.00|
|2020-87-18|Marco's Peppers|Jalapeno Peppers<br>- Organic|36.98|11.33|
|2020-87-18|Marco's Peppers|Banana Peppers<br>- Jar|38.88|7.88|
|2020-87-22|Marco's Peppers|Jalapeno Peppers<br>- Organic|31.27|23.82|





<!-- Start of picture text -->
C H A P T E R<br><!-- End of picture text -->

# **11** 

## **More Advanced Query Structures** 

Most of this book is targeted at beginners, but because beginners can quickly become more advanced in developing SQL, I wanted to give you some ideas of what is possible when you think a little more creatively and go beyond the simplest SELECT statements. SQL is a powerful way to shape and summarize data into a wide variety forms that can be used for many types of analyses. This chapter includes a few examples of more complex query structures. 

#### **UNIONs** 

One query structure that I haven’t yet covered in this book, but which certainly deserves a mention, is the UNION query. Using a UNION, you can combine any two queries that result in the same number of columns with the same data types. The columns must be in the same order in both queries. There are many possible use cases for UNION queries, but the syntax is simple: write two queries with the same number and type of fields, and put a UNION keyword between them: 

> SELECT market_year, MIN(market_date) AS first_market_date FROM farmers_market.market_date_info WHERE market_year = '2019' 

UNION 

_Continues_ 

**159** 

**160 Chapter 11** ■ **More Advanced Query Structures** 

###### _(continued)_ 

SELECT market_year, MIN(market_date) AS first_market_date FROM farmers_market.market_date_info WHERE market_year = '2020' 

Of course, this isn’t a sensible use case, because you could just write one query, GROUP BY market_year, and filter to WHERE market_year IN (‘2019’,’2020’) and get the same output. There are always multiple ways to write queries, but sometimes combining two queries with identical columns selected but different criteria or different aggregation is the quickest way to get the results you want. 

For a more complex example combining CTEs and UNIONs, we’ll build a report that shows the products with the largest quantities available at each market: the bulk product with the largest weight available, and the unit product with the highest count available: 

WITH product_quantity_by_date AS ( SELECT vi.market_date, vi.product_id, p.product_name, SUM(vi.quantity) AS total_quantity_available, p.product_qty_type FROM farmers_market.vendor_inventory vi LEFT JOIN farmers_market.product p ON vi.product_id = p.product_id GROUP BY market_date, product_id ) SELECT * FROM ( SELECT market_date, product_id, product_name, total_quantity_available, product_qty_type, RANK() OVER (PARTITION BY market_date ORDER BY total_quantity_ available DESC) AS quantity_rank FROM product_quantity_by_date WHERE product_qty_type = 'unit' UNION SELECT market_date, product_id, product_name, total_quantity_available, product_qty_type, 

|market_date|product_id|product_name||total_quantity_available|product_qty_type|quantity_rank|
|---|---|---|---|---|---|---|
|2019-88-@3|16|Sweet Corn||308.88|unit|Es|
|2019-88-83|2|Jalapeno Peppers<br>|- Organic|32.23|lbs|a|
|2019-08-07|16|SweetCorn||308.88|unit|1|
|2019-08-87|2|<br>Jalapeno Peppers<br>|- Organic|29.28|lbs|1|
|2019-08-10|16|Sweet Corn||258.08|unit|1|
|2019-08-18|2|Jalapeno Peppers<br>|- Organic|27.18|lbs|1|
|2019-88-14|16|Sweet Corn||208.88|unit|1|
|2019-88-14|2|Jalapeno Peppers<br>|- Organic|33.35|lbs|1|
|2019-08-17|16|Sweet Corn||308.00|unit|1|
|2019-@8-17|2|Jalapeno Peppers<br>|- Organic|25.58|lbs|1|
|2019-@8-21|16|Sweet Corn||258.08|unit|1|
|2019-@8-21|2|Jalapeno Peppers<br>|- Organic|32.@2|lbs|1|
|2019-@8-24|16|Sweet Corn||258.08|unit|1|
|2019-08-24|2|Jalapeno Peppers<br>|- Organic|17.29|lbs|1|
|2019-08-28|16|Sweet Corn||258.08|unit|1|
|2019-@8-28|2|Jalapeno Peppers<br>|- Organic|26.20|lbs|1|
|2019-08-31<br>|16<br>|Sweet Corn<br><br>||308.88<br>|unit<br>|Z<br>|
|2019-@8-31|2|Jalapeno Peppers<br>|- Organic|27.87|lbs|1|



**162 Chapter 11** ■ **More Advanced Query Structures** 

For the sake of instruction, and because I frequently say that there are multiple ways to construct queries in SQL that result in identical outputs, there is at least one other way to get the preceding output that doesn’t require a UNION. In the following query, the second query in the WITH clause queries from the first query in the WITH clause, and the final SELECT statement simply filters the result of the second query: 

WITH product_quantity_by_date AS ( SELECT vi.market_date, vi.product_id, p.product_name, SUM(vi.quantity) AS total_quantity_available, p.product_qty_type FROM farmers_market.vendor_inventory vi LEFT JOIN farmers_market.product p ON vi.product_id = p.product_id GROUP BY market_date, product_id ), rank_by_qty_type AS ( SELECT market_date, product_id, product_name, total_quantity_available, product_qty_type, RANK() OVER (PARTITION BY market_date, product_qty_type ORDER BY total_quantity_available DESC) AS quantity_rank FROM product_quantity_by_date ) SELECT * FROM rank_by_qty_type WHERE quantity_rank = 1 ORDER BY market_date 

We were able to accomplish the same result without the UNION by partitioning by both the market_date and product_qty_type in the RANK() function, resulting in a ranking for each date and quantity type. 

Because I have shown two examples of UNION queries that don’t actually require UNIONs, I wanted to mention one case when a UNION is definitely required: when you have separate tables with the same columns, representing different time periods. This could happen, for example, when you have event logs (such as website traffic logs) that are stored across multiple files, and each file is loaded into its own table in the database. Or, the tables could be static snapshots of the same dynamic dataset from different points in time. Or, maybe the data was 

**Chapter 11** ■ **More Advanced Query Structures 163** 

migrated from one system into another, and you need to pull data from tables in two different systems and combine them together into one view to see the entire history of records. 

#### **Self- Join to Determine To- Date Maximum** 

A _self- join_ in SQL is when a table is joined to itself (you can think of it like two copies of the table joined together) in order to compare rows to one another. 

You write the SQL for a self- join just like any other join, but reference the same table name twice. To differentiate the two “copies” of the table, give each one its own alias: 

SELECT t1.id1, t1.field2, t2.field2, t2.field3 

FROM mytable AS t1 

LEFT JOIN mytable AS t2 

ON t1.id1 = t2.id1 

This particular example is meant to demonstrate the syntax and not highlight a typical use case, because you would not normally be joining on a primary key and comparing a row to itself. One more realistic use case is using a comparison operator other than an equal sign to accomplish something such as joining every row to every previous row, as shown in the queries associated with Figures 11.3 through 11.5 below. 

Let’s say we wanted to show an aggregate metric changing over time, comparing each value to all previous values. One reason you might want to compare a value to all previous values is to create a “record high to- date” indicator. 

One possible use case might be the need to automatically determine when the count of positive COVID- 19 tests for a region on a particular day set a record as the highest count to- date. One way you could use this data point is to create a visual indicator on a COVID- 19 tracking dashboard that appears when the count of new cases hits a new record high. Building this indicator into your dataset allows you to look back at the reported positive case counts at any past point in time and know if the number that day had set a new record high at the time. 

We can demonstrate an example of that type of query using the Farmer’s Market database by creating a report showing whether the total sales on each market date were the highest for any market to- date. If we were always looking at data filtered to dates before a selected date, we could simply use the SUM() and MAX() functions to determine the highest total sales for the given date range. But, if we’re looking back at a log of sales on all dates, and want to do the calculation using data from dates prior to each past date without filtering out the later dates from view, we need a different approach. 

|market_date<br>|sales<br>|
|---|---|
||2019-04-@3|439.80|
|2019-04-86|557.50|
|2019-04-10|483.43|
|2019-04-13|384.62|
|2019-94-17|587.50|
|2019-04-20|433.73|
|2019-04-24|346.42|
|2019-04-27|433.58|
|2019-@5-@1|488.92|
|2019-@5-@4|496.74|





<!-- Start of picture text -->
|<br><!-- End of picture text -->

|market_date|sales|market_date|sales|
|---|---|---|---|
|2019-04-13|364.62|2019-64-63|439.00|
|2019-04-13|384.62|2019-04-66|557.58|
|2019-04-15|364.62|2019-04-18|4683.45|



market_date sales previous_max_sales 2619-84-15 384.62 557.58 

|market_date|sales|previous_max_sales|sales_record_set|
|---|---|---|---|
|2019-04-66|557.5@|439.66|YES|
|2019-84-18|483.43|557.58|NO|
|2019-84-13|384.62|557.58|NO|
|2019-84-17|507.50|557.50|NO|
|2619-64-26|433.73|557.50|NO|
|2019-84-24|346.42|557.58|NO|
|2019-04-27|433.58|557.58|NO|
|2019-85-01|488.92|557.50|NO|
|2019-85-64|496.74|557.58|NO|
|2019-85-68|498.86|557.50|NO|
|2019-85-11|446.5@|557.50|NO|
|2019-85-15|426.06|557.56|NO|
|2019-85-18|465.93|557.50|NO|
|2019-85-22|531.48|557.58|NO|
|2019-85-25|376.31|557.50|NO|
|2019-85-29|576.3@|557.58|YES|
|2019-06-61|472.02|576.30|NO|
|2019-86-65|377.54|576.38|NO|
|2619-06-88|470.85|576.30|NO|



|customer_id|market_date|first_purchase_date|
|---|---|---|
|2|2026-08-15|2019-64-66|
|2|2620-09-19|2019-84-86|
|J|2020-16-67|2019-04-86|
|2|2019-86-85|2019-84-86|
|2|2019-67-27|2019-64-66|
|3|2019-87-18|2019-84-83|
|3|2019-67-31|2019-64-63|
|3|2619-89-25|2019-84-83|
|3|2019-89-28|2019-64-83|
|3|2620-89-16|2019-84-83|
|3|2020-09-26|2019-64-03|
|3|2019-87-06|2019-84-83|
|3|2019-67-20|2019-04-03|



|market_year|market_week|customer_visit_count|distinct_customer_count|
|---|---|---|---|
|2019|14|25|19|
|2019|15|23|16|
|2019|16|27|18|
|2019|17|29|28|
|2019|18|27|21|
|2619|19|25|18|
|2019|208|23|19|
|2619|21|24|18|
|2019|22|27|19|
|2619|23|28|28|
|2019|24|38|22|



**170 Chapter 11** ■ **More Advanced Query Structures** 

Inside the COUNT() function is a CASE statement. Can you tell what it does? It is looking for rows in the results of the customer_markets_attended CTE where the market_date (the date when the customer made the purchase) is equal to the customer’s first purchase date. If those values match, the CASE statement returns a customer_id to count. If not, the CASE statement returns NULL. So, the result is a distinct count of customers that made their first purchase that week. 

The second field, which is the last listed in the following full query, then divides that same value by the total distinct count of customer IDs, giving us a percentage. The result of this query is shown in Figure 11.8. 

WITH customer_markets_attended AS ( SELECT DISTINCT customer_id, market_date, MIN(market_date) OVER(PARTITION BY cp.customer_id) AS first_purchase_ date FROM farmers_market.customer_purchases cp ) SELECT md.market_year, md.market_week, COUNT(customer_id) AS customer_visit_count, COUNT(DISTINCT customer_id) AS distinct_customer_count, COUNT(DISTINCT CASE WHEN cma.market_date = cma.first_purchase_date THEN customer_id ELSE NULL END)AS new_customer_count, COUNT(DISTINCT CASE WHEN cma.market_date = cma.first_purchase_date THEN customer_id ELSE NULL END) / COUNT(DISTINCT customer_id) AS new_customer_percent FROM customer_markets_attended AS cma LEFT JOIN farmers_market.market_date_info AS md ON cma.market_date = md.market_date GROUP BY md.market_year, md.market_week ORDER BY md.market_year, md.market_week 

|market_year|market_week|customer_visit_count|distinct_customer_count|new_customer_count|new_customer_percent|
|---|---|---|---|---|---|
|2019|14|25|19|19|1.0008|
|2019|15|23|16|2|@.1258|
|2019|16|27|18|3|@.1667|
|2019|17|29|28|1|8.8580|
|2019|18|27|21|a4|@.0476|
|2019|19|25|18|e|8.8080|
|2019|28|23|19|e|2.0000|
|2019|21|24|18|e|8.8000|
|2019|22|27|19|@|8.0000|
|2019|23|28|28|e|8.8000|
|2019|24|38|22|@|@.2000|



# **<mark>C H A P T E R</mark> 12** 

## **Creating Machine Learning Datasets Using SQL** 

In previous chapters, we introduced SQL concepts and walked through some analytical reporting examples, but we have not yet focused on the specifics of dataset design for predictive modeling applications. In this chapter, we’ll discuss the development of datasets for two types of algorithms: classification and time series models. 

A _binary classification model_ predicts whether a record belongs to one category or another. For example, a heart disease classification model might analyze data from a patient’s medical history to determine whether they’re likely to develop heart disease, or not. A weather model could use past and current temperature, precipitation, pressure, and wind measurements, as well as those from surrounding geographic areas, to predict whether or not it will rain in the next 24 hours. In a retail scenario like a farmer’s market, the seller may want to predict whether a customer will return to make another purchase within a certain time frame, or not. 

In order to make predictions, the model needs to be trained. Binary classifiers are a type of _supervised learning_ model, which means they are trained by passing example rows of data (also called instances, observations, or feature vectors) labeled with each of the possible outcomes into the algorithm, so it can detect patterns and identify characteristics that are more strongly associated with one result or the other. Some example instances are set aside to test the trained model, feeding them into the algorithm to generate predictions we can compare to the known actual outcomes in order to check the model’s performance and determine in what ways the model is incorrect, so we can make adjustments to it. 

**173** 

**174 Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

A _time series model_ performs statistical operations on a series of measurements over time to forecast what the measurement might be at some point in time in the future. The training data for a time series model is a running log of data measurements from past points in time. Someone could use an hourly history of a stock’s prices to attempt to predict the value of an investment at the end of the day. A college might use historical counts of applications, admission offers, enrolled students, and deposits paid per week to generate a weekly forecast of incoming freshman class enrollment. A farmer’s market may use purchases over time to detect seasonal product sales trends and growth in the customer base, or try to predict how many ears of corn will sell per week next month. 

Each type of model requires a different type of dataset, and we’ll review some approaches for preparing datasets for these two common types of models using SQL. 

#### **Datasets for Time Series Models** 

The simplest type of time series forecasting uses a single variable measured over specified time intervals to predict the value of that same variable at a future point in time. A dataset for training a simple time series model can consist of just two columns: a column with dates or datetime values that indicate the time of measurement, and a column with the value being measured. 

For example, a model to predict the high temperature in a location tomorrow could have a dataset with years’ worth of daily high temperatures measured at that location. The dataset would have one row per day, with one column for the date, and another for the daily high temperature measured. A time series algorithm could detect seasonal temperature patterns, long- term trends, and the most recent daily high temperatures to predict what the high temperature might be tomorrow. 

Let’s create a dataset that allows us to plot a time series of farmer’s market sales per week. Note that this will be a simplistic view of sales, because it will not take into consideration changes in vendors over time, available inventory at different times of year, or external economic factors. 

In Chapter 10, “Building SQL Datasets for Analytical Reporting,” we created a dataset that summarized sales per market date. Here, we’ll further summarize that data to a weekly level. Because we have joined the customer_purchases table to the market_date_info table and there is a market_week field available, you may assume that we want to group by that field. However, remember that market_week is a number that represents the week of the year, and every year has week numbers 1 through 52. So, if you group by market_week only, you will be adding sales from the same calendar weeks from different years together! Therefore, we will need to GROUP BY both market_year and market_week.  However, 

|first_market_date_of_week<br><br>|weekly_sales<br>|
|---|---|
|2020-07-15.<br>—~™|903.09|
|2020-07-22|629.79|
|2020-07-29|724.19|
|2028-88-85|983.64|
|2020-08-12|1055.41|
|2028-88-19|992.47|
|2020-08-26|954.71|
|2020-89-82|693.38|
|2020-@9-@9|969.53|
|2020-89-16|1691.76|
|2020-09-23|846.83|
|2028-89-30|1011.90|
|2028-10-07|1135.33|





<!-- Start of picture text -->
Time-Series Forecast of Weekly Farmer’s Market Sales<br>100<br>Zs<br>First Market Date Of Week<br><!-- End of picture text -->



<!-- Start of picture text -->
oe<br>M Estimate<br><!-- End of picture text -->

**Chapter 12** ■ **Creating Machine Learning Datasets Using SQL 177** 

history of a patient, is it likely that they have heart disease, or not? Given the current and summarized past weather data, is it likely to rain within the next 24 hours, or not? Many of these algorithms can also output a probability or likelihood score, so you can also determine how “sure” the algorithm is that the instance should be classified into one category or the other (how well it matches the patterns detected for training examples in either class). 

These algorithms need training data that is in the same form as the data to be classified. For example, if you want the algorithm to take a patient’s medical history, including current vital measurements, as input, then the training data has to be at the same granularity and level of summary. Based on the dataset it was trained on, your classification model may expect one row of data per patient, with input fields such as a patient’s age, sex, cholesterol as of five years ago, cholesterol as of one year ago, cholesterol measured today (the day of diagnosis), number of years that the patient has smoked cigarettes (as of the day of diagnosis), resting blood pressure as of five years ago, resting blood pressure as of one year ago, resting blood pressure measured today, resting ECG results, chest pain level indicator, and other summary metrics. In this case, each training “instance” (row of data, or vector) should have the data as of the diagnosis date, as well as the measurements or cholesterol and blood pressure from one and five years prior to the diagnosis date, so the duration between those two data points in the training data is as similar as possible to the duration between those two data points in the data you are passing through the trained model to be classified. The conditions under which the model will be applied need to be considered when designing the dataset. 

Say you trained your model on data from a study that was structured that way, collecting data over a five- year period, but it’s unlikely that you will have a five- year history of those measurements for current patients you want this algorithm to make a prediction for. You might not want to include the data from five years ago in the training dataset, since the model might not be good at classifying records with NULL values in the “resting blood pressure as of five years ago” field and other fields requiring past data, if all of the training instances included those values. Alternatively, training a model on data collected five years ago with outcomes as of the current year would be ideal if the thing you’re trying to predict is whether a patient will develop heart disease five years from now. 

Every classification model requires a _target variable_ , which is the thing you’re trying to predict. In binary classifiers, you can usually input the target as a binary value of 1 or 0, with each number representing each outcome. The target variable in the preceding example is a binary flag indicating a diagnosis of heart disease (or no heart disease) as of the date of the latest cholesterol and blood pressure measurements. 

**178 Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

We won’t get into the details of how much past data with known outcomes is required for training and testing a model here, as it depends on the type of model, the number of columns, the variation in the data values, and many other factors beyond the scope of this book. We also won’t be training classification models in this book. However, we will discuss how to structure the datasets needed for binary classification model training and prediction, and how to use SQL to pull the data you need to train and run a classifier. 

When thinking about how to structure a dataset for binary classification, the first thing you’ll need to determine is the target variable, meaning the categories you’re building a model to classify records into. Often, the target variable needs a time bounding, so instead of predicting “Will this patient develop heart disease?” the outcome being predicted could be “Will this patient be diagnosed with heart disease in the next five years?” The time bounding will affect choices you make when designing the training dataset. 

##### **Creating the Dataset** 

To have a concrete example to discuss, we’ll build a dataset that could be used to train a model that can predict an answer to the question “Will this customer who just made a purchase return to make another purchase within the next month?” The binary target variable is “makes another purchase within 30 days,” with the values 1 for “yes” and 0 for “no.” With this time- limited target variable, we can create a training dataset that summarizes information about each customer as of the date of each purchase, and flag that row with a 1 if that customer made another purchase within a month, and 0 if they did not. Now, instead of having one training example per customer, we have one training example per customer per purchase date. 

The benefit of having multiple records per customer is that a lot more training instances are available for the model to use to detect patterns in the data. Additionally, a person’s behavior can change over time, so having a snapshot record of their summary activity every time they make a purchase, and a record of whether they came back within a month of making that purchase, can help the algorithm determine what impact certain activities may have on behavior. One effect of this approach to be aware of is that frequent customers will be overrepresented in the dataset, which could have different impacts depending on the model, and could lead to overfitting the model to that type of customer. (Because a one- time customer will only be in the training dataset one time, while a frequent customer will be in the training dataset many times.) 

Setting up your query to produce a dataset that is at the correct granularity with a target variable that is time- bound can be the most complicated step of the query design process, and it’s worth taking the time to make sure it is calculated correctly before pulling in any other data fields. When I first designed 

**Chapter 12** ■ **Creating Machine Learning Datasets Using SQL 179** 

this example and the dataset to pair with it, I set it up to determine whether each customer makes a purchase in the next calendar month (for example: if the purchase record is from April, will the customer make a purchase in May?). That is one way to approach this model that would be perfectly valid, if that’s the type of prediction you wanted to make. However, I quickly realized that the time duration for the target variable wouldn’t be consistent. Depending on when in April the customer made a purchase, the target variable could be 1 (yes) if the next purchase date was one day after the initial purchase, up to almost two months later if the initial purchase was on April 1 and the second purchase was on May 30. So, I decided to instead put a dynamic one- month time limit after each purchase for determining the returning customer flag value. So in the following queries, the target variable purchased_again_within_30_days represents whether the customer returned within 30 days of making a purchase, without considering the calendar month. 

With this approach, we can start by creating a CTE that has a row for every purchase, like the query we developed in Chapter 11, “More Advanced Query Structures,” that was associated with Figure 11.5. We can reuse the customer_ markets_attended CTE in the following query to look up whether a customer made another purchase within 30 days after the date of each purchase. 

Before we look at the calculated columns in the following query, let’s look at its FROM, WHERE, and GROUP BY clauses, which determine which table(s) we’re selecting from, how they’re filtered, and the granularity of the final result. You can see that we’re selecting from the customer_purchases table, which has one row per customer per product purchased. There is no WHERE clause, so we’re returning all rows. The GROUP BY clause includes the customer_id and market_date from the customer_purchases table, so we’ll end up with one row per customer per market date at which they made a purchase: 

WITH customer_markets_attended AS ( SELECT DISTINCT customer_id, market_date FROM farmers_market.customer_purchases ORDER BY customer_id, market_date ) 

SELECT 

cp.market_date, cp.customer_id, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS purchase_total, COUNT(DISTINCT cp.vendor_id) AS vendors_patronized, COUNT(DISTINCT cp.product_id) AS different_products_purchased, (SELECT MIN(cma.market_date) FROM customer_markets_attended AS cma 

_Continues_ 

**180 Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

_(continued)_ 

WHERE cma.customer_id = cp.customer_id AND cma.market_date > cp.market_date GROUP BY cma.customer_id) AS customer_next_market_date, DATEDIFF( (SELECT MIN(cma2.market_date) FROM customer_markets_attended AS cma2 WHERE cma2.customer_id = cp.customer_id AND cma2.market_date > cp.market_date GROUP BY cma2.customer_id), cp.market_date) AS days_until_customer_next_market_date, CASE WHEN DATEDIFF( (SELECT MIN(cma3.market_date) FROM customer_markets_attended AS cma3 WHERE cma3.customer_id = cp.customer_id AND cma3.market_date > cp.market_date GROUP BY cma3.customer_id), cp.market_date) <=30 THEN 1 ELSE 0 END AS purchased_again_within_30_days FROM farmers_market.customer_purchases AS cp GROUP BY cp.customer_id, cp.market_date ORDER BY cp.customer_id, cp.market_date 

The purchase_total column should be familiar by now, multiplying the quantity and cost of each item purchased and summing that up to get the total spent by each customer at each market date. The vendors_patronized column is a distinct count of how many different vendors the customer made purchases from that day, and the different_products_purchased column is a distinct count of how many different kinds of products the customer purchased. These calculated columns are also called _engineered features_ when you’re talking about datasets for machine learning, and we’re including them so we can explore the relationship between these values and the target variable. Maybe the more vendors the customer makes purchases from, the more likely they are to purchase an item they like so much that they’ll return within 30 days to buy more. Including this column in the dataset enables the exploration of the relationship between this feature and the target variable. 

The next column, customer_next_market_date, is generated by a subquery that references our CTE. Look at all of the code inside parentheses after different_products_purchased, and before customer_next_market_date. This subquery selects the minimum market date a customer attended, which occurs after the current row’s market_date value. In other words, we’re finding the date of this customer’s next purchase. In the WHERE clause of this subquery, we’re matching up the subquery’s customer_id with the main query’s customer_id (to ensure we’re looking at a single customer’s trips to the market). We’re also limiting the subquery rows to those where the market date occurs 

market_date customer_id purchase_total vendors_patronized different_product: customer_next_market_date days_until_customer_next_ purchased_again_within_3@_days 2020-06-27 25 1.5000 1 1 2@20-@7-@1 4 2 2020-07-21 25 12.0171 2 2 2020-87-22 21 s 2020-@7-22 25 21.9735 2 2 2@20-@8-22 31 e 202@-@8-22 25 7.3124 2 2 2020-28-26 4 1 2020-08-26 25 45.5000 1 1 2020-89-85 1e@ 1 202@-@9-@5 25 31.4735 2 3 2@20-@9-19 14 ss 

**182 Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

are a frequent shopper and have a higher likelihood to come back again soon. Let’s add some columns that indicate which vendors each customer shopped at on each market day and flip the days_until_customer_next_market_date calculation to instead indicate how long it’s been since the customer last shopped before the visit represented by the row: 

WITH customer_markets_attended AS ( SELECT DISTINCT customer_id, market_date FROM farmers_market.customer_purchases ORDER BY customer_id, market_date ) SELECT cp.market_date, cp.customer_id, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS purchase_total, COUNT(DISTINCT cp.vendor_id) AS vendors_patronized, MAX(CASE WHEN cp.vendor_id = 7 THEN 1 ELSE 0 END) AS purchased_from_vendor_7, MAX(CASE WHEN cp.vendor_id = 8 THEN 1 ELSE 0 END) AS purchased_from_vendor_8, COUNT(DISTINCT cp.product_id) AS different_products_purchased, DATEDIFF(cp.market_date, (SELECT MAX(cma.market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date GROUP BY cma.customer_id)) AS days_since_last_customer_market_date, CASE WHEN DATEDIFF( (SELECT MIN(cma.market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date > cp.market_date GROUP BY cma.customer_id), cp.market_date) <=30 THEN 1 ELSE 0 END AS purchased_again_within_30_days FROM farmers_market.customer_purchases AS cp GROUP BY cp.customer_id, cp.market_date ORDER BY cp.customer_id, cp.market_date 

You can see in the preceding query that we added a couple demonstration columns indicating whether each customer purchased from vendors 7 or 8. This technique could be repeated to create a column for every vendor. We also flipped the greater- than sign in the date comparison to a less- than sign, to find 

**Chapter 12** ■ **Creating Machine Learning Datasets Using SQL 183** 

how many days it had been since the customer last made a purchase, in the feature aliased days_since_last_customer_market_date. 

Another type of aggregate value that might be useful to input into a predictive model is some type of representation of the customer’s entire history of farmer’s market shopping, up to the date the row represents. For example, how many times has the customer shopped at the farmer’s market before? A long- time shopper might be more likely to return than a brand- new shopper. 

The ROW_NUMBER window function is one way to calculate this value, counting how many prior rows exist for each customer, but you have to be careful where you put it in the query, because ROW_NUMBER only counts the rows returned by the query. So, if we wanted to count how many times the customer has shopped at the market before as of the market date in the current row, but our main query is filtered to only return data from the year 2019, then our ROW_NUMBER window function will only be able to count previous purchases in 2019 and not the customer’s entire shopping history. 

One solution for our use case is to put the ROW_NUMBER function in the customer_markets_attended CTE, which doesn’t need to be filtered by date, even if you wanted to filter the final output, so we can calculate the number of past markets attended using a similar approach we used to determine the previous purchase date, referencing that CTE. This time, instead of returning the maximum market date that’s less than the market_date in the row, we’ll return the row number that’s associated with the current market_date from that same query. In the following query, this value has the alias market_count in the CTE and is summarized as customer_markets_attended_count in the main query. 

One important note is that when we add the ROW_NUMBER to the customer_ markets_attended query in the WITH clause, we have to modify it to use a GROUP BY instead of a COUNT DISTINCT to summarize per customer_id and market_date. The first eight rows of the output of the COUNT DISTINCT approach are shown in Figure 12.4, and the first eight rows of the output of the GROUP BY approach are shown in Figure 12.5. The reason the ROW_NUMBER returns much higher counts when the query is summarized using COUNT DISTINCT is that the window function is calculated on the dataset before the DISTINCT, so since the results aren’t grouped, it’s returning one row per customer per product purchased, not one row per customer per market_date, then numbering every row in the customer_purchases table for that customer. Grouping by market_date solves that issue because the window function is calculated after the data is aggregated by the GROUP BY. Sometimes it takes trial and error to get the order of operations correct, and this is why it’s important to view the details of the underlying data prior to aggregating, so you know whether the resulting summary data is correct. 

|customer_id|market_date|market_count|
|---|---|---|
|1|2019-84-06|1|
|1|2019-@4-13|2|
|1|2019-@4-17|3|
|1|2019-84-17|4|
|1|2619-04-20|5|
|1|2619-64-28|6|
|1|2619-84-24|7|
|1|2019-04-24|8|



|customer_id|market_date|market_count|
|---|---|---|
|1|2019-04-06|1|
|1|2019-04-13|2|
|1|2019-04-17|3|
|1|2619-84-26|4|
|1|2619-84-24|5|
|1|2019-04-27|6|
|1|2019-@5-61|7|
|i|2019-05-64|8|



**Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

**185** 

FROM farmers_market.customer_purchases AS cp GROUP BY cp.customer_id, cp.market_date ORDER BY cp.customer_id, cp.market_date 

One feature we could add that is likely predictive of whether a customer returns in the next 30 days is how many times they shopped in the previous 30 days. So, we can create another column that puts a time range on the calculation for past markets attended and counts the market dates in the last 30 days. This is demonstrated in the following query by the calculation aliased customer_markets_attended_30days_count. You might extrapolate from this calculation one of the aforementioned alternative ways of determining the total count of markets attended: 

WITH customer_markets_attended AS ( SELECT customer_id, market_date, ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY market_date) AS market_count FROM farmers_market.customer_purchases GROUP BY customer_id, market_date ORDER BY customer_id, market_date ) select cp.customer_id, cp.market_date, (SELECT COUNT(market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date AND DATEDIFF(cp.market_date, cma.market_date) <= 30) AS customer_markets_attended_30days_count FROM farmers_market.customer_purchases AS cp GROUP BY cp.customer_id, cp.market_date ORDER BY cp.customer_id, cp.market_date 

##### **Feature Engineering** 

This process of creating different input values that might be helpful to the prediction algorithm is called _feature engineering_ . Most binary classification algorithms require numeric inputs, so sometimes features are engineered to convert another data type into a numeric representation. Other types of features you might create include sets of one- hot encoded flag columns (as mentioned in Chapter 4, “CASE Statements”), converting categorical text columns to numeric values, aggregate 

**186 Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

high or low metrics (such as the maximum ever spent by the customer at a market to- date), other incrementing totals (such as the length of time the person has been a customer of the market), and other summaries for different time periods. 

One important factor when engineering features is that each of these feature values is only what would be knowable as of the date represented by the row— the market_date in this case. We want to train the model on examples of customers with a variety of traits as of specific points in time that can be correlated with a specific outcome or target variable relative to that time. In fact, I’ve been outputting the market_date in each of the previous queries for verification purposes, but I wouldn’t input the full date into a predictive model, because then the training data would all be tied to past dates, when only the relative dates for the events of interest (the time between purchases) are important. If we ran a current customer’s record through the model to try to make a prediction based on data collected this week, but the model had been trained on full date values from the past, the model wouldn’t know what to do with the market_date, because there will have been no training examples with similar dates. So, when I train my classification model using this dataset, I will not input the customer_id or market_date into the algorithm. I will only use them as unique identifiers, or index values, so the predictions the model outputs can be tied back to their respective rows. 

However, the month of the market date is likely predictive, because the market closes for the months of January and February. So, customers shopping in December would have a lower likelihood of returning in the next 30 days than customers in other months. The final version of this example classification dataset query will include a column representing the month, which can be seen in Figures 12.6 and 12.7. The number of columns is too wide to fit into one figure, so the output is split into two figures, with the customer_id and market_date index visible in both sections so you can find the continuation of each row in the second block: 

###### WITH 

customer_markets_attended AS ( SELECT customer_id, market_date, 

ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY market_date) AS market_count 

FROM farmers_market.customer_purchases GROUP BY customer_id, market_date ORDER BY customer_id, market_date ) 

**Chapter 12** ■ **Creating Machine Learning Datasets Using SQL 187** 

SELECT cp.customer_id, cp.market_date, EXTRACT(MONTH FROM cp.market_date) as market_month, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS purchase_total, COUNT(DISTINCT cp.vendor_id) AS vendors_patronized, MAX(CASE WHEN cp.vendor_id = 7 THEN 1 ELSE 0 END) purchased_from_ vendor_7, MAX(CASE WHEN cp.vendor_id = 8 THEN 1 ELSE 0 END) purchased_from_ vendor_8, COUNT(DISTINCT cp.product_id) AS different_products_purchased, DATEDIFF(cp.market_date, (SELECT MAX(cma.market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date GROUP BY cma.customer_id) ) days_since_last_customer_market_date, (SELECT MAX(market_count) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date <= cp.market_date) AS customer_markets_ attended_count, (SELECT COUNT(market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date AND DATEDIFF(cp.market_date, cma.market_date) <= 30) AS customer_markets_attended_30days_count, CASE WHEN DATEDIFF( (SELECT MIN(cma.market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date > cp.market_date GROUP BY cma.customer_id), cp.market_date) <=30 THEN 1 ELSE 0 END AS purchased_again_within_30_days FROM farmers_market.customer_purchases AS cp GROUP BY cp.customer_id, cp.market_date ORDER BY cp.customer_id, cp.market_date 

|| customer_i<br>|d<br>market_date<br>|market_month<br>|purchase_total<br>vendors_patronized<br><br>|purchased_from_vendor_7<br>|purchased_from_vendor_8<br>|different_products_purchased<br>|
|---|---|---|---|---|---|---|
|25<br>|2019-12-04<br>|12<br>|179.5000<br>1<br><br>|@<br>|1<br>|2<br>|
|25<br>|2019-12-14<br>|12<br>|36.0000<br>1<br><br>|@<br>|1<br>|1<br>|
|25<br>|2019-12-18<br>|12<br>|6.5000<br>1<br><br>|e<br>|1<br>|1<br>|
|25<br>|2028-25-06<br>|5<br>|36.0000<br>1<br><br>|@<br>|1<br>|1<br>|
|25<br>|2020-05-16<br>|5<br>|58.5000<br>+<br><br>|e<br>|1<br>|1<br>|
|25<br>|2028-85-23<br>|5<br>|49.0000<br>1<br><br>|@<br>|1<br>|2<br>|
|25<br>|2020-06-13<br>|6<br>|92.0000<br>2<br><br>|e<br>|1<br>|2<br>|
|25|2020-06-27|6|1.5000<br>1|@|e|1|
|25|2020-07-01|7|12.0171<br>2|I|e|2|
|25|2020-87-22|7|21.9735<br>2|Z|e|if|
|25<br>|2020-08-22<br>|8<br>|7.3124<br>2<br><br>|1<br>|e<br>|2<br>|
|25|2020-08-26|8|45.5000<br>1|C)|1|1|
|25|2028-89-85|9|31.4735<br>rd|ZL|e|3|
|25|2028-89-19|9|1€.4151<br>1|1|e|1|
|25|2028-18-83|108|39.0808<br>1|e|1<br>|5||





<!-- Start of picture text -->
customer_id market_date days_since_last_customer_market_date customer_markets_attended_count  customer_markets_attended_3@days_count purchased_again_within_3@_days<br>25 2019-12-04 4 30 3 1<br>25 2019-12-14 18 31 = zx<br>25 2019-12-18 4 32 4 e<br>25 2020-05-26 148 33 e 1<br>25 2020-05-16 10 34 1 1<br>25 2020-05-23 7 35 2 1<br>25 2020-06-13 21 36 2 a<br>25 2020-06-27 14 37 1 1<br>25 2020-07-01 4 38 2 1<br>25 2020-07-22 21 39 ri e<br>25 2020-08-22 31 40 e 1<br>25 2020-08-26 4 41 “i 1<br>25 2020-09-85 10 42 2 1<br>25 2020-09-19 14 43 3 1<br>25 2020-10-03 14 44 2 e<br><!-- End of picture text -->

**Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

**189** 

#### **Taking Things to the Next Level** 

In this chapter, we have built datasets that could be used as inputs to train time series models and binary classification models. Sometimes you will be joining in data from additional tables to add columns to your dataset, and you’ll have to be careful not to change the granularity as you do so. In this case, we engineered features using only data in the customer_purchases table in the Farmer’s Market database, aggregating data from the same table in many ways. You can use the SQL you have learned in this book to engineer a wide variety of features, improving your model by providing it with many different signals to correlate with the target variable. 

Some people do feature engineering in their model- building script or other software. Tools like the pandas package in Python do make certain types of feature engineering straightforward to include in your machine learning script. Benefits of conducting some feature engineering in the SQL code as a separate step in your data pipeline include the ability to easily store your results in a database table to use repeatedly during training (without having to regenerate the calculated columns each time your script is run) or to share with others. Additionally, some types of summarization are more efficient to do in SQL at the point of data extraction from the database than in other coding environments. If you need it to run more quickly, you could ask an experienced data engineer to help make your SQL more computationally efficient, once you have it returning the results you want. Now that you know how to build your own dataset, you can provide them with a query that generates the results you need instead of having to explain the granularity and define every column. And you don’t have to rely on a data engineer to simply add a column to an existing dataset, since you can now read SQL that someone else has developed and modify it yourself. 

The next step after building the dataset will be conducting Exploratory Data Analysis (EDA) on it to better understand the relationship between your input features and the target variable. Then you will go through a training and testing process with the portion of the dataset that contains known outcomes from the past. Once your model is trained, you can feed in current data summarized using the same query, but without values in the target variable column, and have it predict what those values will be. Then, after evaluating your model’s performance, you’ll likely be right back here engineering more features or joining in more data in order to improve your model’s predictions! 

#### **Exercises** 

1. Add a column to the final query in the chapter that counts how many markets were attended by each customer in the past 14 days. 

**190 Chapter 12** ■ **Creating Machine Learning Datasets Using SQL** 

2. Add a column to the final query in the chapter that contains a 1 if the customer purchased an item that cost over $10, and a 0 if not. HINT: The calculation will follow the same form as the purchased_from_vendor_x flags. 

3. Let’s say that the farmer’s market started a customer reward program that gave customers a market goods gift basket and branded reusable market bag when they had spent at least $200 total. Create a flag field (with a 1 or 0) that indicates whether the customer has reached this loyal customer status. HINT: One way to accomplish this involves modifying the CTE (WITH clause) to include purchase totals, and adding a column to the main query with a similar structure to the one that calculates customer_markets_attended_count, to calculate a running total spent. 

###### **<mark>C H A P T E R</mark>** 

# **13** 

## **Analytical Dataset Development Examples** 

In this chapter, I will walk through the development of datasets for answering different types of analytical questions. This involves combining multiple concepts from previous chapters into more complex queries and therefore is more advanced. Note that the example database doesn’t currently contain enough data with correlations for actually doing the analyses that would follow the dataset development, so we won’t be looking for trends in the output screenshots. The focus here is on how I would go about designing and building a dataset from our Farmer’s Market database using SQL to answer each of the following analytical questions: 

- What factors correlate with fresh produce sales? 

- How do sales vary by customer zip code, market distance, and demographic data? 

- How does product price distribution affect market sales? 

#### **What Factors Correlate with Fresh Produce Sales?** 

Let’s say we’re asked the analytical question “What factors are correlated with sales of fresh produce at the farmer’s market?” So what we’re being asked is to determine the relationships between a selection of different variables and a 

**191** 

|product_category_id|product_category_name|
|---|---|
|1|Fresh Fruits & Vegetables|
|2|Packaged Pantry Goods|
|3|Packaged Prepared Food|
|4|Freshly Prepared Food|
|5|Plants &<br>Flowers|
|6|Eggs & Meat<br>(Fresh or Frozen)|
|7|Non-Edible<br>Products|



|| product_id|product_name|product_size|product_category_id|product_qty_type|
|---|---|---|---|---|
|:|Habanero Peppers<br>- Organic|medium|1|lbs|
|2|Jalapeno Peppers<br>- Organic|small|1|lbs|
|3|Poblano Peppers<br>- Organic|large|1|unit|
|9|Sweet Potatoes|medium|1|lbs|
|12|Baby Salad Lettuce Mix<br>...|1/2 1b|1|unit|
|13|Baby Salad Lettuce Mix|1 1b|1|lbs|
|14|Red<br>Potatoes||i||
|15|Red Potatoes<br>-<br>Small||1||
|16|Sweet Corn|Ear|1|unit|
|17|Carrots|sold by weight|1|lbs|
|18|Carrots<br>- Organic|bunch|1|unit|
|21|Organic Cherry Tomatoes|pint|1|unit|
|22|Roma Tomatoes|medium|1|lbs|
|6|Cut Zinnias Bouquet|medium|5|unit|
|1¢é|Eggs|1 dozen|6|unit|
|11|Pork Chops|1 1b|6|lbs|



**194 Chapter 13** ■ **Analytical Dataset Development Examples** 

SELECT * FROM customer_purchases cp INNER JOIN product p ON cp.product_id = p.product_id WHERE p.product_category_id = 1 

I used an INNER JOIN instead of a LEFT JOIN, because for this sales calculation, I’m not interested in products that don’t have purchases. At this stage, it’s good to check the count of rows returned, to ensure it makes sense given your join selection. I also look at the details, to make sure I’m pulling the right data from the tables I meant to pull from, that I’m joining on the correct fields, and that my results are filtered the way I expect. 

Since I’ll be summarizing by week, I don’t need the transaction_time field, and I don’t currently have a need to know about the size of each product. We might eventually need the product quantity type and vendor information for when we start adding up how much product is available for purchase. However, do we need those fields from these tables? Total sales is the dependent variable— the value we’re trying to correlate different values with. If we wanted to get a count of vendors who had the product for sale, we don’t want to get that from the customer_purchases table, because there could be products available for sale that no one purchased, which means their existence wouldn’t be recorded in the customer_purchases table. So, we’ll want to get those pieces of data from the vendor_inventory table at a later step, and not from the customer_purchases table. 

I can join in the market_date_info table to get the week number, to make summarization easier, as well as other date- related information such as the season and the weather. I decided to RIGHT JOIN it to the other tables, because I want to know whether there are market dates with no fresh produce sales at all, and the RIGHT JOIN will still pull in market dates with no corresponding records in the customer_purchases table, as shown in Figure 13.4: 

SELECT 

cp.market_date, cp.customer_id, cp.quantity, cp.cost_to_customer_per_qty, p.product_category_id, mdi.market_date, mdi.market_week, mdi.market_year, mdi.market_rain_flag, mdi.market_snow_flag FROM customer_purchases cp INNER JOIN product p ON cp.product_id = p.product_id RIGHT JOIN market_date_info mdi ON mdi.market_date = cp.market_date WHERE p.product_category_id = 1 



<!-- Start of picture text -->
Prodect_id vender_id market_date customer_ic quantity cost_to_custower_per. trantaction_tive procuct_ic product_nene Product_siz product_categor produrt_aty_ty<br>16 ‘ 2019-07-13 13 2.00 °.90 12:as:e@ 16 Sweet Corn tor a weit<br>“ 4 2019-87-13 23 2.08 e538 18:40:08 16 Sweet Corn fer 1 wed<br>16 4 2019-67-13 26 5.00 @.se 12:23:08 16 Sweet Corn far 1 unit<br>1 ? 2019-07-17 4 3.03 6.99 1844;00 1 Mabarero Peppers - Organic medive 1 les<br>2 ? 2019-07-17 5 4.32 6.9 16:30:68 1 habanero Peppers - Organic mediue 2 ats<br>2 7 2019-07-17 1 4.08 3.49 18:26:00 2 Jalepeno Peppers - Orgenic saell 1 ibs<br>2 ? 2019-67-17 4 1.55 3.40 17:45:60 2 Jalaperc Peppers - Organic seal 2 ies<br>2 7 2019-07-17 7 4.33 3.49 18:51:68 2 Jalapeno Peppers - Organic seal) 2 its<br>2 ? 2€19-67-17 9 @.12 3.49 1644200 2 Jalapeno Peppers - Organic seall 1 les<br>2 ? 2019-07-17 13 3.08 3.49 17:28:60 2 Jalapeno Peppers - Organic small 1 les<br>2 ? 2019-07-17 22 2.56 3.49 18:32:60 2 Jalapere Peppers - Organic seall 2 ies<br>3 7 2019-@7-17 2 3.08 e.0 15:45:00 a Poblenc Peppers - Organic lerge 1 weit<br>3 ? 2019-67-17 2 1.00 e.8 18:56:68 3 Poblenc Peppers - Organic lerge i wrdt<br>3 7 2019-07-17 5S 4.00 e.38 18:45:08 3 Poblanc Peppers - Organic lerge 1 weit<br>3 ? 2019-@7-17 8 5.00 0.0 16:08:€0 3 Poblane Peppers - Organic large 1 unit<br>3 7 2019-07-17 4 5.00 o.0 17247:60 ’ Poblene Peppers - Organic lerge 2 writ<br><!-- End of picture text -->



<!-- Start of picture text -->
2019-06-29 2 4.08 @.50 b 2019-06-29 26 2019 e @<br>2019-06-29 = 10.08 @.45 1 2019-06-29 26 2019 e e<br>2019-06-29 4 8.08 @.45 1 2019-86-29 26 2019 e e<br>2019-06-29 5 5.08 @.58 1 2019-06-29 26 2019 e e<br>2019-06-29 6 5.08 @.58 1 2019-06-29 26 2019 e e<br>2019-06-29 19 5.08 @.58 1 2019-@6-29 26 2019 @ @<br>2019-06-29 25 2.08 @.58 1 2019-06-29 26 2019 e @<br>2019-07-@3 14 @.99 6.99 b 2019-07-83 27 2019 @ @<br>2019-07-83 14 2.18 6.99 1 2019-87-83 27 2019 @ @<br>2019-07-83 41s 1.53 6.99 1 2019-07-03 27 2019 @ @<br>2019-07-83 16 2.02 6.99 1 2019-07-83 27 2019 @ @<br>2019-07-83 22 0.66 6.99 1 2019-87-83 27 2019 e @<br>2019-07-83 4 3.73 3.49 | 2019-87-83 27 2019 e e<br>2019-07-83 9 4.85 3.49 1 2019-87-83 27 2019 e @<br>2019-07-83 12 @.12 3.49 1 2019-87-03 27 2019 e e<br>2019-07-83 16 3.46 3.49 1 2019-87-83 27 2019 @ @<br>2019-07-83 17 1.76 3.49 az 2019-87-03 27 2019 @ e<br><!-- End of picture text -->

|2019-06-29|2|4.08|@.50|b|2019-06-29|26|2019|e|@|
|---|---|---|---|---|---|---|---|---|---|
|2019-06-29|=|10.08|@.45|1|2019-06-29|26|2019|e|e|
|2019-06-29|4|8.08|@.45|1|2019-86-29|26|2019|e|e|
|2019-06-29|5|5.08|@.58|1|2019-06-29|26|2019|e|e|
|2019-06-29|6|5.08|@.58|1|2019-06-29|26|2019|e|e|
|2019-06-29|19|5.08|@.58|1|2019-@6-29|26|2019|@|@|
|2019-06-29|25|2.08|@.58|1|2019-06-29|26|2019|e|@|
|2019-07-@3|14|@.99|6.99|b|2019-07-83|27|2019|@|@|
|2019-07-83|14|2.18|6.99|1|2019-87-83|27|2019|@|@|
|2019-07-83|41s|1.53|6.99|1|2019-07-03|27|2019|@|@|
|2019-07-83|16|2.02|6.99|1|2019-07-83|27|2019|@|@|
|2019-07-83|22|0.66|6.99|1|2019-87-83|27|2019|e|@|
|2019-07-83|4|3.73|3.49|||2019-87-83|27|2019|e|e|
|2019-07-83|9|4.85|3.49|1|2019-87-83|27|2019|e|@|
|2019-07-83|12|@.12|3.49|1|2019-87-03|27|2019|e|e|
|2019-07-83<br>|16<br>|3.46<br>|3.49<br>|1<br>|2019-87-83<br>|27<br>|2019<br>|@<br>|@<br>|
|2019-07-83|17|1.76|3.49|az|2019-87-03|27|2019|@|e|



**Chapter 13** ■ **Analytical Dataset Development Examples 197** 

But look what happened. Even though I’m right joining the market_date_info table to the customer_purchases table, I’m not seeing any market dates that don’t have sales in this category, even though I know they exist in the data! This is a common SQL design error. You might think that the solution is to rearrange all of the joins, but if that’s the only change you make, you will still have the same issue. What’s happening is that our WHERE clause is filtering the results to only rows with a customer purchase from product category 1. So if there are no sales on a market date, there are no product categories associated with that date, so we are filtering it out, defeating the purpose of the RIGHT JOIN. (This is also a good reason to look at the data in each table before joining and write some quality control queries such as distinct counts of market dates, so you are aware if some expected values are missing after you join the tables together.) 

The solution to this filter issue is to put the product category filter in the JOIN ON clause instead of in the WHERE clause, which is something we haven’t covered previously. I can join to the product table on the product_id and product_category_id fields, and filter the product_category_id in the ON clause. This makes the filter only apply to the data from the product table (and now the customer_purchases table, since they’re inner joined), and not to the results set, the way the WHERE clause does. So now all of our market dates will be returned. I moved the market_date_info fields to appear first, and modified the join to include the filter. You can now see that we’re joining on the product_id and filtering the product_category_id in the ON section of the JOIN. Note that now there is no WHERE clause, but we are still filtering the results of one of the tables being joined into the dataset! The output of this query is displayed in Figure 13.5: 

###### SELECT 

mdi.market_date, mdi.market_week, mdi.market_year, mdi.market_rain_flag, mdi.market_snow_flag, cp.market_date, cp.customer_id, cp.quantity, cp.cost_to_customer_per_qty, p.product_category_id FROM customer_purchases cp INNER JOIN product p ON cp.product_id = p.product_id AND p.product_category_id = 1 RIGHT JOIN market_date_info mdi ON mdi.market_date = cp.market_date 

|market_date<br>|market_week<br>|market_year<br>|market_rain_flag<br>|market_snow_flag<br>|market_date<br>|custome<br>|r_id<br>quantit<br>|y<br>cost_to_customer_per_aty<br>|product_category_id<br>|
|---|---|---|---|---|---|---|---|---|---|
|2019-09-28<br>|39<br>|2019<br>|e<br>|@<br>|2019-09-28<br>|7<br>|3.00<br>|@.50<br>|1<br>|
||2019-@9-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|8<br>|3.00<br>|@.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|9<br>|5.08<br>|@.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|12<br>|3.00<br>|@.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|18<br>|5.00<br>|@.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|19<br>|8.00<br>|2.50<br>|1<br>|
|2019-09-28|39|2019|e|e|2019-09-28|21|3.00|@.50|1|
||2@19-e9-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|4<br>|10.00<br>|0.45<br>|1<br>|
||2@19-@9-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|14<br>|5.00<br>|@.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|14<br>|4.00<br>|2.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br>|e<br>|2019-09-28<br>|15<br>|1.00<br>|@.50<br>|1<br>|
|2019-09-28<br>|39<br>|2019<br>|e<br><br>|e<br>|2019-09-28|20|4.00|2.50<br>|1|
|2019-10-02<br>|40<br>|2019<br>|C)<br><br>|C)<br>||||ons||
|2019-10-05<br>|40<br>|2019<br>|e<br>|e<br>||Losiad<br>|os<br>|||
|2019-10-@9|41|2019|e|e|=|=|=|=||
|2019-10-12<br>|41<br>|2019<br>|e<br>|e<br>||||||
|2019-10-16|42|2019|e|e||||Lal||



**Chapter 13** ■ **Analytical Dataset Development Examples 199** 

Now we can see rows for market dates with no fresh produce purchases. I can summarize the customer purchases to one row per week to get sales per week by grouping on market_year and market_week, and we don’t need most of the other columns with additional details about the purchases, so we can remove them from our query. The sales calculation is the same one we used in Chapter 12, “Creating Machine Learning Datasets Using SQL,” with a slight addition. COALESCE is a function that returns the first non- NULL value in a list of values. In this case, when the query returns a market date with no sales in product category 1, the weekly_category1_sales value would be NULL. If we want it to be 0 instead, we can use the syntax 

###### COALESCE([value 1], 0) 

which will return a 0 if “value 1” is NULL, and will otherwise return the calculated value. We wrap our SUM function in this COALESCE function, then ROUND the result of the COALESCE function to two digits after the decimal point. To summarize, in that final line before the FROM clause, we’re adding up the sales, converting the result to 0 if there are no sales, then rounding the numeric result to two digits. 

I’m also returning the MAX of the snow and rain flags, because if there was precipitation at either of the markets during the week, I want to return a 1 in this field. And I returned the minimum market_season value, so only one value is returned if a week happens to be split across two seasons. The updated result using the following query is displayed in Figure 13.6: 

###### SELECT 

mdi.market_year, mdi.market_week, MAX(mdi.market_rain_flag) AS market_week_rain_flag, MAX(mdi.market_snow_flag) AS market_week_snow_flag, MIN(mdi.market_min_temp) AS minimum_temperature, MAX(mdi.market_max_temp) AS maximum_temperature, MIN(mdi.market_season) AS market_season, ROUND(COALESCE(SUM(cp.quantity * cp.cost_to_customer_per_qty), 0), 2) AS weekly_category1_sales FROM customer_purchases cp INNER JOIN product p ON cp.product_id = p.product_id AND p.product_category_id = 1 RIGHT JOIN market_date_info mdi ON mdi.market_date = cp.market_date GROUP BY mdi.market_year, mdi.market_week 



<!-- Start of picture text -->
market_year market_week market_week_rain_flag market_week_snow_flag minimum_temperature maximum_temperature market_season weekly_categoryl_sales<br>2019 22 e @ 49 69 Spring 8.68<br>2@19 23 @ @ 57 82 Summer/Early Fall 42.5@<br>2@19 24 @ @ 56 82 Summer/Early Fall 47.2@<br>2019 25 @ @ 65 8e Summer/Early Fall 41.20<br>2019 26 @ e 72 85 Summer/Early Fall 55.78<br>2019 27 @ @ 67 89 Summer/Early Fall 287.38<br>2019 28 ) @ 65 98 Summer/Early Fall 266.09<br><!-- End of picture text -->

**Chapter 13** ■ **Analytical Dataset Development Examples 201** 

So now we have total sales by week. 

Some of the other aggregate values that could be added to this dataset include the number of vendors carrying products in the category, the volume of inventory available for purchase, and special high- demand product seasonal availability. These are values that come from the vendor_inventory table, because I want to know what the vendors brought to market, regardless of whether people purchased the items. 

We can set up the query for vendor_inventory just like we did for customer_purchases, joining it to the product and market_date_info tables the same way, and filtering to product_category_id = 1 in the JOIN statement as we did previously. The results of this query are shown in Figure 13.7: 

###### SELECT 

mdi.market_date, mdi.market_year, mdi.market_week, vi.*, p.* FROM vendor_inventory vi INNER JOIN product p ON vi.product_id = p.product_id AND p.product_category_id = 1 RIGHT JOIN market_date_info mdi ON mdi.market_date = vi.market_date 

Removing the fields we don’t need for our weekly summary, we can narrow down the vendor_inventory table to keep the features we need for calculating the number of vendors (vendor_id), the number of products (product_id), and volume of products (quantity). We can also use the product_id to flag the existence of certain products. Let’s say that we suspect that when the sweet corn vendors are at the market, some customers come that don’t come at any other time of year, just to get the locally famous corn on the cob. We want to know if overall fresh produce sales go up during the weeks when corn is available, so we’ll create a product availability flag for product 16, sweet corn, called corn_available_flag, as shown in the following query and in Figure 13.8: 

###### SELECT 

mdi.market_year, mdi.market_week, COUNT(DISTINCT vi.vendor_id) AS vendor_count, COUNT(DISTINCT vi.product_id) AS unique_product_count, 

SUM(CASE WHEN p.product_qty_type = 'unit' THEN vi.quantity ELSE 0 END) AS unit_products_qty, 

SUM(CASE WHEN p.product_qty_type = 'lbs' THEN vi.quantity ELSE 0 END) AS bulk_products_lbs, 

ROUND(COALESCE(SUM(vi.quantity * vi.original_price), 0), 2) AS total_product_value, 

_Continues_ 

**202 Chapter 13** ■ **Analytical Dataset Development Examples** 

###### _(continued)_ 

MAX(CASE WHEN p.product_id = 16 THEN 1 ELSE 0 END) AS corn_available_flag FROM vendor_inventory vi INNER JOIN product p ON vi.product_id = p.product_id RIGHT JOIN market_date_info mdi ON mdi.market_date = vi.market_date GROUP BY mdi.market_year, mdi.market_week 

Now that I see these results, I realize that I would like to have a count of vendors selling and products available at the entire market, in addition to the product availability for product category 1. To avoid developing another query that will need to be joined in, I will remove the product_category_id filter and use CASE statements to create a set of fields that provides the same metrics, but only for products in the category. Then, the existing fields will turn into a count for all vendors and products at the market: 

SELECT mdi.market_year, mdi.market_week, COUNT(DISTINCT vi.vendor_id) AS vendor_count, COUNT(DISTINCT CASE WHEN p.product_category_id = 1 THEN vi.vendor_id ELSE NULL END) AS vendor_count_product_category1, COUNT(DISTINCT vi.product_id) AS unique_product_count, COUNT(DISTINCT CASE WHEN p.product_category_id = 1 THEN vi.product_id ELSE NULL END) AS unique_product_count_product_category1, SUM(CASE WHEN p.product_qty_type = 'unit' THEN vi.quantity ELSE 0 END) AS unit_products_qty, SUM(CASE WHEN p.product_category_id = 1 AND p.product_qty_type = 'unit' THEN vi.quantity ELSE 0 END) AS unit_products_qty_product_category1, SUM(CASE WHEN p.product_qty_type  = 'lbs' THEN vi.quantity ELSE 0 END) AS bulk_products_lbs, SUM(CASE WHEN p.product_category_id = 1 AND p.product_qty_type  = 'lbs' THEN vi.quantity ELSE 0 END) AS bulk_products_lbs_product_category1, ROUND(COALESCE(SUM(vi.quantity * vi.original_price), 0), 2) AS total_ product_value, ROUND(COALESCE(SUM(CASE WHEN p.product_category_id = 1 THEN vi.quantity * vi.original_price ELSE 0 END), 0), 2) AS total_product_value_product_ category1, MAX(CASE WHEN p.product_id = 16 THEN 1 ELSE 0 END) AS corn_available_ flag FROM vendor_inventory vi INNER JOIN product p ON vi.product_id = p.product_id RIGHT JOIN market_date_info mdi ON mdi.market_date = vi.market_date GROUP BY mdi.market_year, mdi.market_week 



<!-- Start of picture text -->
marketcate market_year market_week market.cate quantity vendor_id product.i¢ original_erice product.ic product_nase product_size procuct_categor) product_aty_type<br>2039-06-08 2019 2 2019-06-08 «100.004 u“ °.0 “ Sweet Corn ter 2 unit<br>2029-06-12 2019 ™ 2019-06-12 120.004 ctf 0.50 pty Sweet Corn for 2 unit<br>2019-€6-15 2019 coy 2019-06-25 140.004 16 0.50 16 Sweet Corn for x unit<br>2019-06-19 2019 2 2019-06-19 120.00 6 0.50 ty Sweet Corn fer 1 unit<br>2029-06-22 2019 = 2019-06-22 120.004 “ 0. oo Sweet Corn ter 2 voit<br>2019-06-26 2019 26 2019-06-26 140.084 16 0.58 pc Sweet Corn ter 2 unit<br>2019-€6-29 2019 2 2019-06-29 108.024 a6 ese pty Sweet Corn ter a unit<br>2019-€7-05 ©2019 2 2019-07-03 7.38 7 a 6.99 a mapanerc Peppers... seciue a aps<br>2019-47-03 2019 2 2019-87-03 33.63 7 2 3.40 2 Jalapenc Peppers... small 2 ios<br>2019-€7-23 «2019 2 2019-07-03 78.08 = 7 3 0.58 3 Poblano Pespers ... large 1 unit<br>2019-€7-83 ©2019 2 2019-07-03 300.08 4 1“ 0. pt Sweet Corn ter 1 unit<br>2019-47-06 = 2019 2 2019-07-06 = 18.96 7 i 6.9 a Habanero Peppers... sediue a lbs<br>2019-€7-05 ©2019 2 2019-07-06 «= 24.56 7 2 3.49 2 Jalapeno Peppers... small a los<br>2019-€7-06 © 2019 2 2019-07-06 78.08 = 7 3 0.58 3 Poblano Peppers ... large pA unit<br>2019-€7-06 ©2019 2 2019-07-06 = 200.004 16 ese 16 Sweet Corn ter 1 unit<br>2019-€7-10 = 2019 2 2019-07-10 = 13.08 7 i 6.9 1 Habanero Peppers... sediue i los<br>2019-€7-18 = 2019 2 2019-07-18 = 28.83 7 2 3.49 2 Jalapeno Peppers... small a los<br>2019-€7-18 © 2019 2 2019-67-10 68.007 3 0.58 3 Poblano Peppers ... large 1 unit<br>2019-€7-10 = 2019 2B 2019-07-10 300.004 16 0.80 6 Sweet Corn ter 1 unit<br>2019-€7-13 2019 2 2019-07-13 18.22 7 i 6.9 1 Habanero Peppers... sediue a los<br>1019-87 - ut 7 1019-07- 5 no Peopers Ds<br><!-- End of picture text -->



<!-- Start of picture text -->
market_year market_week vei uni unit_p bulk_p total_product_value corn_available_flag<br>2019 _ 25 E 5 | 386.ee @ 08 7 1202 ° 50 _ 4 |<br>2619 26 + & 388.08 8.80 1165.56 1<br>2019 27 3.06C«8 778.0@ 76.53 1660.78 a I<br>2019 28 3. (68 821.0@ 81.3@ 1708.79 1<br>2019 29 - 882.0@ 77.83 1849.83 1<br>2019 38 3 8 785.0@ 74.55 1742.15 1<br>2019 31 3.06C«° 611.00 84.05 1651.16 x<br>2019 32 aS 836.0@ 74.17 1702.34 1<br>2019 33 3.6C«8 764.00 77.44 1645.@5 1<br>2019 34 a & 754.0@ 67.73 1663.85 1<br>2019 35 oe -s 856.0@ 78.81 1802.72 1<br>2019 36 a. @ 524.0@ 88.54 1692.50 3<br>2019 37 3.6C«s 522.00 67.76 1540.54 1<br>2019 38 3. 68 514.00 79.1@ 1616.82 1<br>2019 39 3.06C«°8 538.00 78.46 1702.23 x |<br>2019 48 2 4 139.00 6.00 1062.08 e<br>2019 41 2 4 158.00 8.80 1897.80 @<br>2019 42 2 #4 138.00 6.00 1692.08 @<br>2019 43 2 #4 149.08 8.00 1067.58 @<br>2019 44 2 #4 143.00 8.00 1848.08 e<br>2019 45 2 4 145.00 8.00 1876.80 @<br><!-- End of picture text -->

|market_year <br><br>|market_week<br><br>|ve<br>|i<br>uni<br><br>|unit_p<br>|bulk_p <br>|total_product_value<br> <br><br>|corn_available_flag<br><br>|
|---|---|---|---|---|---|---|---|
|2019 _<br>2|5<br>||5<br>||386.ee|@0871|202 °50<br>_<br>|4<br>||
|2619|26|+|&|388.08|8.80|1165.56|1|
|2019|27|3.0|6C«8|778.0@|76.53|1660.78|aI|
|2019|28|3.|(68|821.0@|81.3@|1708.79|1|
|2019|29|-||882.0@|77.83|1849.83|1|
|2019|38|3|8|785.0@|74.55|1742.15|1|
|2019|31|3.06C«°||611.00|84.05|1651.16|x|
|2019|32|aS||836.0@|74.17|1702.34|1|
|2019|33|3.6|C«8|764.00|77.44|1645.@5|1|
|2019|34|a|&|754.0@|67.73|1663.85|1|
|2019|35|oe|-s|856.0@|78.81|1802.72|1|
|2019|36|a.|@|524.0@|88.54|1692.50|3|
|2019|37|3.6|C«s|522.00|67.76|1540.54|1|
|2019|38|3.|68|514.00|79.1@|1616.82|1|
|2019|39|3.06|C«°8|538.00|78.46|1702.23|x ||
|2019|48|2|4|139.00|6.00|1062.08|e|
|2019|41|2|4|158.00|8.80|1897.80|@|
|2019|42|2|#4|138.00|6.00|1692.08|@|
|2019|43|2|#4|149.08|8.00|1067.58|@|
|2019<br>|44|2|#4|143.00|8.00|1848.08|e|
|2019|45|2|4|145.00|8.00|1876.80|@|



**Chapter 13** ■ **Analytical Dataset Development Examples 205** 

ON cp.product_id = p.product_id AND p.product_category_id = 1 RIGHT JOIN market_date_info mdi ON mdi.market_date = cp.market_date GROUP BY mdi.market_year, mdi.market_week ), my_vendor_inventory AS ( SELECT mdi.market_year, mdi.market_week, COUNT(DISTINCT vi.vendor_id) AS vendor_count, 

COUNT(DISTINCT CASE WHEN p.product_category_id = 1 THEN vi.vendor_id ELSE NULL END) AS vendor_count_product_category1, 

COUNT(DISTINCT vi.product_id) unique_product_count, COUNT(DISTINCT CASE WHEN p.product_category_id = 1 THEN vi.product_id ELSE NULL END) AS unique_product_count_product_category1, 

SUM(CASE WHEN p.product_qty_type = 'unit' THEN vi.quantity ELSE 0 END) AS unit_products_qty, 

SUM(CASE WHEN p.product_category_id = 1 AND p.product_qty_type = 'unit' THEN vi.quantity ELSE 0 END) AS unit_products_qty_product_category1, SUM(CASE WHEN p.product_qty_type <> 'unit' THEN vi.quantity ELSE 0 END) AS bulk_products_qty, 

SUM(CASE WHEN p.product_category_id = 1 AND p.product_qty_type <> 'unit' THEN vi.quantity ELSE 0 END) AS bulk_products_qty_product_category1, ROUND(COALESCE(SUM(vi.quantity * vi.original_price), 0), 2) AS total_product_value, 

ROUND(COALESCE(SUM(CASE WHEN p.product_category_id = 1 THEN vi.quantity * vi.original_price ELSE 0 END), 0), 2) AS total_product_value_product_category1, MAX(CASE WHEN p.product_id = 16 THEN 1 ELSE 0 END) AS corn_available_flag FROM vendor_inventory vi INNER JOIN product p ON vi.product_id = p.product_id RIGHT JOIN market_date_info mdi ON mdi.market_date = vi.market_date GROUP BY mdi.market_year, mdi.market_week ) 

SELECT * FROM my_vendor_inventory LEFT JOIN my_customer_purchases ON my_vendor_inventory.market_year = my_customer_purchases.market_year AND my_vendor_inventory.market_week = my_customer_purchases.market_week ORDER BY my_vendor_inventory.market_year, my_vendor_inventory.market_week 



<!-- Start of picture text -->
market_year market_week vendor_count vendor_count_product_categoryl unique_product_count unique_product_count_product_category1<br>2019 25 3 1 s 1<br>2019 26 3 1 5 1<br>2019 27 3 2 8 4<br>2019 28 3 2 8 4<br>2019 29 =! 2 8 4<br>2019 38 3 2 8 4<br>2019 31 3 2 8 4<br>2019 32 3 2 8 4<br>2019 33 3 2 8 4<br>2019 34 3 2 8 4<br>2019 35 3 2 8 4<br>2019 36 3 2 8 4<br>2019 37 3 2 8 4<br>2019 38 3 2 8 4<br>2019 39 =! 2 8 4<br>2019 48 2 e 4 e<br>2019 41 2 e 4 e<br>2019 42 2 e@ 4 e<br>2019 43 2 @ 4 e<br>2019 44 2 e 4 e<br><!-- End of picture text -->

|market_y|ear<br>market_w|eek<br>vendor_count<br>vendor_count_pro|duct_categoryl<br>unique_product_count|unique_product_count_product_category1|
|---|---|---|---|---|
|2019|25|3<br>1|s|1|
|2019|26|3<br>1|5|1|
|2019|27|3<br>2|8|4|
|2019|28|3<br>2|8|4|
|2019|29|=!<br>2|8|4|
|2019|38|3<br>2|8|4|
|2019|31|3<br>2|8|4|
|2019|32|3<br>2|8|4|
|2019|33|3<br>2|8|4|
|2019|34|3<br>2|8|4|
|2019|35|3<br>2|8|4|
|2019|36|3<br>2|8|4|
|2019|37|3<br>2|8|4|
|2019|38|3<br>2|8|4|
|2019|39|=!<br>2|8|4|
|2019|48|2<br>e|4|e|
|2019|41|2<br>e|4|e|
|2019|42|2<br>e@|4|e|
|2019|43|2<br>@|4|e|
|2019|44|2<br>e|4|e|





<!-- Start of picture text -->
market_year market_week vei ver uni un unit_products_qty unit_products_qty_product_categoryl bulk_products_lbs bulk_products_lbs_product_category1<br>2019 25 3 1 5 1 386.00 248.08 @.00 0.08<br>2019 26 3 1 5 1 386.00 248.08 6.08 6.08<br>2019 27 3 2 8 4 778.00 640.00 76.53 76.53<br>2019 28 3 2 8 4 821.06 690.00 81.38 81.30<br>2019 29 3 2 8 4 882.00 730.08 77.83 77.83<br>2019 3@ 3 2 8 4 785.00 640.00 74.55 74.55<br>2019 31 3 2 8 4 811.06 680.00 84.85 84.05<br>2019 32 3 2 8 4 836.00 698.08 74.17 74.17<br>2019 33 3 2 8 4 764.00 630.00 77.44 77.44<br>2019 34 3.2 8 4 754.00 610.08 67.73 67.73<br>2019 35 3 2 8 4 856.00 710.00 78.81 78.81<br>2019 36 3 2 8 4 524.66 370.08 88.54 88.54<br>2019 37 3 2 8 4 522.00 388.08 67.76 67.76<br>2019 38 3 2 8 4 514.66 376.08 79.18 79.18<br>2019 39 3 2 8 4 538.00 390.08 78.46 78.46<br>2019 48 2 @ 4 @ 139.08 8.08 8.08 6.08<br>2019 41 2 8@ 4 @ 158.00 2.00 6.00 0.08<br>2019 42 2 @ 4 @ 138.00 2.00 @.08 0.08<br>2019 43 2 0@ 4 @ 149.00 2.08 e.00 0.08<br>2019 44 2 @ 4 @ 143.00 2.00 6.08 0.00<br><!-- End of picture text -->



<!-- Start of picture text -->
market_year market_week vei ver uni un unit_p unit_p bulk_p bulk_; total_product_value total_product_value_product_categoryl corn_available_flag<br>2019 25 3 1 5 1 386.00 248.00 8.00 @.0@ 1202.50 120.08 3<br>2019 26 3 1 5S 1 386.00 246.00 6.06 @.0@ 1165.56 120.06 1<br>2019 27 3 2 8 4 778.00 648.080 76.53 76.53 1660.78 651.28 1<br>2019 28 3 2 8 4 821.06 690.00 81.3@ 81.3@ 1708.79 710.29 1<br>2019 29 3 2 8 4 882.00 730.00 77.83 77.83 1849.83 705.33 1<br>2019 3@ 3 2 8 4 785.00 640.00 74.55 74.55 1742.15 641.15 1<br>2019 31 3 2 8 4 811.00 680.00 84.05 84.05 1651.16 710.16 a<br>2019 32 3 2 8 4 836.00 698.00 74.17 74.17 1762.34 665.84 1<br>2019 33 3 2 8 4 764.00 638.00 77.44 77.44 1645.05 65.05 1<br>2019 34 3 2 8 4 754.06 610.0@ 67.73 67.73 1663.85 605.85 1<br>2019 35 3 2 8 4 856.00 710.080 70.81 70.81 1802.72 660.72 1<br>2019 36 3 2 8 4 524.00 370.00 88.54 88.54 1692.5@ 569.50 1<br>2019 37 3 2 8 4 522.0@ 380.00 67.76 67.76 1540.54 493.54 1<br>2019 38 3 2 8 4 514.00 370.00 79.1@ 79.10 1616.82 535.82 1<br>2019 39 3 2 8 4 538.00 390.00 78.46 78.46 1702.23 524.23 1<br>2019 48 2 @ 4 @ 139.00 6.06 8.00 @.0@ 1062.00 6.08 e<br>2019 41 2 @ 4 @ 150.00 8.00 6.00 @.0@ 1097.00 8.00 e<br>2019 42 2 @ 4 @ 138.00 6.06 6.00 @.0@ 1092.00 0.00 e<br>2019 43 2 @ 4 @ 149.00 @.0@ 6.00 @.0@ 1067.50 0.00 e<br>2019 44 2 @ 4 @ 143.00 @.00 0.00 0.00 1040.00 0.00 e<br>2019 45 2 @ 4 @ 145.00 8.00 08.00 @.0@ 1076.00 8.00 e<br><!-- End of picture text -->

|market_y|ear<br>market_|week<br>vei<br>v|er uni un unit_p<br>unit_p|bulk_p|bulk_;|total_product_value|total_product_value_product_categoryl<br>corn_available_flag|
|---|---|---|---|---|---|---|---|
|2019|25|3<br>1|5<br>1<br>386.00248.00|8.00|@.0@|1202.50|120.08<br>3|
|2019|26|3<br>1|<br>5S<br>1<br>386.00 246.00|<br> 6.06|@.0@|1165.56|120.06<br>1|
|2019|27|3<br>2|8<br>4<br>778.00<br>648.080|76.53|76.53|1660.78|651.28<br>1|
|2019|28|3<br>2|8<br>4<br>821.06<br>690.00|81.3@|81.3@|1708.79|710.29<br>1|
|2019|29|3<br>2|8<br>4<br>882.00<br>730.00|77.83|77.83|1849.83|705.33<br>1|
|2019|3@|3<br>2|8<br>4<br>785.00 640.00|74.55|74.55|1742.15|641.15<br>1|
|2019|31|3<br>2|8<br>4<br>811.00<br>680.00|84.05|84.05|1651.16|710.16<br>a|
|2019|32|3<br>2|8<br>4<br>836.00 698.00|74.17|74.17|1762.34|665.84<br>1|
|2019|33|3<br>2|8<br>4<br>764.00<br>638.00|77.44|77.44|1645.05|65.05<br>1|
|2019|34|3<br>2|8<br>4<br>754.06610.0@|67.73|67.73|1663.85|605.85<br>1|
|2019|35|3<br>2|<br>8<br>4<br>856.00 710.080|<br> 70.81|70.81|1802.72|660.72<br>1|
|2019|36|3<br>2|8<br>4<br>524.00<br>370.00|88.54|88.54|1692.5@|569.50<br>1|
|2019|37|3<br>2|8<br>4<br>522.0@ 380.00|67.76|67.76|1540.54|493.54<br>1|
|2019|38|3<br>2|8<br>4<br>514.00<br>370.00|79.1@|79.10|1616.82|535.82<br>1|
|2019<br>|39<br>|3<br>2<br><br>|8<br>4<br>538.00<br>390.00<br><br><br>|78.46<br>|78.46<br>|1702.23<br>|524.23<br>1<br><br>|
|2019|48|2<br>@|4<br>@<br>139.00 6.06|8.00|@.0@|1062.00|6.08<br>e|
|2019<br>|41<br>|2<br>@<br><br>|4<br>@<br>150.00 8.00<br><br><br>|6.00<br>|@.0@<br>|1097.00<br>|8.00<br>e<br><br>|
|2019|42|2<br>@|4<br>@<br>138.006.06|6.00|@.0@|1092.00|0.00<br>e|
|2019<br>|43<br>|2<br>@<br><br>|<br>4<br>@<br>149.00 @.0@<br><br><br>|6.00<br>|@.0@<br>|1067.50<br>|0.00<br>e<br><br>|
|2019<br>|44<br>|2<br>@<br><br>|4<br>@<br>143.00 @.00<br><br><br>|0.00<br>|0.00<br>|1040.00<br>|0.00<br>e<br><br>|
|2019|45|2<br>@|4<br>@<br>145.008.00|08.00|@.0@|1076.00|8.00<br>e|



**Chapter 13** ■ **Analytical Dataset Development Examples 209** 

I can alter the final SELECT statement to include the prior week’s product category 1 sales, too, because the prior week’s sales might be a good indicator of what to expect this week. I can use the LAG window function that was introduced in Chapter 7, ”Window Functions and Subqueries.” And I’ll go ahead and list all of the column names to avoid showing the duplicate market_year and market_week columns that are in both CTEs which therefore show in the output twice when we use *. (This query should be preceded by the same CTE/WITH clause as the previous query, but removed here to save space.) 

SELECT mvi.market_year, mvi.market_week, mcp.market_week_rain_flag, mcp.market_week_snow_flag, mcp.minimum_temperature, mcp.maximum_temperature, mcp.market_season, mvi.vendor_count, mvi.vendor_count_product_category1, mvi.unique_product_count, mvi.unique_product_count_product_category1, mvi.unit_products_qty, mvi.unit_products_qty_product_category1, mvi.bulk_products_qty, mvi.bulk_products_qty_product_category1, mvi.total_product_value, mvi.total_product_value_product_category1, LAG(mcp.weekly_category1_sales, 1) OVER (ORDER BY mvi.market_year, mvi.market_week) AS previous_week_category1_sales, mcp.weekly_category1_sales FROM my_vendor_inventory mvi LEFT JOIN my_customer_purchases mcp ON mvi.market_year = mcp.market_year AND mvi.market_week = mcp.market_week ORDER BY mvi.market_year, mvi.market_week 

Now we have a detailed dataset summarized to one row per week that we could use to explore the relationships between the market weather, product availability, and fresh produce sales. Some of the columns in Figure 13.12 that were shown in previous figures have been condensed so the newly added LAG column is visible. 

Before you read this book, a query like this might have looked large and indecipherable, but now you know that it’s made by using various combinations of straightforward SQL statements you learned in other chapters, which are then combined into datasets with a progressively larger number of columns to use in analysis. 

market market mar sarket_ sini eaxim earket_season wander were unig: unic uniter unit_pese bulk_pr bulk_p tetal_pri totel_pre previousmeek categeryi_sales weekly_category!_sales 2192130-2}2s «22se 437)3% 82«82 «= SeringSummer/ferlySumer/arly FellFall 3>3 222 SSS 222 401.08262.60376.00 240.00250.00120,00 © 0.080.080.08 0.09«0.086.08 1233.58«1151.€@1274.08 60.00128.081398.08 © 9.008.6842.58 6.42.5047.20 292920198Pe 06060C«F a CO 6S©6S72 88«8S90 SummerSummer/EarlySemmor/EarlySummerstoriy/Horly FallFallFotiFoti = 3333 2222 SS86 4421 623.00388.60778.00386.00 649.00699.00240.00240.00 0.080.0376.5361.30 0.080.0361.9076.53 1202.51165.501660.781708.79 651.28710.29128.68120.60 47.2841.2855.70287.38 41.2855.70287.38266.09 

**Chapter 13** ■ **Analytical Dataset Development Examples 211** 

#### **How Do Sales Vary by Customer Zip Code, Market Distance, and Demographic Data?** 

We have a couple of core questions here. How do sales vary by customer zip code and distance from the market? Can we integrate demographic data into this analysis? We will need to pull together several pieces of information to answer these questions. We could group all sales by zip code, but we might get more meaningful answers if we group sales by customer, then look at the summary statistics and distributions of per- customer sales totals by zip code. 

We have the 5- digit zip (postal) code of each customer in the customer table, but we don’t have their full address or 9- digit zip code, so the closest we can get to a “distance from the market” calculation is by calculating the distances between the market location and some location associated with each zip code, such as a centrally located latitude and longitude (keeping in mind that zip codes can be any kind of shape, so the “center” of the area isn’t a great representation of the location of most residences in the postal code). One source of latitudes and longitudes by zip is https://public.opendatasoft.com/explore/ dataset/us- zip- code- latitude- and- longitude/table/?q=22821. If we import this data into our database, we can join it to our queries to add a latitude and longitude per zip code to our dataset. 

There is also plenty of demographic data online related to zip codes, such as census data summarized by ZCTAs (Zip Code Tabulation Areas), so we can pull in age distributions, wealth statistics, and other demographics summarized by zip. 

For this example, I decided to summarize the sales per customer first, then join in the demographic data to every customer’s record, even though it’s not customer- specific. Then, if I were to train a model based on the behavior of customers, I could use the zip code data as an input into the customer- level model, or as a dimension to summarize the other per- customer fields by for reporting purposes. 

So I’ll first summarize sales per customer, including for how long they’ve been a customer, the count of market dates at which they’ve made a purchase, and the total each customer has spent to date. I’ll also join the purchase summary to the customer table, in order to include each customer’s zip code. The output of the following query is shown in Figure 13.13: 

###### SELECT 

c.customer_id, 

c.customer_zip, 

DATEDIFF(MAX(market_date), MIN(market_date)) customer_duration_days, COUNT(DISTINCT market_date) number_of_markets, 

ROUND(SUM(quantity * cost_to_customer_per_qty), 2) total_spent, 

_Continues_ 

**212 Chapter 13** ■ **Analytical Dataset Development Examples** 

###### _(continued)_ 

ROUND(SUM(quantity * cost_to_customer_per_qty) / COUNT(DISTINCT market_date), 2) average_spent_per_market FROM farmers_market.customer c LEFT JOIN farmers_market.customer_purchases cp ON cp.customer_id = c.customer_id GROUP BY c.customer_id 

Note that because of the nature of the sample data, the customers in this case have pretty similar values in this output, which isn’t typical when you look at data collected from real- world scenarios. 

I have loaded some example demographic data into a new table in the database I called zip_data, which is shown in Figure 13.14: 

SELECT * FROM zip_data 

I will join this table to my existing query by the zip code fields, so every customer in a zip code will have the same demographic data added to their record, as shown in Figure 13.15. I condensed the columns that were already shown in Figure 13.13 in order to fit the newly added columns in view: 

###### SELECT 

c.customer_id, 

DATEDIFF(MAX(market_date), MIN(market_date)) AS customer_duration_days, COUNT(DISTINCT market_date) AS number_of_markets, ROUND(SUM(quantity * cost_to_customer_per_qty), 2) AS total_spent, ROUND(SUM(quantity * cost_to_customer_per_qty) / COUNT(DISTINCT market_date), 2) AS average_spent_per_market, 

- c.customer_zip, 

- z.median_household_income AS zip_median_household_income, 

- z.percent_high_income AS zip_percent_high_income, 

- z.percent_under_18 AS zip_percent_under_18, 

- z.percent_over_65 AS zip_percent_over_65, 

- z.people_per_sq_mile AS zip_people_per_sq_mile, 

- z.latitude, 

- z.longitude 

FROM farmers_market.customer c 

LEFT JOIN farmers_market.customer_purchases cp 

ON cp.customer_id = c.customer_id LEFT JOIN zip_data z ON c.customer_zip = z.zip_code_5 GROUP BY c.customer_id 

|customer_id<br>|customer_zip<br>|customer_duration_days<br>|number_of_markets<br>|total_spent<br>|average_spent_per_market<br><br>|
|---|---|---|---|---|---|
|1|22801|“553|“107|"3530.92|33.00<br>:|
|2|22821|553|117|4179.45|35.72|
|3|22821|553|112|3832.16|34.22|
|4|22801|549|115|3561.63|30.97|
|5|22801|556|113|3932.83|34.88|
|6|22801|556|95|3016.47|31.75|
|7|22821|556|188|2921.17|29.21|
|8|22821|553|101|3403.68|33.78|
|9|228@1|556|92|3615.73|32.78|
|16|22801|556|96|2495.41|25.99|



|22821<br>65417<br>@.053<br><br><br><br><br>|@.2<br>|5<br>@.17<br>66.3<br>38.437<br>-78.99<br><br><br><br><br>|
|---|---|---|
|22802<br>48746<br>@.028<br>|0.2|3<br>@.14<br>321.2<br>38.478<br>-78.863|



**214 Chapter 13** ■ **Analytical Dataset Development Examples** 

One part of the analysis question was about distance from the market, which the data we have doesn’t exactly tell us. There is a calculation for distance between two latitudes and longitudes that I found on Dayne Batten’s blog at https://daynebatten.com/2015/09/latitude- longitude- distance- sql/. If the Farmer’s Market is at the coordinates 38.4463, –78.8712, the calculation for distance between the latitude and longitude fields of a record in the dataset and the Farmer’s Market location is: 

ROUND(2 * 3961 * ASIN(SQRT(POWER(SIN(RADIANS((latitude - 38.4463) / 2)),2) + COS(RADIANS(38.4463)) * COS(RADIANS(latitude)) * POWER((SIN(RADIANS((longitude - - 78.8712) / 2))), 2)))) 

Don’t worry about understanding how that calculation works, just know that it returns the distance between two pairs of latitude and longitude rounded to the nearest mile. Replacing the latitude and longitude fields in our query with this calculation, we now have the query: 

###### SELECT 

c.customer_id, DATEDIFF(MAX(market_date), MIN(market_date)) AS customer_duration_days, COUNT(DISTINCT market_date) AS number_of_markets, ROUND(SUM(quantity * cost_to_customer_per_qty), 2) AS total_spent, ROUND(SUM(quantity * cost_to_customer_per_qty) / COUNT(DISTINCT market_date), 2) AS average_spent_per_market, 

c.customer_zip, 

z.median_household_income AS zip_median_household_income, 

z.percent_high_income AS zip_percent_high_income, 

z.percent_under_18 AS zip_percent_under_18, 

z.percent_over_65 AS zip_percent_over_65, 

z.people_per_sq_mile AS zip_people_per_sq_mile, ROUND(2 * 3961 * ASIN(SQRT(POWER(SIN(RADIANS((z.latitude - 38.4463) / 2)),2) + COS(RADIANS(38.4463)) * COS(RADIANS(z.latitude)) * POWER((SIN(RADIANS((z.longitude - - 78.8712) / 2))), 2)))) AS zip_miles_from_market FROM farmers_market.customer AS c LEFT JOIN farmers_market.customer_purchases AS cp ON cp.customer_id = c.customer_id LEFT JOIN zip_data AS z ON c.customer_zip = z.zip_code_5 GROUP BY c.customer_id 

Again, I have condensed the fields shown in Figures 13.13 and 13.15 in order to display the new fields fully in Figure 13.16. 

This will allow me to analyze customer metrics like total amount spent and number of markets attended by customer zip code or by calculated distance from the market. I could now build a scatterplot of zip_miles_from_market 



<!-- Start of picture text -->
custon cust« numbe total_spt average. customer_zip zip_median_household_income zip_percent_high_income zip_percent_under_18 zip_percent_over_65 zip_people_per_sq_mile latitude longitude<br>6 556 95 3016.47 31.75 22801 53042 2.05 0.16 @.11 1279.6 38.427 -78.882<br>7 556 10@ 2921.17 29.21 22821 65417 2.053 0.25 0.17 66.3 38.437 -78.99<br>8 553 101 3403.68 33.78 = 22821 65417 2.053 0.25 0.17 66.3 38.437 -78.99<br>9 556 92 3015.73 32.78 22801 53042 0.05 0.16 @.11 1279.6 38.427 -78.882<br>1e 556 96 2495.41 25.99 22801 53042 2.05 @.16 @.11 1279.6 38.427 -78.882<br>11 556 100 3499.99 35.00 22801 53042 0.05 0.16 @.11 1279.6 38.427 -78.882<br>12 549 103 3298.68 31.94 22821 65417 0.053 0.25 0.17 66.3 38.437 -78.99<br>13 546 71 1582.98 22.30 22821 65417 0.053 0.25 0.17 66.3 38.437 -78.99<br>14 543 68 2322.54 34.16 22801 53042 2.05 0.16 @.11 1279.6 38.427 -78.882<br>15 536 55 1506.35 27.39 22801 53042 0.05 0.16 @.11 1279.6 38.427 -78.882<br>16 553 73 2015.00 27.68 22801 53e42 2.05 0.16 @.11 1279.6 38.427 -78.882<br>7 543 78 1882.61 24.14 22802 48746 0.028 0.23 @.14 321.2 38.478 = -78.863<br>18 55@ 66 1964.08 29.76 22802 48746 0.028 0.23 @.14 321.2 38.478 = -78.863<br>19 535 44 1772.93 40.29 22802 48746 2.028 0.23 @.14 321.2 38.478 = -78.863<br><!-- End of picture text -->



<!-- Start of picture text -->
custon custc numbe total_spe average. customer_zip zip_median_household_ zip_percent_high_income zip_percent_under_18 zip_percent_over_65 zip_people_per_sq_mile zip_miles_from_market<br>4 549 115 3561.63 30.97 22801 53042 0.05 0.16 @.11 1279.6 1<br>5 556 113 3932.83 34.80 22801 53042 0.05 0.16 @.11 1279.6 1<br>6 556 95 3016.47 31.75 22801 53042 0.05 0.16 @.11 1279.6 1<br>7 556 100 2921.17 29.21 22821 65417 0.053 0.25 @.17 66.3 6<br>8 553 101 4=3403.68 +9 33.70 22821 65417 0.053 0.25 0.17 66.3 6<br>9 556 92 3015.73 32.78 22801 53042 0.05 0.16 @.11 1279.6 1<br>18 556 96 2495.41 25.99 22801 53042 0.05 @.16 @.11 1279.6 1<br>11 556 108 3499.99 35.00 22801 53042 0.05 @.16 @.11 1279.6 1<br>12 549 103 3290.08 31.94 22821 65417 @.053 @.25 @.17 66.3 6<br>13 546 71 1582.98 22.3@ 22821 65417 2.053 8.25 @.17 66.3 6<br>14 543 68 2322.54 34.16 22801 53042 @.05 @.16 @.11 1279.6 i<br>15 536 55 1506.35 27.39 22801 53042 0.05 0.16 @.11 1279.6 1<br>16 553 73 2015.06 27.60 22801 53042 @.05 0.16 @.11 1279.6 1<br>7 543 78 1882.61 24.14 22802 48746 0.028 0.23 @.14 321.2 2<br>18 55@ 66 1964.08 29.76 22802 48746 0.028 @.23 e.14 321.2 2<br>19 535 44 1772.93 40.29 22802 48746 0.028 0.23 @.14 321.2 2<br><!-- End of picture text -->

**216 Chapter 13** ■ **Analytical Dataset Development Examples** 

versus total_spent (though all of the customer data points in each zip code would overlap on the distance axis, so I would have to add some jitter or size the dots in order to indicate how many people were represented by that point). 

With the newly added information per zip, I could create a rural versus urban flag based on the population density of the zip code and look at  customer behavior based on that value. I could assess customer longevity by zip code, or look at the distributions of amount spent or customer durations by zip code. I could correlate the percent of high- income residents per zip code with the customers’ total amount spent at the market. There are a wide variety of analyses I could do with just this dataset. 

Some other ideas of additional customer summary fields that could be added to this dataset if we also joined in details about the products include total purchases by product category, top vendor purchased from, number of different vendors purchased from, number of different products purchased, most frequent time of day of purchase, etc. 

Here is one example usage of this dataset where I put the preceding query into a CTE and select from it to get the count of customers and the average total spent per customer for each zip code. Note that in this case, the zip_miles_from_market is the same per row, so I could take the min, max, or average and would get the same value returned because all of the values are identical per zip, which we’re grouping by. I could also add zip_miles_from_market to the GROUP BY statement, or even change the structure of my query so I’m only joining in the zip code data at this point, when I’m summarizing the customers by zip, instead of joining the zip code data to the query inside the CTE. For the purposes of summary, either approach is fine. The output of the following approach is shown in Figure 13.17: 

WITH customer_and_zip_data AS 

( 

SELECT 

c.customer_id, 

DATEDIFF(MAX(market_date), MIN(market_date)) AS customer_duration_days, COUNT(DISTINCT market_date) AS number_of_markets, ROUND(SUM(quantity * cost_to_customer_per_qty), 2) AS total_spent, ROUND(SUM(quantity * cost_to_customer_per_qty) / COUNT(DISTINCT market_date), 2) AS average_spent_per_market, 

c.customer_zip, 

z.median_household_income AS zip_median_household_income, 

z.percent_high_income AS zip_percent_high_income, 

z.percent_under_18 AS zip_percent_under_18, 

z.percent_over_65 AS zip_percent_over_65, 

- z.people_per_sq_mile AS zip_people_per_sq_mile, 

|customer_zip|customer_count|average_total_spent|zip_miles_from_market|
|---|---|---|---|
|22801|is|2681|1|
|228621|7|3064|6|
|228062|4|1857|2|



**218 Chapter 13** ■ **Analytical Dataset Development Examples** 

One clarifying question I would have for the requester in this case before trying to answer these questions is related to time, because I know that the distribution of prices can change over time, and the answer to the second question might have changed at some point as well. So, should we answer these questions only for the most recent market season? Compare year over year? Or just look at all sales for the entire history we have tracked, ignoring any possible changes over time? 

Let’s say that the requester replied to clarify that they want to look at product price distributions for each market season over time (because the types of products sold can be very different in the heat of summer versus at the winter holidays, for example, as well as changing over the years). 

So first, I want to get the product pricing details prior to completing the level of summarization required to answer the questions. 

The first step in this analysis is to get raw data on the price per product per market date. But that seemingly simple task then raises another question: What do we mean by “product”? Is each product_id in the database a product? Like “Carrots” sold by weight? Or do the products differ enough by vendor that I should consider each product_id sold by each vendor as a separate “product”? We were asked to look at the distribution of product prices over time, and different vendors do charge different amounts for the same products if we go by product_id, so I will choose to look at the average price per product per vendor per season. I will start with the original_price per product specified by the vendor in the vendor_inventory table, and won’t consider special discounts given to customers, which would appear in the customer_purchases table. This query’s results are shown in Figure 13.18: 

SELECT p.product_id, p.product_name, p.product_category_id, p.product_qty_type, vi.vendor_id, vi.market_date, SUM(vi.quantity), AVG(vi.original_price) FROM product AS p LEFT JOIN vendor_inventory AS vi ON vi.product_id = p.product_id GROUP BY p.product_id, p.product_name, p.product_category_id, p.product_qty_type, vi.vendor_id, vi.market_date 

|product_id<br>product_name||product_ca|tegory_id<br>product_q|ty_type<br>vendo|r_id<br>market_date|SUM(vi.quantity)|AVG(vi.original_price)|
|---|---|---|---|---|---|---|---|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@8-29|9.38|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-09-02|14.23|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-09-85|9.38|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@9-89|10.75|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@9-12|10.84|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@9-16|10.11|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@9-19|10.04|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-09-23|10.19|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@9-26|9.88|6.990000|
|1<br>Habanero Peppers<br>-|Organic|1|lbs|7|2020-@9-3@|13.76|6.990000|
|2<br>Jalapeno Peppers<br>-|Organic|1|lbs|7|2019-07-03|33.63|3.490000|
|2<br>Jalapeno Peppers<br>|- Organic|1|lbs|7|2019-07-6|24.56|3.490000|
|2<br>Jalapeno Peppers<br>-|Organic|1|lbs|7|2@19-@7-1@|28.83|3.490000|
|2<br>Jalapeno Peppers<br>-|Organic|1|lbs|7|2019-07-13|29.17|3.490000|
|2<br>Jalapeno Peppers<br>-|Organic|1|lbs|7|2@19-@7-17|29.89|3.490000|



**220 Chapter 13** ■ **Analytical Dataset Development Examples** 

Next, since it was determined that we’re looking at prices per season over time, I need to pull in the market_season from the market_date_info table. I can also use the year so we’re talking about seasons over time. And here’s another challenge I can anticipate might arise later when I’m building the reports: The seasons are strings, so how do I know what order they should go in when sorting by season and year? I will keep the minimum month value in the dataset so it can later be used to sort the seasons in the correct order. See Figure 13.19 for the output of this query: 

SELECT p.product_id, p.product_name, p.product_category_id, p.product_qty_type, vi.vendor_id, MIN(MONTH(vi.market_date)) AS month_market_season_sort, mdi.market_season, mdi.market_year, SUM(vi.quantity) AS quantity_available, AVG(vi.original_price) AS avg_original_price FROM product AS p LEFT JOIN vendor_inventory AS vi ON vi.product_id = p.product_id LEFT JOIN market_date_info AS mdi ON vi.market_date = mdi.market_date GROUP BY p.product_id, p.product_name, p.product_category_id, p.product_qty_type, vi.vendor_id, mdi.market_year, mdi.market_season 

One thing you might have noticed is that my attempt to pull in a sortable value to order the market seasons has resulted in multiple month_market_ season_sort values per season, because we are getting the minimum month per season per product, and some products aren’t offered in the earliest month of each season. These differing values could have detrimental effects to our results later on, depending on how we use the sorting field, so we’ll have to be careful how items group and sort with this value involved. We could also use a window function to get the minimum month per market_season across all rows for that season, ignoring the product_id values, which we’ll switch to in the next version of the query. 



<!-- Start of picture text -->
product_id product_neme prodect_category_id precuct_aty.type vendor_i¢ sonth_market_season_sort sarket_sesson merket_year  quantity_evaileple evg_originsl_price<br>2 Mabenere Peppers - Organic 1 ibs 7 7 Sommer/Early Fall 2019 249.94 6.950008<br>2 Mebenero Peppers = Orgenic 2 aes ? ? Semmer/Early Fell 2020 208.01 6.990000<br>2 Jelepens Peppers - Orgenic & abe ? ? Sormar/terty Feil 2019 740.33 3.490009<br>2 Jelepens Peppers - Orgenic 1 ibs ? 7 Semer/Cerly Fall 2020 007.99 3.430000<br>3 Peblana Peppers - Orgenic 1 unde 7 7 Sumer/Early Fall 2019 2750.08 2. seeeoe<br>3 Peblenc Peppers - Orgenic 2 wnt ? bd Senmer/Eerly Fell 2020 2730.08 0. seeeee<br>. Serene Peppers = der 3 welt ? 4 Serine 2039 620.08 4.e0eeee<br>‘ Serene Peppers - Jer 3 wnt 7 6 Semmer/farly fail 2019 1610.08 4.eeeo00<br>‘ Serena Peppers - Jer 3 unt 7 u Late Fall/noligay 2019 628.08 4.eg0e2e<br>« Serane Peopers - Jar 3 unit 7 3 Serine 2020 978.08 4.c0eeee<br>‘ Serene Peccers - 2er 3 unde ? ) Sommer/tarly fell 2620 1420.08 4.e0eee<br>s wmele Wneat Breac 3 unit 8 4 Serine 2019 349.00 6.seeeue<br>s wmole wheat Breac 5 undt 8 ‘ Summer/Early Fail 219 892.08 6.seeeee<br>s lmcle Wheat Bread 3 unit 8 u Late Fall/Holigay 2019 322.08 6.seeeee<br><!-- End of picture text -->

**222 Chapter 13** ■ **Analytical Dataset Development Examples** 

At this point, I also realized that I do need to pull in the customer_purchases data, because the second question is about sales, and the vendor_inventory table only contains available items, not items sold or the total amount generated by sales of each item. So I’ll join that table in and use it to calculate the aggregate sales data for the second question. Note that we need to join on all three matching keys: product_id, vendor_id, and market_date, as shown here, and reflected in the results in Figure 13.20: 

SELECT p.product_id, p.product_name, p.product_category_id, p.product_qty_type, vi.vendor_id, MIN(MONTH(vi.market_date)) OVER (PARTITION BY market_season) AS month_market_season_sort, mdi.market_season, mdi.market_year, AVG(vi.original_price) AS avg_original_price, SUM(cp.quantity) AS quantity_sold, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS total_sales FROM product AS p LEFT JOIN vendor_inventory AS vi ON vi.product_id = p.product_id LEFT JOIN market_date_info AS mdi ON vi.market_date = mdi.market_date LEFT JOIN customer_purchases AS cp ON vi.product_id = cp.product_id AND vi.vendor_id = cp.vendor_id AND vi.market_date = cp.market_date GROUP BY p.product_id, p.product_name, p.product_category_id, p.product_qty_type, vi.vendor_id, mdi.market_year, mdi.market_season 

It would be good at this point to pick a few products and look through the detailed availability and purchase data, to quality check these summarized results before continuing. 



<!-- Start of picture text -->
Brogect_id procuct_same Procuctcategery_ic preductatytyps vendorig morth_merket_seapon_cort market_eaaron market_year avglorigieal_ocice quentity_eold tetal_ealer<br>‘ Banene Peppers - Jar 3 undt 7 Ty Late Fall/moligay 2019 a.apeeee 412.08 1648. BOGE<br>5 hnole kheat Bread =| 3 unit FI py Late Fall/Moligay 2019 ce] 267.08 1735. 5088<br>7 Apole Fle 3 unde Fy Ty Late Fall/Heligey 2019 18. eeeeen 190.00 3420. BORE<br>. Gherry Pie 3 und F 1 Late Fall/Holigey 2019 18.eeteeo 22.00 176.0000<br>4 Secene Peppers < Jer 3 end 7 3 Spring 209 4. DORE 41. 2622.0008<br>‘ Denes Fepoers - Jar 3 unit 7 3 serine aoze 4, 20RRoE 1.0 257.0008<br>$ Whole heat fread 5 undt s 5 Spring 2018 6 Saaeee 2480.00 1820, pnee<br>* bnole brea Bread 3 unit 5 3 Spring 2o20 6. eee 45.09 2372. 5000<br>T apale Fle 3 unde 5 3 Spring zeus 18. e0teee 123.08 224.2008<br>7 Aooke Fie 3 unt 5 3 Soring rere 18.e80eee 158.08 2844.0008<br>Fy henry Pie 3 unde Fy 3 Seeing 29 18.eeteeo 136.08 2488. BORE<br>' Cherry Pie 3 unde F 3 Spring 2020 18. eedeeo 172.00 3006. 2008<br>4 Berens Peppers ~ Jer 3 unde ? € fumear/terly fell 2009 4. DOS 9.00 3207, 2008<br>+ Denese Peppers - Jar 5 und 7 Cf] Sumer/terly fall 2020 4, p0Ene8 97.08 2700.5000<br>$ lnale Wrest Bread = 5 unit 5 6 SummersEarly fall 2019 5, epee 671.08 2361, 5008<br>5 bnale khest Bread 3 unit 5 6 Sumer/Early Fall 2020 Sbeeeee 459.00 3178. 5008<br><!-- End of picture text -->

**224 Chapter 13** ■ **Analytical Dataset Development Examples** 

Now that I have a sale price of each item (the average price each vendor offered each product for each season), I could start exploring the distribution of prices. When developing these queries, I actually tried several different approaches at this point and landed on this one, partly because the small number of products in the database can expose an issue with using NTILEs: two different items of the same price can end up in different NTILEs if the number of NTILEs you choose splits the set at that point. After attempting multiple NTILE number options, I realized that if I wanted to end up with high and low price points in order to answer the second question, I probably shouldn’t be ranking the products anyway. I should be ranking the prices. 

In that case, I decided to modify my approach to group the records by market_year, market_season, and original_price. I used an NTILE value of 3, which then gives me groupings of the top, middle, and bottom 1/3 of prices. I can then summarize the sales of products that fall into each of these price points. Here’s the query that creates three price groupings per season: 

SELECT 

mdi.market_season, mdi.market_year, MIN(MONTH(vi.market_date)) OVER (PARTITION BY market_season) AS month_market_season_sort, vi.original_price, NTILE(3) OVER (PARTITION BY market_year, market_season ORDER BY original_price) AS price_ntile, NTILE(3) OVER (PARTITION BY market_year, market_season ORDER BY original_price DESC) AS price_ntile_desc, COUNT(DISTINCT CONCAT(vi.product_id, vi.vendor_id)) product_count, SUM(cp.quantity) AS quantity_sold, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS total_sales FROM product AS p LEFT JOIN vendor_inventory AS vi ON vi.product_id = p.product_id LEFT JOIN market_date_info AS mdi ON vi.market_date = mdi.market_date LEFT JOIN customer_purchases AS cp ON vi.product_id = cp.product_id AND vi.vendor_id = cp.vendor_id AND vi.market_date = cp.market_date WHERE market_year IS NOT NULL GROUP BY mdi.market_year, mdi.market_season, vi.original_price 

The results of this query are shown in Figure 13.21. 



<!-- Start of picture text -->
market_season market_year month_market_season_sort original_price price_ntile price_ntile_desc product_count quantity_sold total_sales<br>Late Fall/Holiday 2019 11 18.08 3 1 2 422.00 7596 .@008<br>Late Fall/Holiday 2019 11 6.58 2 2 1 267.00 1735.5000<br>Late Fall/Holiday 2019 11 4.08 1 3 1 412.08 1648 .2008<br>Spring 2019 a 18.08 3 1 2 259.00 4662 .2008<br>Spring 2019 3 6.50 2 2 1 280.00 1820.e000<br>Spring 2019 3 4.08 1 3 1 411.00 1612.0000<br>Summer/Early Fall 2019 6 18.0@ 3 1 2 559.08 10062 .0000<br>Summer/Early Fall 2019 6 6.99 3 1 1 175.18 1224.5082<br>Summer/Early Fall 2019 6 6.50 2 3 b 671.00 4361.5008<br>Summer/Early Fall 2019 6 4.08 2 2 p 829.00 3307 .5008<br>Summer/Early Fall 2019 6 3.49 1 3 1 397.91 1382.3506<br>Summer/Early Fall 2019 6 @.58 1 3 2 1718.00 825.6000<br><!-- End of picture text -->

|market_season|market_year|month_market_s|eason_sort<br>original_price|price_ntile<br>price_ntile_desc|product_count|quantity_so|ld<br>total_sales|
|---|---|---|---|---|---|---|---|
|Late Fall/Holiday|2019|11|18.08|3<br>1|2|422.00|7596.@008|
|LateFall/Holiday|2019|11|6.58|2<br>2|1|267.00|1735.5000|
|<br>LateFall/Holiday|2019|11|4.08|1<br>3|1|412.08|1648.2008|
|<br>Spring|2019|a|18.08|3<br>1|2|259.00|<br>4662.2008|
|Spring|2019|3|6.50|2<br>2|1|280.00|1820.e000|
|Spring|2019|3|4.08|1<br>3|1|411.00|1612.0000|
|Summer/EarlyFall|2019|6|18.0@|3<br>1|2|559.08|10062.0000|
|<br>Summer/Early Fall|2019|6|6.99|3<br>1|1|175.18|<br>1224.5082|
|Summer/EarlyFall|2019|6|6.50|2<br>3|b|671.00|4361.5008|
|<br>Summer/EarlyFall|2019|6|4.08|2<br>2|p|829.00|3307.5008|
|<br>Summer/Early Fall|2019|6|3.49|1<br>3|1|397.91|<br>1382.3506|
|Summer/EarlyFall|2019|6|@.58|1<br>3|2|1718.00|825.6000|



**226 Chapter 13** ■ **Analytical Dataset Development Examples** 

Note that the price_ntile break points vary by season. In Summer 2019 and Summer 2020, a $4.00 item is in the second of the three NTILE groups, so it’s in the middle price grouping. In Spring, the distribution of product prices changes, so a $4.00 item is in price_ntile 1, or the low price grouping. 

Also note that I created a column using the NTILE window function with the same number of groups as price_ntile, but sorting the price descending. This way, if you are using the output and don’t know how many groups there are, you can filter to price_ntile = 1 to get the lowest price group, and price_ntile_desc = 1 to get the highest price group. 

Another thing I want to point out in the previous query is that I didn’t COUNT(DISTINCT product_id) values, but first concatenated product_id and vendor_id and did a distinct count of the combined values. The reason is because of how we’re defining “product,” where the same product_id sold by different vendors, possibly for different prices, is considered a different product for our purposes. 

One caveat with these results is that we’re summing up different types of quantities, so we’re counting an ounce, pound, or unit product as “an item sold.” So our quantity isn’t exactly apples- to- apples across seasons, but gives us a quick sales volume measure for rough comparison. 

The output in Figure 13.21 also illustrates why I wanted to create a month_market_season_sort, because alphabetically, the seasons sort out of order as “Late Fall,” “Spring,” and “Summer.” We will make use of the sort values in the next query. 

Now we’ll use the previous query as a CTE and summarize it: 

WITH product_prices AS ( SELECT mdi.market_season, mdi.market_year, MIN(MONTH(vi.market_date)) OVER (PARTITION BY market_season) AS month_market_season_sort, vi.original_price, 

NTILE(3) OVER (PARTITION BY market_year, market_season ORDER BY original_price) AS price_ntile, NTILE(3) OVER (PARTITION BY market_year, market_season ORDER BY original_price DESC) AS price_ntile_desc, COUNT(DISTINCT CONCAT(vi.product_id, vi.vendor_id)) AS product_count, SUM(cp.quantity) AS quantity_sold, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS total_sales FROM product AS p LEFT JOIN vendor_inventory AS vi ON vi.product_id = p.product_id LEFT JOIN market_date_info AS mdi ON vi.market_date = mdi.market_date 

|market|_ market_season|price_ntile|product_count|quantity_sold|min_price|max_price|total_sales|
|---|---|---|---|---|---|---|---|
|2019|Spring|1|1|411.808|4.08|4.08|1612.8008|
|2619|Spring|2|1|280.08|6.58|6.58|<br>182¢.e080|
|2019|Spring|3|2|259.08|18.00|18.00|4662.0008|
|2019|Summer/Early Fall|1|3|2115.91|8.58|3.49|2207.9506|
|2019|Summer/Early Fall|2|2|1500.88|4.08|6.58|7669.8080|
|2019|Summer/Early Fall|3|3|734.18|6.99|18.08|11286.5@82|
|2019|Late Fall/Holiday|1|1|412.00|4.08|4.08|1648. 8000|
|2019|Late Fall/Holiday|2|1|267.08|6.58|6.58|1735.5000|
|2019|Late Fall/Holiday|3|2|422.80|18.08|18.08|7596.8080|



**228 Chapter 13** ■ **Analytical Dataset Development Examples** 

Hopefully these dataset creation walkthroughs have given you a sense of the variety of ways you can combine and summarize data to create a dataset to answer analytical questions, and the kinds of clarifying questions an experienced analyst might ask while going through this process. Keep in mind that each dataset can now be refreshed to pull in the latest data by rerunning the queries, and the results can be reused to answer many questions, not just the ones initially asked! 

###### **<mark>C H A P T E R</mark>** 

# **14** 

## **Storing and Modifying Data** 

We have covered many aspects of developing datasets for machine learning that involve selecting data from a database and preparing it for machine learning models, but what do you do once you have designed your query and are ready to start analyzing the results? Your SQL editor will often allow you to write the results of your query to a CSV file to be imported into Business Intelligence (BI) software such as Tableau or machine learning scripts in a language like Python. However, sometimes for data governance, data security, teamwork, or file size and processing speed purposes, it is preferable to store the dataset within the database. 

In this chapter, we’ll cover some types of SQL queries beyond SELECT statements, such as INSERT statements, which allow you to store the results of your query in a new table in the database. 

#### **Storing SQL Datasets as Tables and Views** 

In most databases, you can store the results of a query as either a table or a view. Storing results as a _table_ takes a snapshot of whatever the results are at the time the query is run and saves the data returned as a new table object, or as new rows appended to an existing table, depending on how you write your SQL statement. A database _view_ instead stores the SQL itself and runs it on- demand when you write a query that references the name of the view, to dynamically 

**229** 

**230 Chapter 14** ■ **Storing and Modifying Data** 

generate a new dataset based on the state of the referenced database objects at the time you run the query. (You may have also heard of the term _materialized view_ , which is more like a stored snapshot and is not what I’m referring to here.) 

If you have database storage space available, permissions to create tables or insert records into tables in your database, and it is not cost- prohibitive to do so, it can be good practice to store snapshots of the datasets you are using in your machine learning applications. You can check with your database administrator to determine whether you can and should create and modify tables, and which schema(s) you have permission to write to. 

When you’re iteratively testing various combinations of fields and parameters in your machine learning algorithm, you’ll want to test multiple different approaches with the same static dataset, so you can be sure your input data isn’t changing each time you run your script by writing the results to a table. You might also decide to store a copy of the dataset for later reference if the dataset you’re querying could change over time and you want to keep a record of the exact values that were run through your model at the time you ran it. 

One way to store the results of a query is to use a CREATE TABLE statement. The syntax is 

CREATE TABLE [schema_name].[new_table_name] AS 

( 

[your query here] ) 

As with the SELECT statements, the indentation and line breaks in these queries don’t matter to the database and are just used to format for readability. The table name used in a CREATE TABLE statement must be new and unique within the schema. If you try to run the same CREATE TABLE statement twice in a row, you will get an error stating that the table already exists. 

Once you create the table, you can query it like any other table or view, referencing the new name you gave it. If you created a table by accident or want to re- create it with a different name or definition, you can DROP the table. 

**~~WARNING~~ Be very careful when using the** DROP TABLE **statement, or you might accidentally delete something that should not have been be deleted! Depending on the database settings and backup frequency, the data you delete may not be recoverable! I usually ensure that I am only granted database permissions to create and drop tables in a personal schema, which is separate from the schema used to run applications or where tables that others are using are stored, so I can’t accidentally delete a table I did not create or that is used in a production application.** 

The syntax for dropping a table is simply: 

DROP TABLE [schema_name].[table_name] 

**Chapter 14** ■ **Storing and Modifying Data 231** 

So, to create, select from, and drop a table that contains a snapshot of the data that is currently in the Farmer’s Market database product table, filtered to products with a quantity type “unit,” run the following three queries in sequence: 

CREATE TABLE farmers_market.product_units AS ( SELECT * FROM farmers_market.product WHERE product_qty_type = "unit" ) ; SELECT * FROM farmers_market.product_units ; DROP TABLE farmers_market.product_units ; 

The semicolons are used to separate multiple queries in the same file. 

**~~TIP~~ If you don’t want to accidentally run a** DROP TABLE **statement that is included in a file with other SQL statements (since many SQL editors have a “run all” command), comment it out immediately after running it, and save the file with that query commented out, so you don’t accidentally run it the next time you open the file and drop a table you didn’t intend to! In MySQL Workbench, you can comment out code by preceding each line with two dashes and a space or by surrounding a block of code with** /* **and** */ **.** 

Database views are created and dropped the same exact way as tables, though when you create a view, you are not actually storing the data, but storing the query to be run when you query the view. So when you drop a view, you are not actually deleting any data, since the data isn’t stored; you are just dropping the named reference to the query: 

CREATE VIEW farmers_market.product_units_vw AS ( SELECT * FROM farmers_market.product WHERE product_qty_type = "unit" ) ; SELECT * FROM farmers_market.product_units_vw ; DROP VIEW farmers_market.product_units_vw ; 

Note that some database systems, like SQL Server, support a SELECT INTO syntax, which operates much like the CREATE TABLE statement previously 

|product_id|product_name|product_size|product_category_id|product_qty_type|snapshot_timestamp|
|---|---|---|---|---|---|
|3|Poblano Peppers<br>- Organic|large|1|unit|2021-04-18 @@:49:24|
|4|Banana Peppers<br>-<br>Jar|8 oz|3|unit|2021-04-18 00:49:24|
|5|Whole Wheat<br>Bread|1.5<br>lbs|3|unit|2021-04-18 00:49:24|
|6|Cut Zinnias Bouquet|medium|5|unit|2021-04-18 00:49:24|
|7|Apple Pie|1"|3|unit|2021-04-18 00:49:24|
|8|Cherry Pie|10"|3|unit|2021-04-18 00:49:24|
|1@|Eggs|1 dozen|6|unit|2021-04-18 00:49:24|
|12|Baby Salad Lettuce Mix<br>- Bag|1/2 lb|1|unit|2021-04-18 00:49:24|
|16|Sweet Corn|Ear|1|unit|2021-04-18 00:49:24|
|18|Carrots<br>- Organic|bunch|1|unit|2021-04-18 00:49:24|
|19|Farmer's Market Resuable Shopping Bag|medium|7|unit|2021-04-18 00:49:24|



|product_id|product_name|product_size<br>product_category_id<br>product_qty_type|snapshot_timestamp|
|---|---|---|---|
|23|Maple Syrup<br>-<br>Jar|8 oz<br>2<br>unit|2021-@4-11 23:41:41|
|23|Maple Syrup<br>-<br>Jar|8 oz<br>2<br>unit|2021-04-18 08:49:24|



**234 Chapter 14** ■ **Storing and Modifying Data** 

You may want to start with SELECT * instead of DELETE so you can see what rows will be deleted before running the DELETE statement! 

The product_id and snapshot_timestamp uniquely identify rows in the product_units table, so we can run the following statement to delete the row added by our previous INSERT INTO: 

DELETE FROM farmers_market.product_units WHERE product_id = 23 AND snapshot_timestamp = '2021- 04- 18 00:49:24' 

Sometimes you want to update a value in an existing row instead of inserting 

a totally new row. The syntax for an UPDATE statement is as follows: 

UPDATE [schema_name].[table_name] 

SET [column_name] = [new value] 

WHERE [set of conditions that uniquely identifies the rows you want to change] 

Let’s say that you’ve already entered all of the farmer’s market vendor booth assignments for the next several months, but vendor 4 informs you that they can’t make it on October 10, so you decide to upgrade vendor 8 to vendor 4’s booth, which is larger and closer to the entrance, for the day. 

Before making any changes, let’s snapshot the existing vendor booth assignments, along with the vendor name and booth type, into a new table using the following SQL: 

CREATE TABLE farmers_market.vendor_booth_log AS ( SELECT vba.*, b.booth_type, v.vendor_name, CURRENT_TIMESTAMP AS snapshot_timestamp FROM farmers_market.vendor_booth_assignments vba INNER JOIN farmers_market.vendor v ON vba.vendor_id = v.vendor_id INNER JOIN farmers_market.booth b ON vba.booth_number = b.booth_number WHERE market_date >= '2020- 10- 01' ) 

Selecting all records from this new log table produces the results shown in Figure 14.3. 

|vendor_id|booth_number|market_date|booth_type|vendor_name|snapshot_timestamp|
|---|---|---|---|---|---|
|1|2|2020-10-87|Standard|Chris's Sustainable Eggs & Meats|2021-04-18 01:23:24|
|3|1|2020-10-87|Standard|Mountain View Vegetables|2021-04-18 @1:23:24|
|4|7|2020-10-@7|Standard|Fields of Corn|2021-04-18 61:23:24|
|7|11|2020-10-87|Large|Marco's Peppers|2021-04-18 @1:23:24|
|8|6|2026-18-87|Small|Annie's Pies|2021-04-18 @1:23:24|
|9|8|2020-10-07|Small|MediterraneanBakery|2021-04-18@1:23:24|
|1|2|2626-18-18|Standard|<br>Chris's Sustainable Eggs & Meats|<br>2021-04-18 @1:23:24|
|3|1|2020-18-18|Standard|Mountain View Vegetables|2021-04-18 @1:23:24|
|4|7|2628-18-18|Standard|Fields of Corn|2621-04-18 @1:23:24|
|7|11|2628-18-18|Large|Marco's Peppers|2021-04-18 @1:23:24|
|8|6|2826-10-18|Small|Annie's Pies|2621-04-18 @1:23:24|
|9|8|2020-18-18|Small|MediterraneanBakery|2021-04-18@1:23:24|



a 7 2620-18-83 2021-04-18 61:23:24 4 7 2020-10-87 2021-04-18 61:23:24 os 7 2620-18-18 2021-04-18 @1:23:24 8 6 2020-10-83 2021-04-18 @1:23:24 8 6 2020-18-87 2021-04-18 61:23:24 8 6 2020-10-18 2021-04-18 @1:23:24 4 7 2020-18-83 2021-04-18 61:35:14 es 7 2020-10-87 2021-04-18 61:35:14 & 6 2020-18-83 2021-04-18 61:35:14 8 6 2020-10-87 2021-04-18 @1:35:14 8 7 2620-18-18 2021-04-18 61:35:14 

**Chapter 14** ■ **Storing and Modifying Data 237** 

available to help you connect and write to a variety of databases without even needing to write dynamic SQL INSERT statements— the packages generate the SQL for you to insert values from an object in Python like a dataframe into a database table for persistent storage. 

Another approach is to programmatically create a file to temporarily store your data, transfer the file to a location that is accessible from your script and your database, and load the results from the file into your table. For example, you might use Python to write data from a pandas dataframe to a CSV file, transfer the CSV file to an Amazon Web Services S3 bucket, then access the file from the database and copy the records into an existing table in a Redshift database. All of these steps can be automated from your script. 

One machine learning use case for writing data from your script to the database is if you want to store your transformed dataset after you have completed feature engineering and data preprocessing steps in your script that weren’t completed in the original dataset- generating SQL. 

Another use case for writing values generated within your script back to the database is when you want to store the results that your predictive model generates and associate them with the original dataset. You can create a table that stores the unique identifiers for the rows in your input dataset for which you have scores, a timestamp, the name or ID of your model, and the score or classification generated by the model for each record. You can insert new rows into the table each time you refresh your model scores. Then, use a SQL query to filter this model score log table to a specific date and model identifier and join it to the table with your input dataset, joining on the unique row identifiers. This will allow you to analyze the results of the model alongside the input data used to generate the predictions at the time. 

There are many ways to connect to and interact with data from a database in your other scripts that may or may not require SQL. 

#### **In Closing** 

Now that you know SQL basics, you should have the foundation needed to create datasets for your machine learning models, even if you need to search the internet for functions and syntax that were not covered in this book. 

I have been a data scientist for five years now, and all of the queries I have written to generate my datasets for machine learning have been variations of the SQL I originally learned in school 20 years ago. I hope that this book has given you the SQL skills you need to achieve your analysis goals faster and more independently, and that you find pulling and modifying your own datasets as empowering as I do! 

**238 Chapter 14** ■ **Storing and Modifying Data** 

#### **Exercises** 

1. If you include a CURRENT_TIMESTAMP column when you create a view, what would you expect the values of that column to be when you query the view? 

2. Write a query to determine what the data from the vendor_booth_ assignment table looked like on October 3, 2020 by querying the vendor_booth_log table created in this chapter. (Assume that records have been inserted into the log table any time changes were made to the vendor_booth_assignment table.) 

###### **<mark>A P P E N D I X</mark>** 

## **Answers to Exercises** 

#### **Chapter 1: Data Sources** 

##### **Answers** 

1. If the “Author Full Name” field is updated (overwritten) in the existing Authors table record for the author, then when a query is run to retrieve a list of authors and their books, all past books associated with the author will now be associated with the author’s new name in the database, even if that wasn’t the name printed on the cover of the book. 

   - If instead a new row is added to the Authors table to record the new name (leaving the existing books associated with the prior name), then there might be no way to know that the two authors, who now have different Author IDs, are actually the same person. 

There are solutions to this problem that include designing the database tables and relationships to allow multiple names per Author ID, with start and stop dates, or adding a field to the Authors table such as “prior Author ID” that associates an Authors table record with another record in the same table, if one exists. 

Understanding these relationships and when and how data is updated in the database you’re querying is important for understanding and explaining the results of your queries. 

**239** 

**240 Appendix** ■ **Answers to Exercises** 

2. One example might be tracking personal exercise routines. You could have a table of workout sessions and a table of exercises, which would be a _many to many_ relationship: each workout could contain multiple exercises, and each exercise could be part of multiple workouts. If you included a table of workout session locations, that could be designed as a “one to many” relationship with the workout sessions table, assuming each workout could only take place in one location (say, at home or at the gym), but each location could be the site of many workout sessions. 

#### **Chapter 2: The SELECT Statement** 

##### **Answers** 

1. This query returns everything in the customer table: 

SELECT * FROM farmers_market.customer 

2. This query displays all of the columns and 10 rows from the customer table, sorted by customer_last_name, then customer_first_name: 

SELECT * FROM farmers_market.customer ORDER BY customer_last_name, customer_first_name LIMIT 10 

3. This query lists all customer IDs and first names in the customer table, sorted by first_name: 

SELECT customer_id, customer_first_name FROM farmers_market.customer ORDER BY customer_first_name 

#### **Chapter 3: The WHERE Clause** 

##### **Answers** 

There are multiple answers to most SQL questions, but here are some possible solutions for the exercises in Chapter 3: 

1. Remember that even though the English phrasing is “product ids 4 and 9,” using AND between the conditions in the query will not return any results, because there is only one product_id per customer_purchase. Use 

**Appendix** ■ **Answers to Exercises 241** 

an OR between the conditions in the WHERE clause to return every row that has a product_id of either 4 or 9: 

SELECT * FROM farmers_market.customer_purchases WHERE product_id = 4 OR product_id = 9 

2. Note that the first query uses >= and <= to establish the inclusive range, while the second query uses BETWEEN to achieve the same result: 

SELECT * FROM farmers_market.customer_purchases WHERE vendor_id >= 8 AND vendor_id <= 10 

SELECT * FROM farmers_market.customer_purchases WHERE vendor_id BETWEEN 8 AND 10 

3. One approach is to filter to market dates that are not in the “rainy dates” list, by using the NOT operator to negate the IN condition. This will return TRUE for the rows in the customer_purchases table with a market_date that is NOT IN the query in the WHERE clause: 

SELECT market_date, customer_id, vendor_id, quantity * cost_to_customer_per_qty AS price FROM farmers_market.customer_purchases WHERE market_date NOT IN ( SELECT market_date FROM farmers_market.market_date_info WHERE market_rain_flag = 1 ) 

Another option is to keep the IN condition but change the query in the WHERE clause to return dates where it was not raining, when market_rain_ flag is set to 0: 

SELECT market_date, customer_id, vendor_id, quantity * cost_to_customer_per_qty AS price FROM farmers_market.customer_purchases 

_Continues_ 

**242 Appendix** ■ **Answers to Exercises** 

_(continued)_ 

WHERE market_date IN ( SELECT market_date FROM farmers_market.market_date_info WHERE market_rain_flag = 0 ) 

#### **Chapter 4: CASE Statements** 

##### **Answers** 

1. Look back at Figure 2.1 for sample data and column names for the product table referenced in this exercise. This query outputs the product_id and product_name columns from product, with a column called prod_qty_ type_condensed that displays the word “unit” if the product_qty_type is “unit,” and otherwise displays the word “bulk”: 

SELECT product_id, product_name, CASE WHEN product_qty_type = "Unit" THEN "unit" ELSE "bulk" END AS prod_qty_type_condensed FROM farmers_market.product 

2. To add a column to the previous query called pepper_flag that outputs a 1 if the product_name contains the word “pepper” (regardless of capitalization), and otherwise outputs 0, do the following: 

SELECT product_id, product_name, CASE WHEN product_qty_type = "Unit" THEN "per unit" ELSE "bulk" END AS prod_qty_type_condensed, CASE WHEN LOWER(product_name) LIKE '%pepper%' THEN 1 ELSE 0 END AS pepper_flag FROM farmers_market.product 

3. If the product name doesn’t include the word “pepper,” spelled exactly that way, it won’t be flagged. For example, a product might only be labeled as “Jalapeno” instead of Jalapeno pepper. 

**Appendix** ■ **Answers to Exercises 243** 

#### **Chapter 5: SQL JOINs** 

##### **Answers** 

1. This query INNER JOINs the vendor table to the vendor_booth_ assignments table and sorts the result by vendor_name , then market_date: 

SELECT * FROM vendor AS v INNER JOIN vendor_booth_assignments AS vba ON v.vendor_id = vba.vendor_id ORDER BY v.vendor_name, vba.market_date 

2. The following query uses a LEFT JOIN to produce output identical to the output of this exercise’s query: 

SELECT c.*, cp.* FROM customer_purchases AS cp LEFT JOIN customer AS c ON cp.customer_id = c.customer_id 

This could have been written with SELECT * and be considered correct. Using the table aliases in this way allows you to control which table’s columns are displayed first, so in addition to returning the same data, it’s also returned with the same column order as the given query. 

3. One approach is to INNER JOIN the product table and the product_ category table, to get the category of every product (a new category with no products in it yet wouldn’t need to be included here, and there shouldn’t be any products without categories), then LEFT JOIN the vendor_inventory table to the product table. I chose a LEFT JOIN instead of an INNER JOIN because we might want to know if products exist in the database that are never in season because they have never been offered by a vendor at the farmer’s market. There are acceptable answers that include all types of JOINs, as long as the reason for each choice is explained. 

Because we haven’t learned about aggregation (summarization) yet, the dataset you can create using the information included in this chapter will have one row per product per vendor who offered it per market date it was offered, labeled with the product category. Because the vendor_inventory table includes the date the product was offered for sale, you could sort by product_category, product, and market_date, and scroll through the query results to determine when each type of item is in season. 

**244 Appendix** ■ **Answers to Exercises** 

#### **Chapter 6: Aggregating Results for Analysis** 

##### **Answers** 

1. This query determines how many times each vendor has rented a booth at the farmer’s market: 

SELECT vendor_id, count(*) AS count_of_booth_assignments FROM farmers_market.vendor_booth_assignments GROUP BY vendor_id 

2. This query displays the product category name, product name, earliest date available, and latest date available for every product in the “Fresh Fruits & Vegetables” product category: 

SELECT pc.product_category_name, p.product_name, min(market_date) AS first_date_available, max(market_date) AS last_date_available FROM farmers_market.vendor_inventory vi INNER JOIN farmers_market.product p ON vi.product_id = p.product_id INNER JOIN farmers_market.product_category pc ON p.product_category_id = pc.product_category_id WHERE product_category_name = 'Fresh Fruits & Vegetables' 

3. This query joins two tables, uses an aggregate function, and uses the HAVING keyword to generate a list of customers who have spent more than $50, sorted by last name, then first name: 

SELECT cp.customer_id, c.customer_first_name, c.customer_last_name, SUM(quantity * cost_to_customer_per_qty) AS total_spent FROM farmers_market.customer c LEFT JOIN farmers_market.customer_purchases cp ON c.customer_id = cp.customer_id GROUP BY cp.customer_id, c.customer_first_name, c.customer_last_name HAVING total_spent > 50 ORDER BY c.customer_last_name, c.customer_first_name 

**Appendix** ■ **Answers to Exercises 245** 

#### **Chapter 7: Window Functions and Subqueries** 

##### **Answers** 

1. Here are the answers to the two parts of this exercise: 

   - a. These queries use DENSE_RANK() or ROW_NUMBER() to select from the customer_purchases table and numbers each customer’s visits to the Farmer’s Market using DENSE_RANK(): 

select cp.*, DENSE_RANK() OVER (PARTITION BY customer_id ORDER BY market_date) AS visit_number FROM farmers_market.customer_purchases AS cp ORDER BY customer_id, market_date 

###### or 

select customer_id, market_date, ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY market_date) AS visit_number FROM farmers_market.customer_purchases GROUP BY customer_id, market_date ORDER BY customer_id, market_date 

- b. This is how to reverse the numbering of the preceding query so each customer’s most recent visit is labeled 1, and then use another query to filter the results to only the customer’s most recent visit: 

SELECT * FROM ( select customer_id, market_date, ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY market_ date DESC) AS visit_number FROM farmers_market.customer_purchases GROUP BY customer_id, market_date ORDER BY customer_id, market_date ) x where x.visit_number = 1 

###### Or 

SELECT * FROM ( select cp.*, DENSE_RANK() OVER (PARTITION BY customer_id ORDER BY market_ date DESC) AS visit_number FROM farmers_market.customer_purchases AS cp ORDER BY customer_id, market_date ) x where x.visit_number = 1 

**246 Appendix** ■ **Answers to Exercises** 

2. Here’s how to use a COUNT() window function and include a value along with each row of the customer_purchases table that indicates how many different times that customer has purchased that product_id: 

select cp.*, 

COUNT(product_id) OVER (PARTITION BY customer_id, product_id) AS product_purchase_count 

FROM farmers_market.customer_purchases AS cp ORDER BY customer_id, product_id, market_date 

3. If you swap out LEAD for LAG, you’re looking at the next row instead of the previous, so to get the same output, you just have to sort market_date in descending order, so everything is reversed! 

SELECT 

market_date, 

SUM(quantity * cost_to_customer_per_qty) AS market_date_total_sales, LEAD(SUM(quantity * cost_to_customer_per_qty), 1) OVER (ORDER BY market_date DESC) AS previous_market_date_total_sales FROM farmers_market.customer_purchases GROUP BY market_date ORDER BY market_date 

#### **Chapter 8: Date and Time Functions** 

##### **Answers** 

1. Here is how to get the customer_id, month, and year (in separate columns) of every purchase in the farmers_market.customer_purchases table: 

SELECT customer_id, 

EXTRACT(MONTH FROM market_date) AS purchase_month, EXTRACT(YEAR FROM market_date) AS purchase_year FROM farmers_market.customer_purchases 

2. Here is an example of filtering and summing purchases made in the past two weeks. 

Using March 31, 2019 as the reference date: 

SELECT MIN(market_date) AS sales_since_date, SUM(quantity * cost_to_customer_per_qty) AS total_sales FROM farmers_market.customer_purchases WHERE DATEDIFF('2019- 03- 31', market_date) <= 14 

**Appendix** ■ **Answers to Exercises 247** 

Using CURDATE(), which will result in NULL results on the sample database, since all dates are more than two weeks ago: 

SELECT MIN(market_date) AS sales_since_date, SUM(quantity * cost_to_customer_per_qty) AS total_sales FROM farmers_market.customer_purchases WHERE DATEDIFF(CURDATE(), market_date) <= 14 

3. This is an example of using a quality control query to check manually entered data for correctness: 

SELECT market_date, market_day, DAYNAME(market_date) AS calculated_market_day, CASE WHEN market_day <> DAYNAME(market_date) then "INCORRECT" ELSE "CORRECT" END AS entered_correctly FROM farmers_market.market_date_info 

#### **Chapter 9: Exploratory Data Analysis with SQL** 

##### **Answers** 

1. The following query gets the earliest and latest dates in the customer_ purchases table: 

SELECT MIN(market_date), MAX(market_date) FROM farmers_market.customer_purchases 

2. Here is how to use the DAYNAME() and EXTRACT() functions to select and group by the weekday and hour of the day, and count the distinct number of customers during each hour of the Wednesday and Saturday markets: 

SELECT DAYNAME(market_date), EXTRACT(HOUR FROM transaction_time), COUNT(DISTINCT customer_id) FROM farmers_market.customer_purchases GROUP BY DAYNAME(market_date),  EXTRACT(HOUR FROM transaction_time) ORDER BY DAYNAME(market_date),  EXTRACT(HOUR FROM transaction_time) 

3. A variety of answers would be acceptable. Two examples are shown here. 

How many customers made purchases at each market? 

SELECT market_date, COUNT(DISTINCT customer_id) FROM customer_purchases GROUP BY market_date ORDER BY market_date 

**248 Appendix** ■ **Answers to Exercises** 

What is the total value of the inventory each vendor brought to each market? 

SELECT market_date, vendor_id, ROUND(SUM(quantity * original_price),2) AS inventory_value FROM vendor_inventory GROUP BY market_date, vendor_id ORDER BY market_date, vendor_id 

#### **Chapter 10: Building SQL Datasets for Analytical Reporting** 

##### **Answers** 

1. Sales per vendor per market week: 

SELECT market_week, vendor_id, vendor_name, SUM(sales) AS weekly_sales FROM farmers_market.vw_sales_by_day_vendor AS s GROUP BY market_week, vendor_id, vendor_name ORDER BY market_date 

2. Subquery rewritten using a WITH clause: 

WITH x AS ( SELECT market_date, vendor_id, booth_number, LAG(booth_number,1) OVER (PARTITION BY vendor_id ORDER BY market_ date, vendor_id) AS previous_booth_number FROM farmers_market.vendor_booth_assignments ORDER BY market_date, vendor_id, booth_number ) SELECT * FROM x WHERE x.market_date = '2020- 03- 13' AND (x.booth_number <> x.previous_booth_number OR x.previous_booth_number IS NULL) 

3. There is one vendor booth assignment per vendor per market date, so we don’t need to change the granularity of our dataset in order to summarize by booth type, but we do need to pull that booth type into the dataset. We can accomplish that by LEFT JOINing in the vendor_booth_assignments 

**Appendix** ■ **Answers to Exercises 249** 

and booth tables, and including the booth_number and booth_type columns in our SELECT statement: 

SELECT cp.market_date, md.market_day, md.market_week, md.market_year, cp.vendor_id, v.vendor_name, v.vendor_type, **vba.booth_number, b.booth_type,** ROUND(SUM(cp.quantity * cp.cost_to_customer_per_qty),2) AS sales FROM farmers_market.customer_purchases AS cp LEFT JOIN farmers_market.market_date_info AS md ON cp.market_date = md.market_date LEFT JOIN farmers_market.vendor AS v ON cp.vendor_id = v.vendor_id **LEFT JOIN farmers_market.vendor_booth_assignments AS vba ON cp.vendor_id = vba.vendor_id AND cp.market_date = vba.market_date LEFT JOIN farmers_market.booth AS b ON vba.booth_number = b.booth_number** GROUP BY cp.market_date, cp.vendor_id ORDER BY cp.market_date, cp.vendor_id 

#### **Chapter 11: More Advanced Query Structures** 

##### **Answers** 

1. There are multiple possible solutions. Here is one: 

WITH sales_per_market_date AS ( SELECT market_date, ROUND(SUM(quantity * cost_to_customer_per_qty),2) AS sales FROM farmers_market.customer_purchases GROUP BY market_date ORDER BY market_date ), record_sales_per_market_date AS ( SELECT cm.market_date, cm.sales, 

_Continues_ 

**250 Appendix** ■ **Answers to Exercises** 

_(continued)_ 

MAX(pm.sales) AS previous_max_sales, CASE WHEN cm.sales > MAX(pm.sales) THEN "YES" ELSE "NO" END sales_record_set FROM sales_per_market_date AS cm LEFT JOIN sales_per_market_date AS pm ON pm.market_date < cm.market_date GROUP BY cm.market_date, cm.sales ) SELECT market_date, sales FROM record_sales_per_market_date WHERE sales_record_set = 'YES' ORDER BY market_date DESC LIMIT 1 

2. This may be more challenging than you initially anticipated! First, we need to add vendor_id to the output and the partition in the CTE, so we are ranking the first purchase date per customer per vendor. Then, we need to count the distinct customers per market per vendor, so we add the vendor_id to the GROUP BY in the outer query, and also modify the CASE statements to use the field we have re- aliased to first_purchase_from_vendor_date: 

WITH customer_markets_vendors AS ( SELECT DISTINCT customer_id, vendor_id, market_date, MIN(market_date) OVER(PARTITION BY cp.customer_id, cp.vendor_id) AS first_purchase_from_vendor_date FROM farmers_market.customer_purchases cp ) SELECT md.market_year, md.market_week, cmv.vendor_id, COUNT(customer_id) AS customer_visit_count, COUNT(DISTINCT customer_id) AS distinct_customer_count, COUNT(DISTINCT CASE WHEN cmv.market_date = cmv.first_purchase_from_vendor_date THEN customer_id ELSE NULL 

**Appendix** ■ **Answers to Exercises 251** 

END) AS new_customer_count, COUNT(DISTINCT CASE WHEN cmv.market_date = cmv.first_purchase_from_vendor_date THEN customer_id ELSE NULL END) / COUNT(DISTINCT customer_id) AS new_customer_percent FROM customer_markets_vendors AS cmv LEFT JOIN farmers_market.market_date_info AS md ON cmv.market_date = md.market_date GROUP BY md.market_year, md.market_week, cmv.vendor_id ORDER BY md.market_year, md.market_week, cmv.vendor_id 

3. Again, there are many possible solutions, but here is one where the sales per market date are ranked ascending and descending, and then the top results from each of those rankings are selected and unioned together: 

WITH sales_per_market AS ( SELECT market_date, ROUND(SUM(quantity * cost_to_customer_per_qty),2) AS sales FROM farmers_market.customer_purchases GROUP BY market_date ), market_dates_ranked_by_sales AS ( SELECT market_date, sales, RANK() OVER (ORDER BY sales) AS sales_rank_asc, RANK() OVER (ORDER BY sales DESC) AS sales_rank_desc FROM sales_per_market ) SELECT market_date, sales, sales_rank_desc AS sales_rank FROM market_dates_ranked_by_sales WHERE sales_rank_asc = 1 UNION SELECT market_date, sales, sales_rank_desc AS sales_rank FROM market_dates_ranked_by_sales WHERE sales_rank_desc = 1 

**252 Appendix** ■ **Answers to Exercises** 

#### **Chapter 12: Creating Machine Learning Datasets Using SQL** 

##### **Answers** 

1. This can be accomplished by duplicating the customer_markets_ attended_30days_count feature and replacing each “30” with 14: 

(SELECT COUNT(market_date) FROM customer_markets_attended cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date AND DATEDIFF(cp.market_date, cma.market_date) <= 14) AS customer_markets_attended_14days_count, 

2. The query is already grouped by customer_id and market_date, so we just need to add a column that determines if any underlying row has an item with a price over $10, and if so, return a 1, then use the MAX function to get the highest number per group, which will be a 1 if any row met the criteria: 

MAX(CASE WHEN cp.cost_to_customer_per_qty > 10 THEN 1 ELSE 0 END) purchased_item_over_10_dollars, 

3. This is a tricky one. One way to accomplish it is to add the purchase_total per market date to the CTE, then add up all purchase_total values for dates prior to the row’s market_date. Both total_spent_to_date and customer_has_spent_over_200 fields have been added to the following query, which also includes the fields from exercises 1 and 2: 

WITH customer_markets_attended AS ( SELECT customer_id, market_date, SUM(quantity * cost_to_customer_per_qty) AS purchase_total, ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY market_ date) AS market_count FROM farmers_market.customer_purchases GROUP BY customer_id, market_date ORDER BY customer_id, market_date ) 

SELECT cp.customer_id, cp.market_date, 

**Appendix** ■ **Answers to Exercises 253** 

EXTRACT(MONTH FROM cp.market_date) AS market_month, SUM(cp.quantity * cp.cost_to_customer_per_qty) AS purchase_total, COUNT(DISTINCT cp.vendor_id) AS vendors_patronized, MAX(CASE WHEN cp.vendor_id = 7 THEN 1 ELSE 0 END) AS purchased_ from_vendor_7, MAX(CASE WHEN cp.vendor_id = 8 THEN 1 ELSE 0 END) AS purchased_ from_vendor_8, COUNT(DISTINCT cp.product_id) AS different_products_purchased, DATEDIFF(cp.market_date, (SELECT MAX(cma.market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date GROUP BY cma.customer_id)) days_since_last_customer_market_date, (SELECT MAX(market_count) FROM customer_markets_attended cma WHERE cma.customer_id = cp.customer_id AND cma.market_date <= cp.market_date) AS customer_ markets_attended_count, (SELECT COUNT(market_date) FROM customer_markets_attended cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date AND DATEDIFF(cp.market_date, cma.market_date) <= 30) AS customer_markets_attended_30days_count, (SELECT COUNT(market_date) FROM customer_markets_attended cma WHERE cma.customer_id = cp.customer_id AND cma.market_date < cp.market_date AND DATEDIFF(cp.market_date, cma.market_date) <= 14) AS customer_markets_attended_14days_count, MAX(CASE WHEN cp.cost_to_customer_per_qty > 10 THEN 1 ELSE 0 END) AS purchased_item_over_10_dollars, (SELECT SUM(purchase_total) FROM customer_markets_attended cma WHERE cma.customer_id = cp.customer_id AND cma.market_date <= cp.market_date) AS total_spent_to_ date, CASE WHEN (SELECT SUM(purchase_total) FROM customer_markets_attended cma WHERE cma.customer_id = cp.customer_id AND cma.market_date <= cp.market_date) > 200 THEN 1 ELSE 0 END AS customer_has_spent_over_200, CASE WHEN DATEDIFF( (SELECT MIN(cma.market_date) FROM customer_markets_attended AS cma WHERE cma.customer_id = cp.customer_id AND cma.market_date > cp.market_date 

_Continues_ 

**254 Appendix** ■ **Answers to Exercises** 

###### _(continued)_ 

GROUP BY cma.customer_id), cp.market_date) <=30 THEN 1 ELSE 0 END AS purchased_ again_within_30_days FROM farmers_market.customer_purchases AS cp GROUP BY cp.customer_id, cp.market_date ORDER BY cp.customer_id, cp.market_date 

#### **Chapter 14: Storing and Modifying Data** 

##### **Answers** 

1. The timestamp returned when you query the view will be the current time (on the server), because unlike with a table, the view isn’t storing any data and is generating the results of the query when it is run. 

2. There are multiple correct answers, but one approach is to filter to records prior to October 4, 2020 (so if a change was made at any time on October 3, it is retrieved), and include a window function that returns the maximum timestamp per vendor and booth pair, indicating the most recent record of each booth assignment on or before the filtered date range. Then, the results of the query are embedded inside an outer query that filters to rows in the subquery where the snapshot timestamp matches the maximum timestamp calculated in the window function: 

SELECT x.* FROM ( SELECT vendor_id, booth_number, market_date, snapshot_timestamp, MAX(snapshot_timestamp) OVER (PARTITION BY vendor_id, booth_ number) AS max_timestamp_in_filter FROM farmers_market.vendor_booth_log WHERE DATE(snapshot_timestamp) <= '2020- 10- 04' ) AS x WHERE x.snapshot_timestamp = x.max_timestamp_in_filter 

## **Index** 

###### **A** 

Access (Microsoft), 2 ad- hoc reporting, 143 aggregation AVG (average) function within, 91–93 CASE statement inside, 94–96 COUNT DISTINCT function within, 90–91 COUNT function within, 90–91 date functions within, 119–125 displaying group summaries, 80–83 exercise using, 244–245 granularity and, 138 GROUP BY within, 79–80 on joined tables, 86 LISTAGG for, 111 MAX function within, 88–90 MIN function within, 88–90 performing calculations inside, 84–88 underlying data prior to, 183 window functions and, 97, 103–108 algorithms, 177, 185 alias WITH clause (CTE), 204–205 FROM clause and, 66 columns, 21–22, 65–66 within Exploratory Data Analysis (EDA), 130 of tables, 66, 89 Amazon Redshift, 2, 115, 119 analytical dataset custom, 149–153 requirements of, 144–148 reusing of, 153–157 AND NOT operator, 34, 38 AND operator, 34, 37, 38 

AS keyword, 21, 22, 66, 149 ASC (ascending) keyword, 18–19 asterisk symbol, 16, 21 attribute, 3–4 averaging, 92 AVG (average) function, 91–93, 97, 103–104 

###### **B** 

Batten, Dayne, 214 BETWEEN keyword, 41–42 binary classification algorithms, 185 binary classification model, 173, 176–178 binary flag field, 52–53, 177–178, 181, 190 binning, 53–56 blank, within database, 44 

###### **C** 

calculations aggregate, 103 averaging, 92 date, 116 with DATEDIFF function, 123 of distance, 214 engineered features, 180 LAG and LEAD functions for, 111 performing inside aggregate functions, 84–88 ROUND function and, 92 rounding, 22–23 of sales, 155–156 simple inline, 20–22 total spent, 87 window functions and, 97 

**255** 

**256 Index** ■ **C–C** 

CASE statement aggregate functions and, 94–96 binary flags using, 52–53, 181 binning using, 53–56 categorical encoding using, 56–59 COUNT () function within, 170 example of, 202 grouping using, 53–56 overview of, 49 summary of, 59–60 syntax of, 50–52 categorical encoding, 56–59 categorical text column, 185 classification algorithms, 176 classification model, 173, 177 clauses FROM, 66, 80 ON, 197–198 FROM, 199 WITH clause analytical dataset and, 149–153 defined, 124–125 example of, 162 exercise using, 190 ROW_NUMBER window function and, 183 subquery using, 248 use of, 151, 161, 164, 168, 204–205, 209 HAVING clause example of, 125 exercise using, 244–245 filtering with, 93 GROUP BY statement and, 93 syntax of, 16, 80 use of, 132 LIMIT, 16–17, 19, 25, 26 ORDER BY clause within CONCAT function, 24–25 example of, 85, 140 LIMIT clause and, 19 location of, 32 NTILE groups and, 103 within the partition, 98 PARTITION BY window function and, 107–108 sort order specification within, 108 sorting column and, 100 sorting results using, 18–20 SUM window function and, 106–107 syntax of, 16, 29–30, 80 RANGE, 111 SELECT, 16 TOP, 17 WHERE clause condition of, 87 date filtering in, 93 

defined, 100 differences between, 161 error from, 101 example of, 70 exercise using, 241 filtering uses within, 41–44, 84, 197 location of, 32 multi- column conditional filtering within, 40–41 multiple condition filtering within, 34–40 overview of, 31 querying databases using, 17 removing, 141, 166 row removal using, 122 ROW_NUMBER () window function to, 184–185 syntax of, 16, 80, 233, 234 TOP clause and, 17 COALESCE function, 199 Cognos, 79 column alias of, 65–66 categorical text, 185 defined, 3–4 demonstration, 182 as dummy variables, 57 engineered features of, 180 input, 13 listing, 18 multi conditional filtering, 40–41 one- hot encoded flag, 185 selecting, 16–18 sorting, 100 timestamp, 232 value possibilities within, 131–133 comment out code, 231 Common Table Expression (CTE) analytical dataset and, 149–153 WITH clause and, 161, 164, 204–205, 209 creation of, 179 defined, 124–125 exercise using, 190 select from, 216 subquery of, 180 summary of, 226–227 UNION queries and, 160–161 comparison operator, 163 CONCAT function, 24–26, 114 concatenating strings, 24–26 concatenation parameters, 25 conditional filtering, multi- column, 40–41 conditional statements, 33 Coordinated Universal Time (UTC), 232 COUNT DISTINCT function, 90–91, 120, 183 COUNT () function, 80–81, 90–91, 102, 170 

**Index** ■ **C–D 257** 

COUNT () window function, 112, 246 COVID- 19 tracking dashboard, 163 CREATE TABLE statement, 230, 232 CREATE VIEW AS statement, 151 crow’s feet symbol, 62 CURDATE () function, 121, 126, 247 CURRENT_DATE function, 121 CURRENT_TIMESTAMP function, 232, 238 customer table calculations within, 20–22 columns within, 24–26 demographic data and, 211–217 example of, 59 exercises for, 30 joining with, 86–87, 211 IN keyword within, 42–43 LIMIT clause and, 26–29 new _versus_ returning counting, 167–171 WHERE clause within, 33–38, 40–41 customer_purchases table calculated views within, 154–155 WITH clause and, 167–171 custom analytical datasets within, 149–153 demographic data and, 211–217 example using, 80–81, 82–86, 120–125, 193, 194–196, 204–208 exercise of, 126, 142 feature engineering and, 186–188 feature set and, 181–185 GROUP BY clause and, 179–181 joining with, 71–74, 94 market_date_info table and, 174–175 sales tracking within, 146–148 vendor_inventory table and, 136–142 

**D** dashboard, 141, 163 data, 1, 7–9, 10–11, 174, 211 data leakage, 181 data point, 13 data sources, 1–3, 9–11 data warehouses, 7–9 database defined, 4 direct connection to, 3 doctor’s office, 4–6, 8–9 exercises for, 13, 30, 47, 76–77, 96, 111–112 inserting rows within, 233–236 relational, 3–7 relationships, 61–71 star schema, 7, 8 tables, relationship between, 4 types of, 11 updating values within, 10, 233–236 Database (Oracle), 2 

database administrators (DBAs), 9 dataset analytical, 144–157 for binary classification, 176–178 creating, 178–181 defined, 144 for predictive models, 113 refreshing of, 228 storing, 229–232 for time series model, 174–176 within time- series analysis, 113 for weather classification model, 174 date codes for, 114–115 counting within, 167–171 exercise using, 171 exploring changes within, 134–135 filtering to, 93 greater- than sign within, 182 maximum values of, 133 minimum values of, 133 setting field values for, 114–115 summary of, 145–146, 174–175 training data error and, 186 date filter, 166 DATE () function, 115–116 date functions, 119–125 DATE_ADD function, 116–118 DATEDIFF function, 118, 121, 123, 124 DATE_FORMAT function, 115 DATE_PART function, 115–116 DATE_SUB function, 116–118 datetime_demo table, 118 Daylight Savings Time, 232 DAYNAME () function, 126, 142, 147, 247 DELETE FROM statement, 233 demographic data, sources for, 211 demonstration column, 182 DENSE RANK () window function, 101–102 DENSE_RANK () function, 245 DESC function, 128 DESC (descending) keyword, 18–19 DESCRIBE function, 128, 132 detectable patterns, 181 dimension, 8, 144 dimension table, 8 dimensional data warehouses, 7–9 dimensional model, 9 dimensional modeling techniques, 7 distance, calculation of, 214 DISTINCT keyword duplicate removal using, 122 example of, 131 use of, 73, 82–83, 168, 183 doctor’s office database, 4–6, 8–9 

**258 Index** ■ **D–F** 

DROP TABLE statement, 230–231 dummy variable, 57 duplicates, removing of, 122 dynamic date ranges, 113 dynamic list of values, 46 

###### **E** 

Eastern Standard Time, 232 edge cases, 27–28 editing, in SQL, 2–3 ELSE statement, 50, 56 encoding, categorical, 56–59 engineered features, 180 entity, 3 entity- relationship diagram (ERD), 5, 62 ETL engineers, 9 event logs, 162 Excel (Microsoft), 1–2 Exploratory Data Analysis (EDA) alias within, 130 column value possibilities within, 131–133 demonstrating of, 128 exploring changes over time within, 134–135 multiple table exploring within, 135–138 within the predictive modeling process, 127 process of, 189 sales _versus_ inventory within, 138–142 use of, 11 exponential smoothing, 175–176 EXTRACT () function, 115–116, 247 

###### **F** 

fact, 8 fact table, 8 FALSE evaluation, 33, 34–40 Farmer’s Market Database, introduction to, 11–12. _See also specific tables_ feature, 13 feature engineering, 185–188, 189 feature set, expanding, 181–185 feature vectors, 173 field, 3–4 field values, for date/time, 114–115 filtering ON clause, 197–198 date, 93 front- end, 88 within HAVING clause, 93 JOIN statement, 71–74 BETWEEN keyword, 41–42 IN keyword, 42–43 LIKE keyword, 43 multi- column conditional, 40–41 multiple conditions, 34–40 

NULL value, 44–46, 71–72 removing, 166 from SELECT statement, 32–34 with a subquery, 104–105 using subqueries, 46–47 ways to, 41–44 WHERE clause and, 122 flags, binary, 52–53, 177–178, 181, 190 follow- up questions, anticipation of, 144–145 forecasting functions, 175–176 foreign key, 5 FROM clause, 66, 80, 199 FROM statement, 16, 17, 29–30, 32 front- end filtering, 88 functions. _See also_ window functions AVG (average), 91–93, 97, 103–104 COALESCE, 199 CONCAT, 24–26, 114 COUNT (), 80–81, 90–91, 102, 170 COUNT DISTINCT, 90–91, 120, 183 CURDATE (), 121, 126, 247 CURRENT_DATE, 121 CURRENT_TIMESTAMP, 238 DATE (), 115–116 DATE_ADD, 116–118 DATEDIFF, 118, 121, 123, 124 DATE_FORMAT, 115 DATE_PART, 115–116 DATE_SUB, 116–118 DAYNAME (), 126, 142, 147, 247 DENSE_RANK (), 245 DESC, 128 DESCRIBE, 128, 132 GETDATE, 121 LAG, 108–111, 121–122, 209, 246 LEAD, 108–111, 123, 124 LOWER, 51 MAX () DATEDIFF function and, 121 example of, 120, 140 exercise using, 252 overview of, 88–90 use of, 163, 165, 199 MIN (), 88–90, 120, 121, 140, 167–168 NTILE, 102–103, 224–225 ROUND, 22–23 ROUND function COALESCE function and, 199 defined, 97 example of, 87, 104–105, 108 use of, 22–23, 92 SQL, defined, 22 STR_TO_DATE, 114, 115 SYSDATE, 121 TIME (), 115–116 

**Index** ■ **F–K 259** 

TIMESTAMPDIFF, 119 TODAY, 121 TRIM, 44 UPPER, 25, 51 WEEK, 147 YEAR, 147 

###### **G** 

GETDATE function, 121 grain, 9 granularity within aggregation, 138 changing of, 189 choosing of, 145 of customer_purchases table, 81 for forecasting, 176 table, 129 with target variable, 178–179 understanding, 10, 82 graphical use interface (GUI), 2–3 greater- than sign, 182 Greenwich Mean Time, 232 GROUP BY clause COUNT function and, 90 defined, 97 example of, 84, 85, 95–96, 110, 216 HAVING clause and, 93, 125 ROW_NUMBER window function and, 183 within summary, 145 syntax of, 16, 79–80 use of, 161, 165, 174–175 group summaries, displaying, 80–83 grouping, continuous values with CASE statements, 53–56 

###### **H** 

hard- coded list of values, within IN keyword, 46 HAVING clause example of, 125 exercise using, 244–245 filtering with, 93 GROUP BY statement and, 93 syntax of, 16, 80 use of, 132 heart disease classification model, 173 histogram, 11, 141–142 human- readable report labels, joining within, 144 

###### **I** 

IBM DB2, 2 "IF" statements, 31 IN keyword, 42–43, 46, 241 

infinity symbol, 62 inline calculations, 20–23, 24–26 INNER JOIN, 68–71, 76, 194, 243 inner subquery, 100 input column, 13 input parameters, 22–23 input variable, 13 INSERT INTO SELECT statement, 233 INSERT statement, 233 inside scripts, 236–237 instance, 13, 173 integer overflow, 119 Integrated Development Environment (IDE), 2–3 inventory, sales _versus,_ 138–142 IS NULL keyword, 44 

###### **J** 

JOIN statement aggregation using, 86 ON clause, 197–198 database relationships and, 61–71 error within, 164 example of, 94, 166 exercises for, 77, 243, 248–249 filtering pitfalls within, 71–74 INNER JOIN, 68–71, 76, 194, 243 LEFT JOIN example of, 74–76, 87, 139, 148, 166 exercises for, 77, 243, 248–249 filtering pitfalls within, 71–74 overview of, 63–67 lookup tables and, 140 of multiple tables, 74–76 RIGHT JOIN, 67–68, 139, 194–197 self- joining, 163–167 Jupyter notebook, 127 

###### **K** 

keywords AS, 21, 22, 66, 149 BETWEEN, 41–42 IN, 42–43, 46, 241 AS, 66, 149 ASC (ascending), 18–19 defined, 15 DESC (descending), 18–19 DISTINCT duplicate removal using, 122 example of, 131 use of, 73, 82–83, 168, 183 IS NULL, 44 LIKE, 43, 52 NOT IN, 241 

**260 Index** ■ **L–P** 

###### **L** 

LAG function, 108–111, 121–122, 209, 246 latitudes, distance calculation of, 214 LEAD function, 108–111, 123, 124 LEFT JOIN example of, 74–76, 87, 139, 148, 166 exercises for, 77, 243, 248–249 filtering pitfalls within, 71–74 overview of, 63–67 less- than sign, 182 LIKE keyword, 43, 52 likelihood score, 177 LIMIT clause, 16–17, 19, 25, 26–27 line chart, 175–176 longitudes, distance calculation of, 214 lookup tables, 140 LOWER function, 51 

###### **M** 

machine learning, dataset terminology, 12–13 machine learning algorithm, 13 machine learning applications, 230 many- to- many relationship, 6 market_date_info table binary flags within, 52–53 customer_purchases table and, 174–175 datetime field values within, 114–118 example using, 220 exercise of, 126 filtering within, 46–47 UNION query within, 159–160 market_vendor_inventory table, 160–161 materialized view, 230 MAX () function DATEDIFF function and, 121 example of, 120, 140 exercise using, 252 overview of, 88–90 use of, 163, 165, 199 measures, 8, 144 medical database table, 4–6 medical history, algorithms and, 177 Microsoft Access, 2 Microsoft Excel, 1–2 Microsoft SQL Server, 2 MIN () function, 88–90, 120, 121, 140, 167–168 modeling techniques, dimensional, 7 multiplication, 93 MySQL Workbench Community Edition, 3, 132 

###### **N** 

N symbol, 62 negative correlation, of variables, 192 NOT IN keyword, 241 NOT operator, 241 NTILE window function, 102–103, 224–225 NULL value within ascending order, 18 CASE statement and, 50 COALESCE function and, 199 defined, 5 as edge cases, 27–28 example of, 123 filtering of, 71–72 IS NULL keyword, 44–46 within STR_TO_DATE function, 115 warning regarding, 44–46 numeric inputs, for binary classification algorithms, 185 numeric price output, 33 

###### **O** 

observations, 173 ODBC (Open Database Connectivity), 3 ON clause, 197–198 one- hot encoded flag column, 185 one- hot encoding, 57–59 one- to- many relationship, 5, 62, 63 Open Database Connectivity (ODBC), 3 OR operator, 34, 38 Oracle Database, 2, 111, 115, 119 ORDER BY clause within CONCAT function, 24–25 example of, 85, 140 LIMIT clause and, 19 location of, 32 NTILE groups and, 103 within the partition, 98 PARTITION BY window function and, 107–108 sort order specification within, 108 sorting column and, 100 sorting results using, 18–20 SUM window function and, 106–107 syntax of, 16, 29–30, 80 outer subquery, 100, 122 output, query, evaluating, 26–29 

###### **P** 

pandas package (Python), 189 parameters, 22–23, 25 parentheses symbol, 22–23 partition, 105, 168 

**Index** ■ **P–S 261** 

PARTITION BY window function, 98, 101, 107–108 passing example rows of data, training by, 173 percent symbol, 43 positive correlation, of variables, 192 PostgreSQL, 2, 111 predictive modeling, 113, 127, 144, 186 price, formatting, 33 primary key, 5, 132 probability score, from algorithms, 177 product table example of, 17, 18 exercise of, 77, 142 exercises for, 60 exploring, 128–131 IS NULL keyword within, 44–46 joining with, 61–71, 94 LIMIT clause and, 17 output comparison within, 39–40 possible column values within, 131–133 snapshot from, 231 sorting within, 19 UNION query within, 160–161, 162 WHERE clause within, 32, 39–40 product_category table, 61–71, 77, 129–131, 192–194 product_units table, 233–236 purchase table, 53–56 Python connecting to, 3 Exploratory Data Analysis (EDA) within, 127 packages within, 236–237 pandas package within, 189 scripting language within, 49 special characters within, 236 

###### **Q** 

query, 26–29, 100, 149, 156, 160 query_alias, 149 quotes symbol, 21, 236 

###### **R** 

R, connecting to, 3 RANGE clause, 111 RANK () window function, 100, 101–102, 121–122, 161, 162 raw data, 7 record, 3 record high to- date indicator, 163 Redshift (Amazon), 2, 115, 119 refreshing, of datasets, 228 relational database, 3–7 Relational Database Management Systems (RDBMS), 2, 5, 6, 62, 63 

reporting, ad- hoc, 143 Result Grid, 27 RIGHT JOIN, 67–68, 70, 77, 139, 194–197 ROUND function COALESCE function and, 199 defined, 97 example of, 87, 104–105, 108 use of, 22–23, 92 rounding, as inline calculation, 22–23 ROW_NUMBER () window function, 98–101, 102, 183, 184–185, 245 rows COUNT function and, 90 defined, 3 FALSE evaluation within, 33, 34–40 inserting, 233–236 LAG function and, 108 LIMIT clause and, 16–17, 26–27 limiting, 16–18 passing example of data, 173 summary within, 86–87 TRUE evaluation within, 33, 34–40 running total, SUM function as, 107–108 **S** sales affects to, 192 calculations of, 155–156 comparison of, 192 exercises regarding, 157, 171 forecasting of, 176 inventory _versus,_ 138–142 summary of, 145–146, 174–175, 211 trend comparison of, 192 variable changes and, 192 variation changes of, 211–217 saving, of queries, 156 scatterplot, 192 SELECT INTO statement, 231–232 SELECT statement, 15, 16, 29–30, 32–34, 79 self- join, to- date maximum and, 163–167 SET statement, 234 signal patterns, 181 simple inline calculations, 20–22 snapshots, storing, 230 Snowflake, 2 sort order, 19, 108 sortable value, 220 sorting column, adding, 100 special characters, escaping of, 236 SQL function, 22 SQL Server (Microsoft), 2, 17, 115, 119 SQLite, 2 star schema, 7, 8 

**262 Index** ■ **S–T** 

statements FROM, 16, 17, 29–30, 32 conditional, 33 CREATE TABLE, 230, 232 CREATE VIEW AS, 151 DELETE FROM, 233 DROP TABLE, 230–231 ELSE, 50, 56 "IF," 31 INSERT, 233 INSERT INTO SELECT, 233 JOIN statement aggregation using, 86 ON clause, 197–198 database relationships and, 61–71 error within, 164 example of, 94, 166 exercises for, 77, 243, 248–249 filtering pitfalls within, 71–74 INNER JOIN, 68–71, 76, 194, 243 LEFT JOIN, 63–67, 71–76, 77, 87, 139, 148, 166, 243, 248–249 lookup tables and, 140 of multiple tables, 74–76 RIGHT JOIN, 67–68, 139, 194–197 self- joining, 163–167 SELECT, 15, 16, 29–30, 32–34, 79 SELECT INTO, 231–232 SET, 234 THEN, 50 UPDATE, 232, 233, 234 WHEN, 50 stock prices, time series model for, 174 storage, within a dimensional model, 9 storing, dataset, 229–232 strings categorical encoding of, 56–59 concatenating, 24–26 as edge cases, 27–28 merging, 24 quotes for, 236 searching, 43 wildcard comparison of, 41 STR_TO_DATE function, 114, 115 structured data, 1 Structured Query Language (SQL), tools for connecting to, 2–3 subject matter experts (SMEs), 9–11 subquery CTE reference by, 180 defined, 100 filtering using, 46–47, 104–105 inner, 100 limiting of, 180–181 outer, 100 

use of, 122 using a WITH clause, 248 SUM () function CASE statement and, 95 COALESCE function and, 199 example of, 84, 110 ORDER BY clause of, 106–107 as running total, 107–108 use of, 80–81, 146, 163 summary COUNT function and, 80–81 of CTE, 226–227 of date, 145–146, 174–175 displaying group, 80–83 within dynamic date ranges, 113 efficiency within, 189 granularity within, 145 GROUP BY statement and, 79 within rows, 86–87 of sales, 145–146, 174–175, 211 SUM function and, 80–81 of time, 145–146 of time period, 167–171 of variables, 192 summary tables, 7 supervised learning model, 173 symbols, 16, 21, 22–23, 43, 62, 236 syntax, of SELECT query, 16 syntax- highlighting of SQL, 3 SYSDATE function, 121 **T** table alias of, 66, 89 Book, 4, 6–7, 13 connector symbols within, 62 customer table calculations within, 20–22 columns within, 24–26 demographic data and, 211–217 example of, 59 exercises for, 30 joining with, 86–87, 211 IN keyword within, 42–43 LIMIT clause and, 26–29 new _versus_ returning counting, 167–171 WHERE clause within, 33–38, 40–41 customer_purchases table calculated views within, 154–155 WITH clause and, 167–171 custom analytical datasets within, 149–153 demographic data and, 211–217 example using, 80–81, 82–86, 120–125, 193, 194–196, 204–208 exercise of, 126, 142 

**Index** ■ **T–T 263** 

feature engineering and, 186–188 feature set and, 181–185 GROUP BY clause and, 179–181 joining with, 71–74, 94 market_date_info table and, 174–175 sales tracking within, 146–148 vendor_inventory table and, 136–142 datetime_demo table, 118 dimension, 8 EDA exploring over multiple, 135–138 granularity of, 82, 129 JOINS of, 74–76, 86 lookup, 140 market_date_info table binary flags within, 52–53 customer_purchases table and, 174–175 datetime field values within, 114–118 example using, 220 exercise of, 126 filtering within, 46–47 UNION query within, 159–160 market_vendor_inventory table, 160–161 medical database, 4–6, 8–9 product table example of, 17, 18 exercise of, 77, 142 exercises for, 60 exploring, 128–131 IS NULL keyword within, 44–46 joining with, 61–71, 94 LIMIT clause and, 17 output comparison within, 39–40 possible column values within, 131–133 snapshot from, 231 sorting within, 19 UNION query within, 160–161, 162 WHERE clause within, 32, 39–40 product_category table, 61–71, 77, 129–131, 192–194 product_units table, 233–236 purchase table, 53–56 relationship between, 4 storing datasets as, 229–232 summary, 7 updating, 10 vendor table categorical encoding within, 56–59 custom analytical datasets within, 149–153 example of, 29–30, 59–60 exercise of, 76 joining with, 74–76, 86–87, 148 BETWEEN keyword within, 41–42 types within, 51 

vendor booth assignment example within, 18, 20 WHERE clause within, 41 vendor_booth_assignments table, 75–76, 108–111 vendor_inventory table aggregate window functions within, 103–108 averaging within, 92 AVG () window function within, 103–104 calculated views within, 154–155 changes over time within, 134–135 customer_purchases table and, 136–142 DENSE RANK function within, 101–102 example using, 88–89, 90–91, 132–133, 193, 194, 217–219 exercise of, 77, 142 granularity of, 132 HAVING clause within, 93–94 NTILE function within, 102–103 query from, 201–204 RANK function within, 101–102 ROUND () function within, 104–105 ROW_NUMBER () within, 98–99 UNION query within, 162 Tableau dataset into, 141 Exploratory Data Analysis (EDA) within, 127 forecasting function of, 175–176 front- end filtering within, 88 SQL into, 79, 152–153, 156–157 summary within, 145 target variable, 13, 177, 178–179 THEN statement, 50 time, 114–115, 134–135, 145–146, 167–171 time bounding, for target variables, 178 TIME () function, 115–116 time of year/season, comparison of, 192 time series model, 174–176 time zones, 116, 121, 232 time- bound predictive models, 113 time- series analysis, 113 timestamp, 115, 119, 232 TIMESTAMPDIFF function, 119 to- date maximum, 163–167 TODAY function, 121 TOP clause, 17 trained model, testing of, 173 training data, 174, 177, 186 training dataset, creating, 178–181 training example, 13 transactional data, 33 TRIM function, 44 TRUE evaluation, 33, 34–40, 42, 50, 241 tuple, 3 

**264 Index** ■ **U–Z** 

###### **U** 

UNION query, 159–163, 171 unstructured data, 1 UPDATE statement, 232, 233, 234 UPPER function, 25, 51 UTC (Coordinated Universal Time), 232 

###### **V** 

value, distribution of, 10–11 value, updating, 233–236 variables, 13, 56–59, 177, 178–179, 191–192 vendor table categorical encoding within, 56–59 custom analytical datasets within, 149–153 example of, 29–30, 59–60 exercise of, 76 joining with, 74–76, 86–87, 148 BETWEEN keyword within, 41–42 types within, 51 vendor booth assignment example within, 18, 20 WHERE clause within, 41 vendor_booth_assignments table, 75–76, 108–111 vendor_inventory table aggregate window functions within, 103–108 averaging within, 92 AVG () window function within, 103–104 calculated views within, 154–155 changes over time within, 134–135 customer_purchases table and, 136–142 DENSE RANK function within, 101–102 example using, 88–89, 90–91, 132–133, 193, 194, 217–219 exercise of, 77, 142 granularity of, 132 HAVING clause within, 93–94 NTILE function within, 102–103 query from, 201–204 RANK function within, 101–102 ROUND () function within, 104–105 ROW_NUMBER () within, 98–99 UNION query within, 162 view, 149–153, 204–205, 229–232 vw_ prefix, 151 

###### **W** 

weather classification model, 173, 174 WEEK function, 147 WHEN statement, 50 WHERE clause condition of, 87 date filtering in, 93 

defined, 100 differences between, 161 error from, 101 example of, 70 exercise using, 241 filtering uses within, 41–44, 84, 197 location of, 32 multi- column conditional filtering within, 40–41 multiple condition filtering within, 34–40 overview of, 31 querying databases using, 17 removing, 141, 166 row removal using, 122 ROW_NUMBER () window function to, 184–185 syntax of, 16, 80, 233, 234 TOP clause and, 17 wildcard character, 43 wildcard comparison, 41 window functions. _See also_ functions aggregate, 103–108 COUNT (), 112, 246 date functions within, 119–125 defined, 97 DENSE RANK (), 101–102 NTILE, 102–103, 224–225 within outer subquery, 122 PARTITION BY, 98, 101, 107–108 partitioning by, 168 RANK (), 100, 101–102, 121–122, 161, 162 ROW_NUMBER (), 98–101, 102, 183, 184–185, 245 use examples of, 97 window naming, 111 WITH clause analytical dataset and, 149–153 defined, 124–125 example of, 162 exercise using, 190 ROW_NUMBER window function and, 183 subquery using, 248 use of, 151, 161, 164, 168, 204–205, 209 Workbench Community Edition (MySQL), 3, 132 **Y** YEAR function, 147 

###### **Z** 

Zip Code Tabulation Areas (ZCTAs), 211 

### **WILEY END USER LICENSE AGREEMENT** 

Go to www.wiley.com/go/eula to access Wiley’s ebook EULA. 

