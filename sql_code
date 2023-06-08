#1 How many customers do we have each day? Are there any peak hours?

SELECT DATE(date) AS day, COUNT(*) AS Total_Orders
from pizza_sales.orders
GROUP BY day

SELECT AVG(count) AS average_count
FROM (
    SELECT COUNT(*) AS count
    FROM pizza_sales.orders
    GROUP BY DATE(date)
) AS subquery
		# We have 60 (59.6) customers per day
        
SELECT EXTRACT(HOUR FROM Time) AS Orders_Hour, COUNT(*) AS order_count
FROM pizza_sales.orders
GROUP BY Orders_Hour
ORDER BY order_count DESC
		#The peak hours for orders is between 12:00 and 13:59    23% of orders during these 2 hours
        


#2 How many pizzas are typically in an order? Do we have any bestsellers?

Select avg(total_quantity) as Avg_quan
from(
SELECT order_id, SUM(quantity) AS total_quantity
FROM pizza_sales.order_details
GROUP BY order_id
)As sub
		# We have 2 (2.3) pizzas in an order


SELECT p.pizza_type_id, SUM(od.quantity) AS total_quantity
FROM pizza_sales.order_details AS od
JOIN pizza_sales.pizzas AS p
ON od.pizza_id = p.pizza_id
GROUP BY p.pizza_type_id
ORDER BY total_quantity DESC

		#Our bestsellers are classic_dlx, bbq_ckn, hawaiian, pepperoni with 9725 sold items in 49574. The 20% of orders is from these 4 pizza types

#3 How much money did we make this year? Can we indentify any seasonality in the sales?

SELECT SUM(od.quantity) * p.price AS total_amount
FROM pizza_sales.order_details AS od
JOIN pizza_sales.pizzas AS p ON od.pizza_id = p.pizza_id
		#We made 656855.5 $ this year
        

SELECT MONTH(o.date) AS month, SUM(od.quantity) * p.price AS total_earnings
FROM pizza_sales.order_details AS od
JOIN pizza_sales.pizzas AS p ON od.pizza_id = p.pizza_id
JOIN pizza_sales.orders AS o ON od.order_id = o.order_id
GROUP BY MONTH(o.date)
ORDER BY (total_earnings) desc
		#there is no seasonility
        
#4 Are there any pizzas we should take of the menu?

# brie_carre should be taken of the menu because the sales are so low
