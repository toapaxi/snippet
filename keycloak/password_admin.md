con esto cambio la clave del usuario admin a mami2016
```cmd
cambiar 
ue.realm_id = '80fc85cf-2400-4039-b8b2-5f624d2498c9'
Y ue.username = 'admin'
```

```sql
UPDATE credential c
SET
    credential_data = '{"hashIterations":27500,"algorithm":"pbkdf2-sha256","additionalParameters":{}}',
    secret_data     = '{"value":"5yipaMdgPH6L5NiVQMtweERRLp26Bo0jmLKfDv8iF9dqzd/K01TFy0dPx6lAi5vwS0MEFkuBmJpQGAMOESpsAw==","salt":"SlgdRdVcfOS2NV26A4F0vw==","additionalParameters":{}}'
WHERE c.id = (
    SELECT c2.id
    FROM user_entity ue
    JOIN credential c2
        ON c2.user_id = ue.id
    WHERE ue.realm_id = '80fc85cf-2400-4039-b8b2-5f624d2498c9'
      AND ue.username = 'admin'
      AND c2.type = 'password'
);
```
