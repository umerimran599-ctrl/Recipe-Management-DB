# Recipe-Management-DB
A normalized SQL database system designed for managing culinary recipes, ingredients, and categories efficiently."
# 🍳 Cooking Recipe Database System (RecipeDB)

## 📌 Project Metadata
* **Course Name:** Database Systems Lab (CC2141L)
* **Course Instructor:** Ms. Somia Waseem
* **Program Name:** BS Computer Science[cite: 1]
* **Semester/Section:** BSCS 4, V2[cite: 1]
* **Project Evaluation Marks:** 15 Marks Max[cite: 1]
* **Associated Document:** `Semester Project DB lab (2).docx`

### 👥 Project Development Team
* Chand Farwa[cite: 1]
* Minahil Tariq[cite: 1]
* Ume Hafza[cite: 1]
* Muhammad Umer[cite: 1]

---

## 📖 Table of Contents
1. [Chapter 1: Introduction to the Problem](#1-chapter-1-introduction-to-the-problem)
   * 1.1 Introduction
   * 1.2 Purpose
   * 1.3 Objective
2. [Chapter 2: Logical Database Design](#2-chapter-2-logical-database-design)
   * 2.1 Entities & Attributes
   * 2.2 Relational Mapping & Constraints
   * 2.3 Functional Dependencies & Normalization
   * 2.4 Relational Schema Model
   * 2.5 Enhanced Entity Relationship Diagram (EERD)
3. [Chapter 3: Physical Database Design](#3-chapter-3-physical-database-design)
   * 3.1 Schema Blueprint Data Dictionary
   * 3.2 Physical Model Blueprint
4. [Chapter 4: Implementation & System Queries](#4-chapter-4-implementation--system-queries)
   * 4.1 Development Environment
   * 4.2 SQL Scripting & Architecture
   * 4.3 Advanced Queries, Views & Programming Components
5. [Chapter 5: Project Conclusion](#5-chapter-5-project-conclusion)

---

## 1. Chapter 1: Introduction to the Problem

### 1.1 Introduction
Managing and scaling culinary recipes manually leads to disorganized records and inefficient meal planning[cite: 1]. A Cooking Recipe Database solves this by digitizing and centralizing recipes, ingredients, and categories[cite: 1].

### 1.2 Purpose
The purpose is to develop a database system that allows users to seamlessly store, categorize, and retrieve cooking recipes[cite: 1].

### 1.3 Objective
The objective is to implement a normalized relational database that manages recipes and ingredients efficiently while enforcing data integrity through constraints[cite: 1].

---

## 2. Chapter 2: Logical Database Design

### 2.1 Entities & Attributes
Our relational core consists of the following key conceptual building blocks[cite: 1]:
* **Categories:** `categoryID` (Simple, Primary Key), `name` (Simple)[cite: 1]
* **Recipes:** `recipeID` (Simple, Primary Key), `title` (Simple), `instructions` (Simple)[cite: 1]
* **Ingredients:** `ingredientID` (Simple, Primary Key), `name` (Simple)[cite: 1]
* **RecipeDetails:** `quantity` (Simple)[cite: 1]

### 2.2 Relational Mapping & Constraints
* **Categories to Recipes (1:M):** One single category can house multiple food recipes, but a specific recipe belongs exclusively to one operational category[cite: 1].
* **Recipes to Ingredients (M:N):** A composite recipe requires a multitude of distinct ingredients, and conversely, a single ingredient can be utilized across various dynamic dishes[cite: 1]. This relational paradigm is effectively mapped using a bridge entity named `RecipeDetails`[cite: 1].

### 2.3 Functional Dependencies & Normalization
The attributes satisfy the following Functional Dependencies (FDs)[cite: 1]:
* $\text{categoryID} \rightarrow \text{name}$[cite: 1]
* $\text{recipeID} \rightarrow \text{title}, \text{instructions}, \text{categoryID}$[cite: 1]
* $\text{ingredientID} \rightarrow \text{name}$[cite: 1]
* $\text{recipeID}, \text{ingredientID} \rightarrow \text{quantity}$[cite: 1]

#### 🛠️ Applied Normalization Stages
To prevent data redundancy and guarantee structural consistency, the schema was progressively filtered through three major forms:
* **1st Normal Form (1NF):** Eliminated repeating groups and multi-valued variables. Every cell strictly captures atomic and completely indivisible data points[cite: 1].
* **2nd Normal Form (2NF):** Successfully transitioned into a complete 1NF state[cite: 1]. All non-key attributes are strictly and fully functionally dependent on the primary keys, removing partial functional dependencies[cite: 1].
* **3rd Normal Form (3NF):** Achieved an absolute 2NF structure with zero hidden transitive functional dependencies[cite: 1]. Non-key columns have no operational dependencies on other non-key values[cite: 1].

### 2.4 Relational Schema Model
* $\text{Categories}$ (**PK** `categoryID`, `name`)[cite: 1]
* $\text{Recipes}$ (**PK** `recipeID`, `title`, `instructions`, **FK** `categoryID`)[cite: 1]
* $\text{Ingredients}$ (**PK** `ingredientID`, `name`)[cite: 1]
* $\text{RecipeDetails}$ (**PK/FK1** `recipeID`, **PK/FK2** `ingredientID`, `quantity`)[cite: 1]

### 2.5 Enhanced Entity Relationship Diagram (EERD)
The logical structural relations are visibly mapped below:

![Logical EERD](images/eerd_logical.png)

---

## 3. Chapter 3: Physical Database Design

### 3.1 Schema Blueprint Data Dictionary

| Table | Attribute | Target Data Type | Constraints / Keys | Default Value / Properties |
| :--- | :--- | :--- | :--- | :--- |
| **Categories** | categoryID | INT | Primary Key[cite: 1] | IDENTITY(1,1), NOT NULL[cite: 1] |
| | name | VARCHAR(255)[cite: 1] | Unique[cite: 1] | NOT NULL[cite: 1] |
| **Recipes** | recipeID | INT | Primary Key[cite: 1] | IDENTITY(1,1), NOT NULL[cite: 1] |
| | title | VARCHAR(255)[cite: 1] | Index Target[cite: 1] | NOT NULL[cite: 1] |
| | instructions | VARCHAR(255)[cite: 1] | Text Descriptors | NOT NULL[cite: 1] |
| | categoryID | INT | Foreign Key[cite: 1] | REFERENCES Categories[cite: 1] |
| **Ingredients** | ingredientID | INT | Primary Key[cite: 1] | IDENTITY(1,1), NOT NULL[cite: 1] |
| | name | VARCHAR(255)[cite: 1] | Text Data[cite: 1] | NOT NULL[cite: 1] |
| | unit | VARCHAR(50)[cite: 1] | Extended Field[cite: 1] | NULL (Altered)[cite: 1] |
| **RecipeDetails**| recipeID | INT | Composite PK, FK1[cite: 1]| REFERENCES Recipes[cite: 1] |
| | ingredientID | INT | Composite PK, FK2[cite: 1]| REFERENCES Ingredients[cite: 1] |
| | quantity | INT | Numeric Value[cite: 1] | NOT NULL[cite: 1] |

### 3.2 Physical Model Blueprint
The dark-themed schema structural flow used within MySQL Workbench/MS SQL Server:

![Physical Model Diagram](images/physical_model.png)

---

## 4. Chapter 4: Implementation & System Queries

### 4.1 Development Environment
* **Primary DBMS Framework:** Microsoft SQL Server / Transact-SQL (T-SQL Scripts)[cite: 1]
* **Design & Prototyping Software:** MySQL Workbench / Visual Entity Builders[cite: 1]

### 4.2 SQL Scripting & Architecture
The structural setup script is saved cleanly in the repository inside the `schema.sql` code file. To read the database engine configuration:

```sql
CREATE DATABASE RecipeDB;
GO
USE RecipeDB;
GO

CREATE TABLE Categories (
    categoryID INT IDENTITY(1,1) PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);
GO

CREATE TABLE Recipes (
    recipeID INT IDENTITY(1,1) PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    instructions VARCHAR(255) NOT NULL,
    categoryID INT,
    FOREIGN KEY (categoryID) REFERENCES Categories(categoryID)
);
GO
ALTER TABLE Ingredients ADD unit VARCHAR(50);
GO
SELECT categoryID, COUNT(recipeID) as Total 
FROM Recipes 
WHERE title LIKE '%Cake%' 
GROUP BY categoryID 
HAVING COUNT(recipeID) > 0 
ORDER BY Total DESC;
GO
-- Inner Join Exploration
SELECT r.title, c.name FROM Recipes r INNER JOIN Categories c ON r.categoryID = c.categoryID;

-- Left Outer Join Exploration
SELECT r.title, c.name FROM Recipes r LEFT JOIN Categories c ON r.categoryID = c.categoryID;

-- Right Outer Join Exploration
SELECT r.title, c.name FROM Recipes r RIGHT JOIN Categories c ON r.categoryID = c.categoryID;
GO
CREATE VIEW RecipeView AS 
SELECT title FROM Recipes;
GO
CREATE INDEX idx_title ON Recipes(title);
GO
CREATE PROCEDURE GetRecipes
AS
BEGIN
    SELECT * FROM Recipes;
END;
GO

CREATE TRIGGER PreventZeroQty 
ON RecipeDetails
INSTEAD OF INSERT
AS
BEGIN
    INSERT INTO RecipeDetails (recipeID, ingredientID, quantity)
    SELECT 
        recipeID, 
        ingredientID, 
        CASE WHEN quantity <= 0 THEN 1 ELSE quantity END
    FROM inserted;
END;
GO
### Is se kya fayda hoga?
1. **Formatting:** Data Dictionary Table aur proper Markdown use karne se project ki look professional aayegi.
2. **Code Blocks:** SQL Code clear dikhega aur syntax highlighting active hogi.
3. **Citations:** Word document file (`Semester Project DB lab (2).docx`) ka direct metadata track maintain hoga[cite: 1].















