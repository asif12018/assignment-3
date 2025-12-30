

# Vehicle Rental System – SQL Queries

This repository contains **SQL query problems and their solutions** for a simple **Vehicle Rental System** database.
The queries demonstrate common SQL concepts such as joins, filtering, subqueries, grouping, and aggregation.

---

##  Database Tables Used for Queries

* `users` – Stores customer information and admin information
* `vehicles` – Stores vehicle details and availability information
* `bookings` – Stores booking records linking users and vehicles information

---

##  Query Problems and Solutions

---

### 1️ Retrieve Booking Information with Customer and Vehicle Details

**Requirement**
Retrieve booking information along with:

* Customer name
* Vehicle name

**Concepts Used:** `INNER JOIN`

**Solution**
This query joins the `bookings`, `users`, and `vehicles` information tables to display booking details along with customer and vehicle information.

```sql
SELECT
  b.booking_id,
  u.name AS customer_name,
  v.name AS vehicle_name,
  b.start_date,
  b.end_date,
  b.status
FROM bookings AS b
INNER JOIN users AS u ON b.user_id = u.user_id
INNER JOIN vehicles AS v ON b.vehicle_id = v.vehicle_id;
```

---

###  Find All Vehicles That Have Never Been Booked

**Requirement**
Retrieve vehicles information that have no booking history.

**Concepts Used:** `NOT EXISTS`

**Solution**
This query checks for vehicles that do not appear in the `bookings` table.

```sql
SELECT *
FROM vehicles AS v
WHERE NOT EXISTS (
  SELECT 1
  FROM bookings AS b
  WHERE b.vehicle_id = v.vehicle_id
);
```

---

###  Retrieve All Available Vehicles of a Specific Type

**Requirement**
Find all vehicles that are:

* Available
* Of a specific type (e.g., car, bike, truck)

**Concepts Used:** `SELECT`, `WHERE`

**Solution**
This query filters vehicles based on availability status and type.

```sql
SELECT *
FROM vehicles
WHERE status = 'available'
AND type = 'car';
```

---

###  Find Vehicles with More Than 2 Bookings

**Requirement**
Find the total number of bookings for each vehicle and display only those vehicles that have more than 2 bookings.

**Concepts Used:** `GROUP BY`, `HAVING`, `COUNT`

**Solution**
This query groups bookings by vehicle and filters vehicles with more than two bookings.

```sql
SELECT
  v.name AS vehicle_name,
  COUNT(b.booking_id) AS total_bookings
FROM vehicles AS v
JOIN bookings AS b ON v.vehicle_id = b.vehicle_id
GROUP BY v.name
HAVING COUNT(b.booking_id) > 2;
```

---

## Notes

* All queries are written for **PostgreSQL**
* Naming conventions follow clarity and readability
* Queries are suitable for **learning, interviews, and practice**

---

##  License

This project is for educational purposes.


