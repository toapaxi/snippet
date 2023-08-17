## ELIMINAR MODELOS Y CAMPOS DE LOS MODELOS EN LA BASE

```sql
    --BORRAR 1 MODELO
    select * from ir_model where model  like '%transporte.tipo%';
    
    select * from ir_model_fields where model_id = '616';
    
    delete from ir_model_fields where model_id = '616';
    
    delete from ir_model where id = '616';
```

```sql
--BORRAR MUCHOS MODELO

select * from ir_model_fields where model_id in (select id from ir_model where model  like 'abastecimiento_%')

DELETE from ir_model_fields where model_id in (select id from ir_model where model  like 'abastecimiento_%')

delete from ir_model where model  like 'abastecimiento_%';
```
