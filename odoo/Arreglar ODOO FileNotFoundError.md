# ARREGLAR ODOO (FileNotFoundError: [Errno 2] No existe el archivo o el directorio:)
## '/home/muerte/.local/share/Odoo/filestore/conaplas16/2f/2f7028932480cdcb927f83b0165d577669e620fa'

```sql
select * from ir_attachment
WHERE
store_fname LIKE '%b8f9001425cfd0ef0315797909281b912817643a%'

Confirmamos la existencia de ese registro y lo borramos

delete from ir_attachment
WHERE
store_fname LIKE '%b8f9001425cfd0ef0315797909281b912817643a%'
```
