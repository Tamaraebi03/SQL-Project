
---

````md
## List of Questions + Solutions

### `A. Customer Loyalty Analysis`

1. What is the total number of active loyalty program members compared to cancelled members?

```sql
SELECT 
    CASE 
        WHEN `Cancellation Year` IS NULL THEN 'Active'
        ELSE 'Cancelled'
    END AS membership_status,
    COUNT(*) AS total_members
FROM Customer_Loyalty_History
GROUP BY membership_status;
````

**Result Set :**

| membership_status | total_members |
| ----------------- | ------------- |
| Cancelled         | 5014         |

<br>

2. What is the average Customer Lifetime Value (CLV) for each country?

```sql
SELECT Country,
       ROUND(AVG(CLV),2) AS avg_clv
FROM Customer_Loyalty_History
GROUP BY Country
ORDER BY avg_clv DESC;
```

**Result Set :**

| Country | avg_clv |
| ------- | ------- |
| Canada  | 8397.62 |

<br>

3. What is the gender distribution of loyalty program members?

```sql
SELECT Gender,
       COUNT(*) AS total_members,
       ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM Customer_Loyalty_History),2) AS percentage
FROM Customer_Loyalty_History
GROUP BY Gender;
```

**Result Set :**

| Gender | total_members | percentage |
| ------ | ------------- | ---------- |
| Male   | 2513          | 50.12      |    
| Female | 2501          | 49.88      |

<br>

4. How has the number of enrollments changed over the years?

```sql
SELECT `Enrollment Year`,
       COUNT(*) AS total_enrollments
FROM Customer_Loyalty_History
GROUP BY `Enrollment Year`
ORDER BY `Enrollment Year`;
```

**Result Set :**

| Enrollment Year | total_enrollments |
| --------------- | ----------------- |
|      2012	      |        496        |
|      2013	      |        736        |
|      2014	      |        713        |
|      2015	      |        681        |
|      2017	      |        716        |
|      2018	      |        895        |

<br>

5. Which education level has the highest average CLV?

```sql
SELECT Education,
       ROUND(AVG(CLV),2) AS avg_clv
FROM Customer_Loyalty_History
GROUP BY Education
ORDER BY avg_clv DESC;
```

**Result Set :**

| Education            | avg_clv |
| ---------            | ------- |
| High School or Below | 8521.1
Doctor	8511.06
Bachelor	8408.12
College	8346.28
Master	8215.74  |

<br>

6. What is the average salary and how does it relate to the average CLV?

```sql
SELECT 
    ROUND(AVG(Salary),2) AS avg_salary,
    ROUND(AVG(CLV),2) AS avg_clv
FROM Customer_Loyalty_History;
```

**Result Set :**

| avg_salary | avg_clv |
| ---------- | ------- |
| XXXX       | XXXX    |

<br>

7. Which city has the highest number of active loyalty members?

```sql
SELECT City,
       COUNT(*) AS active_members
FROM Customer_Loyalty_History
WHERE `Cancellation Year` IS NULL
GROUP BY City
ORDER BY active_members DESC
LIMIT 1;
```

**Result Set :**

| City | active_members |
| ---- | -------------- |
| XXX  | XXXX           |

<br>

8. What is the most common enrollment type and its average CLV?

```sql
SELECT `Enrollment Type`,
       COUNT(*) AS total_members,
       ROUND(AVG(CLV),2) AS avg_clv
FROM Customer_Loyalty_History
GROUP BY `Enrollment Type`
ORDER BY total_members DESC
LIMIT 1;
```

**Result Set :**

| Enrollment Type | total_members | avg_clv |
| --------------- | ------------- | ------- |
| XXX             | XXXX          | XXXX    |

<br>

9. Which year had the highest number of loyalty program cancellations?

```sql
SELECT `Cancellation Year`,
       COUNT(*) AS total_cancellations
FROM Customer_Loyalty_History
WHERE `Cancellation Year` IS NOT NULL
GROUP BY `Cancellation Year`;
```

**Result Set :**

| Cancellation Year | total_cancellations |
| ----------------- | ------------------- |
| XXXX              | XXXX                |

<br>

10. What is the average CLV by marital status?

```sql
SELECT `Marital Status`,
       ROUND(AVG(CLV),2) AS avg_clv
FROM Customer_Loyalty_History
GROUP BY `Marital Status`;
```

**Result Set :**

| Marital Status | avg_clv |
| -------------- | ------- |
| XXX            | XXXX    |

<br>

11. How are loyalty program members distributed by education level and enrollment type?

```sql
SELECT Education,
       `Enrollment Type`,
       COUNT(*) AS total_members
FROM Customer_Loyalty_History
GROUP BY Education, `Enrollment Type`
ORDER BY total_members DESC;
```

**Result Set :**

| Education | Enrollment Type | total_members |
| --------- | --------------- | ------------- |
| XXX       | XXX             | XXXX          |

<br>

12. How many years, on average, does a member stay in the program before cancelling?

```sql
SELECT 
    ROUND(AVG(`Cancellation Year` - `Enrollment Year`),2) AS avg_years_before_cancel
FROM Customer_Loyalty_History
WHERE `Cancellation Year` IS NOT NULL;
```

**Result Set :**

| avg_years_before_cancel |
| ----------------------- |
| XX.XX                   |

<br>

13. Which months see the highest number of membership cancellations?

```sql
SELECT `Cancellation Month`,
       COUNT(*) AS total_cancellations
FROM Customer_Loyalty_History
WHERE `Cancellation Month` IS NOT NULL
GROUP BY `Cancellation Month`
ORDER BY total_cancellations DESC;
```

**Result Set :**

| Cancellation Month | total_cancellations |
| ------------------ | ------------------- |
| XXX                | XXXX                |

<br>
```

---

✅ This now matches your reference:

* Same **section style (`A. ...`)**
* Same **numbered questions**
* Same **SQL blocks**
* Same **Result Set tables**
* Same **spacing (`<br>`)**

---

If you want next level 🔥, I can:

* Replace the `XXXX` with **real computed outputs**
* Add **insights under each result (this impresses recruiters A LOT)**
* Or merge this into a **complete portfolio README + project structure**
