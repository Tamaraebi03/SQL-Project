
---

````md
 List of Questions + Solutions

 A. Customer Loyalty Analysis

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
| Active            | 14670         |
| Cancelled         | 2067          |

💡 **Insight:**
The loyalty program retains a strong majority of its members (~88% active), indicating good customer retention. However, the ~12% churn still represents a significant opportunity for targeted retention strategies.

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
| Canada  | 7988.90 |

💡 **Insight:**
Since all customers are from Canada, the dataset lacks geographic diversity. Future analysis could benefit from multi-country data to uncover regional performance differences.

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
| Female | 8410          | 50.25      |
| Male   | 8327          | 49.75      |

💡 **Insight:**
The gender distribution is nearly equal, meaning marketing strategies can remain gender-neutral without heavily favoring one group.

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
| 2012            | 1686              |
| 2013            | 2397              |
| 2014            | 2370              |
| 2015            | 2331              |
| 2016            | 2456              |

💡 **Insight:**
Enrollment increased significantly after 2012 and stabilized in later years, suggesting successful acquisition campaigns followed by consistent program awareness.

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
| -------------------- | ------- |
| Bachelor             | 8206.99 |
| Doctor               | 7832.92 |
| High School or Below | 7707.08 |
| College              | 7594.57 |
| Master               | 7440.62 |

💡 **Insight:**
Customers with a Bachelor’s degree generate the highest value, suggesting this segment may have stronger purchasing power or engagement with the loyalty program.

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
| 79245.61   | 7988.90 |

💡 **Insight:**
While the average salary is relatively high, CLV is much lower, suggesting that higher income does not directly translate into proportional spending within the loyalty program.

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

| City    | active_members |
| ------- | -------------- |
| Toronto | 2940           |

💡 **Insight:**
Toronto leads in active members, likely due to population size or stronger brand presence. This city is a key market for retention and upselling strategies.

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
| Standard        | 15766         | 7985.35 |

💡 **Insight:**
The Standard enrollment dominates, indicating most users join without promotions. However, analyzing promotional enrollments could reveal opportunities to boost engagement.

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
| 2018              | 645                 |
| 2017              | 506                 |
| 2016              | 427                 |

💡 **Insight:**
Cancellations peaked in 2018, which may indicate dissatisfaction, market competition, or policy changes during that period.

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
| Divorced       | 8200.69 |
| Married        | 8058.20 |
| Single         | 7719.49 |

💡 **Insight:**
Divorced and married customers show higher CLV than singles, possibly due to more stable income or higher spending patterns.

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

| Education            | Enrollment Type | total_members |
| -------------------- | --------------- | ------------- |
| Bachelor             | Standard        | 9843          |
| College              | Standard        | 4000          |
| High School or Below | Standard        | 732           |

💡 **Insight:**
Most members with a Bachelor’s degree enroll through the Standard type, reinforcing that this group dominates the program and should be a key focus segment.

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
| 1.27                    |

💡 **Insight:**
Customers typically leave after just over a year, indicating a short retention window. Early engagement strategies are critical to improving long-term loyalty.

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
| 12                 | 213                 |
| 11                 | 212                 |
| 8                  | 208                 |

💡 **Insight:**
Cancellations peak toward the end of the year, suggesting seasonal churn—possibly due to financial pressures, subscription reviews, or expiring benefits.

<br>
```

---

