# Como cambiar el resource de las personas

```sql
select name, display_name from res_users u, res_partner p
where u.partner_id = p.id
and display_name ilike '%SANDRO QUITO BERMEO%'
```
