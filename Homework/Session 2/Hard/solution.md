SELECT COUNT(*) AS payment_count
FROM (
    SELECT t1.transaction_id
    FROM transactions t1
    JOIN transactions t2
      ON t1.merchant_id = t2.merchant_id
     AND t1.credit_card_id = t2.credit_card_id
     AND t1.amount = t2.amount
     AND t1.transaction_timestamp > t2.transaction_timestamp
     AND t1.transaction_timestamp <= t2.transaction_timestamp + INTERVAL '10 minute'
) repeated;