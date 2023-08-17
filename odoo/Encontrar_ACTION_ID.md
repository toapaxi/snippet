# Buscar el nombre de un ACTION ID

Para ejemplo buscaremos el id:    638

```sql
    SELECT name, module, * FROM ir_model_data 
    WHERE model='ir.actions.act_window' 
    AND res_id=638;
```

Con esto tomo el name y lo busco en el codigo fuente de ODOO

**Para el ejemplo:		action_hr_payslip_by_employees**

Y encontraremos en este formato **name="%(action_hr_payslip_by_employees)d"**

Esto indica la accion que buscamos

```xml
    <button name="%(action_hr_payslip_by_employees)d" type="action" states="draft" string="Generate Payslips" class="oe_highlight"/>
```
