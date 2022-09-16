#ARREGLAR ODOO

SELECT id, name, description, res_model, res_field, res_id, company_id, type, url, public, access_token, db_datas, store_fname, file_size, checksum, mimetype, index_content, create_uid, create_date, write_uid, write_date, original_id
	FROM public.ir_attachment
	where store_fname like '%fdffc45cba0e31dd34423b54f06fd48e9824192c%'
	
	delete  from ir_attachment
	where id >1
	
	 select * from ir_model where model  like '%transporte.tipo%';
select * from ir_model_fields where model_id = '616';

delete from ir_model_fields where model_id = '616';

delete from ir_model where id = '616';
