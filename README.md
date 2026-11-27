# University Academic Performance Data Warehouse

This repository contains the technical presentation, Star Schema architecture, and analytical SQL queries for the **Analyzing University Performance** project, developed as part of the *Data Integration and Warehousing (DS2202)* course at Umm Al-Qura University.

## 📊 Project Overview
The project integrates multi-source educational datasets (Programs: 5,981 records; Graduates: 1,204 records; Students: 20 college records; plus unstructured student reviews) into a centralized Data Warehouse to evaluate academic performance, enrollment demand, and graduation trends across colleges.

## 🏗️ Architecture & Methodology
* **Data Cleaning & Preprocessing:** Standardized college/department names, removed duplicates, and normalized degree formats.
* **Schema Matching & Mapping:** Executed 1:1 attribute matching and mapping (`Program_Name`, `College_Name`) across disparate data sources.
* **Star Schema Design:**
  * **Fact Table:** `FACT_STUDENT_METRICS` (`Program_ID`, `Time_ID`, `Student_Count`, `Graduate_Count`)
  * **Dimension Tables:** `DIM_PROGRAM` (`Program_Name`, `College_Name`, `Degree_Level`) and `DIM_TIME` (`Academic_Year`)

## 🔍 Key Analytical SQL & OLAP Queries
1. **Highest Student Enrollment by College:**
   ```sql
   SELECT p.College_Name, SUM(f.Student_Count) AS Total_Students
   FROM FACT_STUDENT_METRICS f
   JOIN DIM_PROGRAM p ON f.Program_ID = p.Program_ID
   GROUP BY p.College_Name
   ORDER BY Total_Students DESC;
