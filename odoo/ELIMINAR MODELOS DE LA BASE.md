## ELIMINAR MODELOS Y CAMPOS DE LOS MODELOS EN LA BASE

    select * from ir_model where model  like '%transporte.tipo%';
    
    select * from ir_model_fields where model_id = '616';
    
    delete from ir_model_fields where model_id = '616';
    
    delete from ir_model where id = '616';
