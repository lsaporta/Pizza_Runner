# Pizza_Runner: Runner and Customer Experience #



## Project Background ? ##

###### Goal 1: Uberize pizza delivery. 

###### Goal 2: Recruit 'runners' who transport and deliver the orders of customers 

###### Goal 3: Recruit a team of developers who'll develop an app where potential consumers can place orders. 



# Data And Tables Introduction: 


## Table A: Runners 

| runner_id | registration_date        |
|-----------|--------------------------|
| 1         | 2021-01-01T00:00:00.000Z |
| 2         | 2021-01-03T00:00:00.000Z |
| 3         | 2021-01-08T00:00:00.000Z |
| 4         | 2021-01-15T00:00:00.000Z |

###### The first table showcases each runner (runner_id) and their (registration_date)
###### Ex: runner 1 (runner_id 1) registered on January 1st 2021 

## Table B: Customer_Orders 

| order_id | customer_id | pizza_id | exclusions | extras | order_time               |
|----------|-------------|----------|------------|--------|--------------------------|
| 5        | 104         | 1        | null       | 1      | 2021-01-08T21:00:29.000Z |
| 6        | 101         | 2        | null       | null   | 2021-01-08T21:03:13.000Z |
| 7        | 105         | 2        | null       | 1      | 2021-01-08T21:20:29.000Z |
| 8        | 102         | 1        | null       | null   | 2021-01-09T23:54:33.000Z |
| 9        | 103         | 1        | 4          | 1, 5   | 2021-01-10T11:22:59.000Z |
| 10       | 104         | 1        | null       | null   | 2021-01-11T18:34:49.000Z |
| 10       | 104         | 1        | 2, 6       | 1, 4   | 2021-01-11T18:34:49.000Z |
| 1        | 101         | 1        | null       |        | 2021-01-01T18:05:02.000Z |
| 3        | 102         | 1        | null       |        | 2021-01-02T23:51:23.000Z |
| 3        | 102         | 2        | null       |        | 2021-01-02T23:51:23.000Z |
| 4        | 103         | 1        | 4          | null   | 2021-01-04T13:23:46.000Z |
| 4        | 103         | 1        | 4          | null   | 2021-01-04T13:23:46.000Z |
| 4        | 103         | 2        | 4          | null   | 2021-01-04T13:23:46.000Z |
| 2        | 101         | 1        | null       | null   | 2021-01-01T19:00:52.000Z |

###### This table catalogues every customer order ever sent by each customer 
###### There can be multiple records in the order_id column because customers can request multiple items per order
###### Ex: customer_id 103 ordered three items in their order. They ordered two pizza_id 1 and one of pizza_id 2 
###### Exclusions column shows the ingredients each customer requested be left out of their order 
###### Ex: customer_id 104 wanted ingredients 2 and 6 to be excluded from pizza_id 1 in thier order_id 10
###### Extras column shows the ingredients each customer requests be added to their order
###### Ex: In order_id 7, customer_id 105, requested that ingredient 1 be added to their order 

## Table C: Runners_Orders 

|   order_id  |   runner_id  |   pickup_time    |   distance  |   duration  |   cancellation  |
|-------------|--------------|------------------|-------------|-------------|-----------------|
|   5         |   3          |   1/8/21 21:10   |   10        |   15        |                 |
|   7         |   2          |   1/8/21 21:30   |   25        |   25        |   null          |
|   1         |   1          |   1/1/21 18:15   |   20        |   32        |   null          |
|   2         |   1          |   1/1/21 19:10   |   20        |   27        |   null          |
|   3         |   1          |   1/3/21 0:12    |   13        |   20        |                 |
|   8         |   2          |   1/10/21 0:15   |   23        |   15        |   null          |
|   10        |   1          |   1/11/21 18:50  |   10        |   10        |   null          |
|   4         |   2          |   1/4/21 13:53   |   23        |   40        |                 |

###### This table catalogues the runner who received each customer order and whether or not they successfully delivered it or not
###### Orders can be cancelled by either the customer or the restaurant 
###### The (distance) column shows how far in km each runner had to travel to complete each order 
###### The (duration) column shows how long each runner took to complete each order 
###### Ex: runner_id 2 received order_id 7. They traveled 25km to deliver the order, taking them 25 minutes 

## Table D: Pizza_Names

| pizza_id | pizza_name |
|----------|------------|
| 1        | Meatlovers |
| 2        | Vegetarian |

###### This table shows the item name associated with each (pizza_id)
###### Ex: Pizza_id 1 is a meatlovers pizza 

## Table E: Pizza_Recipes 

|   pizza_id  |   toppings                 |
|-------------|----------------------------|
|   1         |   1, 2, 3, 4, 5, 6, 8, 10  |
|   2         |   4, 6, 7, 9, 11, 12       |

###### This table shows the ingredients which can be added to each pizza order 
###### Ex: pizza_id 2 can have ingredients 4, 6, 7, 9, 11 and 12 added per order 

## Table F: Pizza_Toppings 

| topping_id | topping_name |
|------------|--------------|
| 1          | Bacon        |
| 2          | BBQ Sauce    |
| 3          | Beef         |
| 4          | Cheese       |
| 5          | Chicken      |
| 6          | Mushrooms    |
| 7          | Onions       |
| 8          | Pepperoni    |
| 9          | Peppers      |
| 10         | Salami       |
| 11         | Tomatoes     |
| 12         | Tomato Sauce |

###### This final table shows which ingredient or (topping_name) corresponds to each (topping_id)
###### Ex: topping_id 12 corresponds to Tomato Sauce 



# Runner And Customer Experience Situation And Goals?


## What Questions Do Any Extracted Insights And Identified Trends Aim To Answer? 

###### How well does each runner perform?
###### How long does each order take to get prepared and be successfully delivered?
###### How well do runners perform across multiple performance metrics? (Ex-avg speed, distance, time/ customer order etc) 
###### Who are the highest and lowest performing runners? 
###### How well does the current business model handle consumer orders and requests?

# Runner And Customer Experience: Business Questions


## Question 1: How many runners signed up for each one week period? 

```sql
SELECT 
      DATE_PART('week', registration_date) AS runner_week, 
      COUNT(runner_id) AS registered_runners
FROM pizza_runner.runners 
GROUP BY runner_week
ORDER BY registered_runners DESC;
```

|   runner_week  |   registered_runners  |
|----------------|-----------------------|
|   53           |   2                   |
|   1            |   1                   |
|   2            |   1                   |

###### 2 of the registered runners registered on the 53rd week of the year 

## Question 2: Which runner takes the longest on AVG to pickup each order?

```sql
WITH avg_pickup AS (
SELECT
      runner_id,
      DATE_PART('hour', pickup_time::TIMESTAMP)  AS hour, 
      DATE_PART('hour', pickup_time::TIMESTAMP) * 60 AS minutes
FROM pizza_runner.runner_orders
)
SELECT 
      DISTINCT runner_id AS runner,
      AVG(minutes) AS avg_pickuptime
FROM avg_pickup 
GROUP BY runner
ORDER BY avg_pickuptime DESC; 
```

|   runner  |   avg_pickuptime  |
|-----------|-------------------|
|   3       |   1260            |
|   1       |   825             |
|   2       |   680             |

###### runner 3 on average, takes the longest to pick up their order

## Question 3: Is there a relationship between the amount of items per order and the the time it takes to prepare? 

```sql
SELECT 
      DISTINCT customer_orders.order_id AS orders, 
      COUNT(customer_orders.order_id) AS order_counts,
      customer_orders.order_time, 
      runner_orders.pickup_time
FROM pizza_runner.customer_orders
INNER JOIN pizza_runner.runner_orders
ON customer_orders.order_id = runner_orders.order_id
GROUP BY 
        orders, 
        order_time, 
        pickup_time
ORDER BY pickup_time DESC, order_time DESC; 
```

|   orders  |   order_counts  |   order_time                |   pickup_time    |
|-----------|-----------------|-----------------------------|------------------|
|   10      |   2             |   2021-01-11T18:34:49.000Z  |   1/11/21 18:50  |
|   8       |   1             |   2021-01-09T23:54:33.000Z  |   1/10/21 0:15   |
|   7       |   1             |   2021-01-08T21:20:29.000Z  |   1/8/21 21:30   |
|   5       |   1             |   2021-01-08T21:00:29.000Z  |   1/8/21 21:10   |
|   4       |   3             |   2021-01-04T13:23:46.000Z  |   1/4/21 13:53   |
|   3       |   2             |   2021-01-02T23:51:23.000Z  |   1/3/21 0:12    |
|   2       |   1             |   2021-01-01T19:00:52.000Z  |   1/1/21 19:10   |
|   1       |   1             |   2021-01-01T18:05:02.000Z  |   1/1/21 18:15   |

###### The returns of the above query suggest that there is no noticeable correlation between the quantity of items placed per order 
###### and the duration it takes for the order to be available for pickup
###### Ex: Order 10 had two items and had the latest order_time and pickup time however, the following three records only have one item per order

## Question 4: What was the AVG distance traveled for each customer? 

```sql
WITH order_distance AS (
SELECT
      runner_orders.order_id,
      customer_orders.customer_id,
      runner_orders.distance::INTEGER AS distance_per_order
FROM pizza_runner.runner_orders
INNER JOIN pizza_runner.customer_orders
ON runner_orders.order_id = customer_orders.order_id
)
SELECT 
      DISTINCT customer_id AS purchasing_customer,
      AVG(distance_per_order) AS distance_per_buyer
FROM order_distance 
GROUP BY purchasing_customer
ORDER BY distance_per_buyer DESC; 
```

|   purchasing_customer  |   distance_per_buyer  |
|------------------------|-----------------------|
|   105                  |   25                  |
|   103                  |   23                  |
|   101                  |   20                  |
|   102                  |   16.33333333         |
|   104                  |   10                  |

###### Runners travel 25km and 23km on AVG to deliver successfuly to customer's 105 and 103 

## Question 5: What was the difference between the longest and shortest durations for customer orders?

```sql
SELECT 
      MAX(runner_orders.duration::INTEGER) AS longest_deliverytime, 
      MIN(runner_orders.duration::INTEGER) AS quickest_deliverytime, 
      MAX(runner_orders.duration::INTEGER) - MIN(runner_orders.duration::INTEGER) AS time_difference
FROM pizza_runner.runner_orders;
```

|   longest_deliverytime  |   quickest_deliverytime  |   time_difference  |
|-------------------------|--------------------------|--------------------|
|   40                    |   10                     |   30               |

###### The longest time it took to deliver an order was 40 minutes. The shortest duration was 10 minutes. 
###### The difference is 30 minutes 

## Question 6: What is the average time it takes to deliver an order in minutes, per runner? Are there any noticeable trends? 

```sql
WITH runner_speed AS (
SELECT 
      runner_id, 
      duration
FROM pizza_runner.runner_orders
)
SELECT 
      DISTINCT runner_id AS runners, 
      AVG(duration::INTEGER) AS avgrunner_time
FROM runner_speed 
GROUP BY runners 
ORDER BY avgrunner_time DESC; 
```

|   runners  |   avgrunner_time  |
|------------|-------------------|
|   2        |   26.66666667     |
|   1        |   22.25           |
|   3        |   15              |

###### Runners 2 and 3 take the longest on AVG to deliver an order

## Question 7: AVG duration in minutes for each order? Any trends regarding the runners handling the fastest and slowest orders? 

```sql 
WITH order_speed AS (
SELECT
      order_id, 
      runner_id,
      duration
FROM pizza_runner.runner_orders
)
SELECT 
      DISTINCT order_id, 
      runner_id,
      AVG(duration::INTEGER) AS avg_order_time
FROM pizza_runner.runner_orders 
GROUP BY 
        order_id, 
        runner_id
ORDER BY avg_order_time DESC; 
```

|   order_id  |   runner_id  |   avg_order_time  |
|-------------|--------------|-------------------|
|   4         |   2          |   40              |
|   1         |   1          |   32              |
|   2         |   1          |   27              |
|   7         |   2          |   25              |
|   3         |   1          |   20              |
|   5         |   3          |   15              |
|   8         |   2          |   15              |
|   10        |   1          |   10              |

###### Runner's 1 and 2 had the slowest AVG duration per order in terms of minutes

## Question 8A: For runners 1 and 2, what is the COUNT of successful deliveries?

```sql
SELECT 
      runner_id,
      COUNT(*) AS completed_delivers
FROM pizza_runner.runner_orders
WHERE cancellation = 'null'
GROUP BY runner_id
ORDER BY completed_delivers DESC; 
```

|   runner_id  |   completed_delivers  |
|--------------|-----------------------|
|   1          |   3                   |
|   2          |   2                   |

###### runner 1 has successfully completed one more delivery than runner 2 

## Questio 8 Part Two: For runners 1 and 2 what is their percentage in terms of successful deliveries? 

```sql
SELECT 
      runner_id,
      COUNT(*) AS completed_delivers, 
      COUNT(*)::NUMERIC / SUM(COUNT(*)) OVER () AS success_percentage
FROM pizza_runner.runner_orders
WHERE cancellation = 'null'
GROUP BY runner_id
ORDER BY completed_delivers DESC; 
```

|   runner_id  |   completed_delivers  |   success_percentage  |
|--------------|-----------------------|-----------------------|
|   1          |   3                   |   0.6                 |
|   2          |   2                   |   0.4                 |

###### runner 1 has the highest successful delivery percentage w/ %60 success rate 



# Conclusion: What Insights And Trends Can Be Identified?

## Runner 3 takes the longest to pick up customer orders but has the quickest delivery time
## Every customer appears to be getting served with an equal quality of service 
## Business model isn't overwhelmed with multi-item orders 
## Runners one and two appear to take the longest w/ successfully completing deliveries 



# Suggestions Going Forward?

## Closely monitor the future performance of runners 1 and 2
## Make sure that runners 1 and 2 deliver their orders quicker in the future



