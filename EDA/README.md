# Project description

  **What is a better plan?**

You work as an analyst for the telecommunications operator Megaline. The company offers its clients two prepaid rates, Surf and Ultimate. The commercial department wants to know which of the plans generates the most income in order to adjust the advertising budget.

You are going to perform a preliminary analysis of rates based on a relatively small selection of customers. You will have data on 500 Megaline customers: who the customers are, where they are from, what rate they use, as well as the number of calls they made and text messages they sent in 2018. Your job is to analyze customer behavior and Determine which prepaid rate generates the most revenue.

**Description of rates**

Note: Megaline rounds seconds to minutes and megabytes to gigabytes. For **calls**, each individual call is rounded up: even if the call lasted only one second, it will be counted as one minute. For **web traffic**, individual web sessions are not rounded. Instead, the month's total is rounded up. If someone uses 1025 megabytes this month, they will be charged for 2 gigabytes.

| Detalle         | **Surf** | **Ultimate** |
|-----------------|----------|----------    |
| Pago mensual    | 20 USD   | 70 USD       |
| Paquete         | 500 minutos al mes, 50 SMS y 15 GB de datos   | 3000 minutos al mes, 1000 SMS y 30 GB de datos  |
| Límite excedido | - 1 minuto: 3 centavos | - 1 minuto: 1 centavo |
|                 | - 1 SMS: 3 centavos    | - 1 SMS: 1 centavo|
|                 | - 1 GB de datos: 10 USD| - 1 GB de datos: 7 USD  |

### `users` table
Stores user data:
- *user_id* – unique user identifier
- *first_name* – user name
- *last_name* — user's last name
- *age* - user's age (in years)
- *reg_date* — subscription date (dd, mm, yy)
- *churn_date* — the date the user stopped using the service (if the value is absent, the rate was being used when this data was retrieved)
- *city* — city of residence of the user
- *plan* – rate name

### Calls table
Stores data about calls:

- *id* – unique identifier of the call
- *call_date* — call date
- *duration* - call duration (in minutes) - **These are rounded to minutes, 1 sec = 1 min**.
- *user_id* – the ID of the calling user

### `messages` table
Stores data about SMS:

- *id* – unique identifier of the SMS
- *message_date* — SMS date
- *user_id* – the identifier of the user who sent the SMS

### `internet` table
Stores data about web sessions:

- *id* – unique identifier of the session
- *mb_used* — the volume of data spent during the session (in megabytes)
- *session_date* — date of the web session
- *user_id* – user identifier

### `plans` table
Stores rate data:

- *plan_name* – rate name
- *usd_monthly_fee* — monthly payment in US dollars
- *minutes_included* — minutes included per month
- *messages_included* — SMS included per month
- *mb_per_month_included* — data included per month (in megabytes) - **These are rounded up**.
- *usd_per_minute* — price per minute after exceeding the package limits (for example, if the package includes 100 minutes the operator will charge for the 101st minute)
- *usd_per_message* — price per SMS after exceeding package limits
- *usd_per_gb* — price per gigabyte of extra data after exceeding package limits (1 GB = 1024 megabytes)

# Conclusion

1. In preparing the data, we had to understand the information that each table offered us and how these values were related to the objective we had of knowing which of the plans generated the most income. To do this, we corrected some data so that they were easy to understand. work and analyze.
2. After having the tables reviewed and clean, we group the data from each table by user and month in order to unify them into a single dataframe to have relevant and complete information in a single view. This helped us identify that there were users who exceeded the packages of minutes, messages and internet that the plans offered monthly, which would alter the monthly income of each user in each plan.
3. Next, we study the statistical distribution of user consumption and income. From this, it was concluded that the "Ultimate" plan has greater income than "Surf" solely because its cost of the plan is higher since the "Surf" plan is the one that generates greater income from additional consumption than the available contracted. . Therefore, it can be suggested to encourage these "Surf" users who exceed their consumption to migrate to the "Ultimate" plan and thus increase the income of this plan.
4. Finally, 2 two-tailed hypotheses were formulated comparing the means of 2 populations where the null hypotheses were rejected, accepting the following theses:
     - The average income of users of the Ultimate and Surf calling plans are different.
     - The average income of users in the NY-NJ area is different from users in other regions.
