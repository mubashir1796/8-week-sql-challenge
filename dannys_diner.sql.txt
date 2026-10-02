-- Danny's Diner
-- Case Study Questions


-- 1. What is the total amount each customer spent at the restaurant?
SELECT
    sales.customer_id,
    SUM(menu.price)
FROM dannys_diner.sales
JOIN dannys_diner.menu
    ON sales.product_id = menu.product_id
GROUP BY sales.customer_id;


-- 2. How many days has each customer visited the restaurant?
SELECT
    customer_id,
    COUNT(DISTINCT order_date) AS visit_days
FROM dannys_diner.sales
GROUP BY customer_id;


-- 3. What was the first item from the menu purchased by each customer?
SELECT DISTINCT
    s.customer_id,
    m.product_name
FROM dannys_diner.sales AS s
JOIN dannys_diner.menu AS m
    ON s.product_id = m.product_id
WHERE s.order_date = (
    SELECT MIN(s2.order_date)
    FROM dannys_diner.sales AS s2
    WHERE s2.customer_id = s.customer_id
);


-- 4. What is the most purchased item on the menu and how many times was it purchased by all customers?
SELECT
    m.product_name,
    COUNT(*) AS purchase_count
FROM dannys_diner.sales AS s
JOIN dannys_diner.menu AS m
    ON s.product_id = m.product_id
GROUP BY m.product_name
ORDER BY purchase_count DESC
LIMIT 1;


-- 5. Which item was the most popular for each customer?
SELECT
    s.customer_id,
    menu.product_name
FROM dannys_diner.sales AS s
JOIN dannys_diner.members AS m
    ON s.customer_id = m.customer_id
JOIN dannys_diner.menu AS menu
    ON s.product_id = menu.product_id
WHERE s.order_date = (
    SELECT MIN(s2.order_date)
    FROM dannys_diner.sales AS s2
    WHERE s2.customer_id = s.customer_id
      AND s2.order_date >= m.join_date
);


-- 6. Which item was purchased first by the customer after they became a member?
SELECT
    s.customer_id,
    menu.product_name
FROM dannys_diner.sales AS s
JOIN dannys_diner.members AS m
    ON s.customer_id = m.customer_id
JOIN dannys_diner.menu AS menu
    ON s.product_id = menu.product_id
WHERE s.order_date = (
    SELECT MIN(s2.order_date)
    FROM dannys_diner.sales AS s2
    WHERE s2.customer_id = s.customer_id
      AND s2.order_date >= m.join_date
);


-- 7. Which item was purchased just before the customer became a member?
SELECT
    s.customer_id,
    m.product_name
FROM dannys_diner.sales AS s
JOIN dannys_diner.members AS mem
    ON s.customer_id = mem.customer_id
JOIN dannys_diner.menu AS m
    ON s.product_id = m.product_id
WHERE s.order_date = (
    SELECT MAX(s2.order_date)
    FROM dannys_diner.sales AS s2
    WHERE s2.customer_id = s.customer_id
      AND s2.order_date < mem.join_date
);


-- 8. What is the total items and amount spent for each member before they became a member?
SELECT
    s.customer_id,
    COUNT(*) AS total_items,
    SUM(menu.price) AS total_spent
FROM dannys_diner.sales AS s
JOIN dannys_diner.members AS mem
    ON s.customer_id = mem.customer_id
JOIN dannys_diner.menu AS menu
    ON s.product_id = menu.product_id
WHERE s.order_date < mem.join_date
GROUP BY s.customer_id;


-- 9.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
SELECT
    s.customer_id,
    SUM(
        CASE
            WHEN m.product_name = 'sushi' THEN m.price * 20
            ELSE m.price * 10
        END
    ) AS total_points
FROM dannys_diner.sales AS s
JOIN dannys_diner.menu AS m
    ON s.product_id = m.product_id
GROUP BY s.customer_id;


-- 10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?
SELECT
    s.customer_id,
    SUM(
        CASE
            WHEN s.order_date BETWEEN mem.join_date
                                  AND mem.join_date + INTERVAL '6 days'
                THEN menu.price * 20
            WHEN menu.product_name = 'sushi'
                THEN menu.price * 20
            ELSE menu.price * 10
        END
    ) AS total_points
FROM dannys_diner.sales AS s
JOIN dannys_diner.members AS mem
    ON s.customer_id = mem.customer_id
JOIN dannys_diner.menu AS menu
    ON s.product_id = menu.product_id
WHERE s.customer_id IN ('A', 'B')
  AND s.order_date <= '2021-01-31'
GROUP BY s.customer_id;