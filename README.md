# QA-Challenge
**Summary**

This scenario is intended to demonstrate an end to end flow of a basic scenario that we regularly perform. We don't expect a 100% complete challenge. We're looking to see how you code, problem solve, and research.

Feel free to email us when you have questions at inkboxqa@getinkbox.com

**Description**

Create an automated test case for iOS/Android which contains the below scenarios:
1. Sort the products by “Featured”
2. Connect to the database (refer to dump for tables) and compare the front-end with the Best selling data in the DB*
3. Filter with Artist Lenera Solntseva
4. Visit the PDP of product “Ocean heart”
5. Add a checkpoint to make sure there aren’t any downtimes/400/500 errors on any webpage
6. Validate that the “How to apply” accordion has a video attached
7. Add “e-gift” card from Frequently purchased
8. Increment the product in cart and verify the number of products in cart match with “item(s)”
9. Click on continue to checkout


*Best selling logic to make it easier
SELECT sp.title, soi.product_id, SUM(soi.quantity) AS total_quantity, COUNT(DISTINCT soi.order_id) AS total_orders
FROM orders_items soi
LEFT JOIN products sp
ON soi.product_id = sp.product_id
WHERE DATE(first_created) >= DATE_SUB(CURRENT_DATE(), INTERVAL 30 DAY)
AND sp.product_type NOT LIKE '%custom%'
AND sp.product_type LIKE '%tattoo%'
GROUP BY sp.title, soi.product_id
ORDER BY total_quantity DESC
LIMIT 200;

