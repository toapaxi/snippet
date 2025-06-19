# not found in bundle web.assets_common

## Error

```log
File "/usr/lib/python3/dist-packages/odoo/addons/base/models/ir_asset.py", line 439, in _raise_not_found
    raise ValueError("File(s) %s not found in bundle %s" % (path, bundle))
ValueError: File(s) /website/static/src/scss/options/user_values.scss not found in bundle web.assets_common
```
### Verifica
```sql
select target,website_id,name, count(*) from ir_asset
group by target,website_id,name
having count(*) > 1


--resultado
"target"	"website_id"	"name"	"count"
"/website/static/src/scss/options/user_values.scss"	10	"web.assets_common: replace user_values.custom.web.assets_common.scss"	2

select target,website_id,name,* from ir_asset
where target = '/website/static/src/scss/options/user_values.scss'
and website_id = 10

--borrar el mas viejo

```
