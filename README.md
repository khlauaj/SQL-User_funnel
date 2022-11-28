User funnel - purchase behaviour

From browse the product to purchase the product.

      WITH funnels AS (
        SELECT DISTINCT b.browse_date,
           b.user_id,
           c.user_id IS NOT NULL AS 'is_checkout',
           p.user_id IS NOT NULL AS 'is_purchase'
        FROM browse AS 'b'
        LEFT JOIN checkout AS 'c'
          ON c.user_id = b.user_id
        LEFT JOIN purchase AS 'p'
          ON p.user_id = c.user_id)
      
      SELECT COUNT(*) AS 'num_browse',
         SUM(is_checkout) AS 'num_checkout',
         SUM(is_purchase) AS 'num_purchase',
         1.0 * SUM(is_checkout) / COUNT(user_id) AS 'browse_to_checkout',
         1.0 * SUM(is_purchase) / SUM(is_checkout) AS 'checkout_to_purchase'
      FROM funnels;
      
      
 ![image](https://user-images.githubusercontent.com/39978937/204303040-7691df90-60e5-4cd0-9103-4948388ea155.png)
