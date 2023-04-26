---
tags: [Learning]
title: Databse Design Considerations
created: '2023-04-24T05:45:03.602Z'
modified: '2023-04-24T10:05:13.247Z'
---

# Databse Design Considerations

## The design process `ref Microsoft`

- Determine the purpose of your database    

  This helps prepare you for the remaining steps.

- Find and organize the information required     

  Gather all of the types of information you might want to record in the database, such as product name and order number.

- Divide the information into tables    

  Divide your information items into major entities or subjects, such as Products or Orders. Each subject then becomes a table.

- Turn information items into columns    

  Decide what information you want to store in each table. Each item becomes a field, and is displayed as a column in the table. For example, an Employees table might include fields such as Last Name and Hire Date.

- Specify primary keys    

  Choose each table’s primary key. The primary key is a column that is used to uniquely identify each row. An example might be Product ID or Order ID.

- Set up the table relationships    

  Look at each table and decide how the data in one table is related to the data in other tables. Add fields to tables or create new tables to clarify the relationships, as necessary.

- Refine your design    

  Analyze your design for errors. Create the tables and add a few records of sample data. See if you can get the results you want from your tables. Make adjustments to the design, as needed.

- Apply the normalization rules    

  Apply the data normalization rules to see if your tables are structured correctly. Make adjustments to the tables, as needed.

## Normlisation

 Apply the data normalization rules (sometimes just called normalization rules) as the next step in your design. You use these rules to see if your tables are structured correctly. The process of applying the rules to your database design is called normalizing the database, or just normalization.

**First Normal Form (1NF):** A table is in 1NF if and only if all the values in each column of the table are atomic, meaning they cannot be decomposed further. In other words, every column should contain only one value per row, and each value should be of the same data type.

**Second Normal Form (2NF):** A table is in 2NF if it is in 1NF and every non-key column is fully dependent on the entire primary key, not just on part of it. This means that a table should not have any partial dependencies, which occur when a non-key attribute depends on only a portion of the primary key.

**Third Normal Form (3NF):** A table is in 3NF if it is in 2NF and has no transitive dependencies, meaning that a non-key column cannot be dependent on another non-key column. This can be achieved by removing columns that are not fully dependent on the primary key and placing them in separate tables.

### 1 NF

- Eliminate duplicative columns from the same table.
- Create separate tables for each group of related data and identify each row with a
unique column or set of columns (the primary key).

```
A relation is in first normal form if ... none of its domains has elements which are
themselves sets. An unnormalized relation is one which is not in first normal form.
                                                            - E.F. Codd (Who Introduced 1NF)
```

**Violation of 1NF**

| Supplier | Product    |
|----------|------------| 
| S2       | P1, P2     |
| S1       | P2, P4,P5  |
| S3       | -          |

**1NF Applied**
| Supplier | Product    |
|----------|------------| 
| S2       | P1         |
| S2       | P2         |
| S1       | P2         |
| S1       | P4         |
| S1       | P5         |

**Violation of 1NF**

| OrderID | CustomerName | Product1 | Quantity1 | Product2 | Quantity2 |
| -------|--------------|---------|-----------|---------|-----------|
| 1001   | John Smith   | T-Shirt | 2         | Jeans   | 1         |
| 1002   | Jane Doe     | Hat     | 1         | T-Shirt | 3         |
| 1003   | Tom Johnson  | Jeans   | 2         | Shoes   | 1         |

In this table, you can see that the columns "Product1" and "Quantity1" represent the first product and its quantity for each order, while "Product2" and "Quantity2" represent the second product and its quantity, respectively. This table violates the 1NF because it has repeating groups of columns for each product, which can make it difficult to search, sort, or aggregate data. In addition, if a customer orders more than two products, you will need to add more columns, which can lead to a lot of empty or null values.

To comply with the 1NF, it would be better to split the orders into separate rows and store the product and quantity values in separate tables with a one-to-many relationship to the main order table.

### 2 NF `Remove Partial Dependency`

Partial dependency is a concept in database normalization that occurs when a non-key attribute in a table depends on only a part of the primary key instead of the entire key. In other words, the value of a non-key attribute is determined by a subset of the primary key instead of the entire primary key.

Suppose we have a database for a library that keeps track of books, authors, and publishers. We have the following tables:

1. Book (book_id, book_title, author_id, publisher_id, year_published)
2. Author (author_id, author_name, author_birthdate, author_nationality)
3. Publisher (publisher_id, publisher_name, publisher_city, publisher_country)

The Book table has the following dependencies:

- book_id -> book_title, author_id, publisher_id, year_published
- author_id -> author_name, author_birthdate, author_nationality
- publisher_id -> publisher_name, publisher_city, publisher_country

The book_id is the primary key of the Book table, and the author_id and publisher_id are foreign keys that reference the Author and Publisher tables respectively. 

However, the Book table is not in 2NF because the book_title, year_published, author_name, author_birthdate, author_nationality, publisher_name, publisher_city, and publisher_country are all dependent on the book_id. This means that there is a partial dependency, where only part of the primary key determines these attributes. 

To convert the Book table to 2NF, we need to split it into two tables:

1. Book (book_id, book_title, author_id, publisher_id)
2. Book_Details (book_id, year_published)

In this new design, the Book table has the primary key book_id, and the foreign keys author_id and publisher_id reference the Author and Publisher tables respectively. The Book_Details table has the composite key (book_id, year_published) and contains additional details about the book. 

Now, the attributes in each table are dependent on the entire primary key, so there are no partial dependencies. This satisfies the requirements for 2NF.

### 3NF `Remove Transitive Dependency`

To achieve 3NF, a table must first satisfy the requirements of 1NF and 2NF. Additionally, every non-key attribute in the table must be directly dependent on the primary key, and not transitively dependent.

## Data Type Evluation 

- Check whether we've applied a right data type for colums that ensures data integerity and consistency.
- Try to optimize the data storage need for column `(use TinyInt if instead of BIGINT if suits)`

## Indexing based on business needs.

1. Identify the columns that are frequently used in queries: Start by analyzing the queries that are commonly used in your application to identify the columns that are frequently accessed. These columns are good candidates for indexing.

2. Determine the appropriate type of index: There are several types of indexes, including clustered indexes, non-clustered indexes, and full-text indexes. Determine which type of index is appropriate for the columns you want to index based on their data type and the type of queries that will be executed.

3. Test the performance: After creating the index, test the performance of the queries that access the indexed columns to ensure that the index is providing the desired performance benefits. we may need to experiment with different types of indexes or indexing strategies to find the optimal solution for your database.





