# CONTEXT ENVIO DE BOTON A WIZARD
## XML LE ENVIO POR CONTEXT
'default_corp_hr_tipo_roles_id': corp_hr_tipo_roles_id
'defalut_FIELD_RECIBE': FIELD OBJETO DEL BOTON

```
            <xpath expr="//button[@name='%(hr_payroll_community.action_hr_payslip_by_employees)d']" position="attributes">
                <attribute name="context">{'default_corp_hr_tipo_roles_id': corp_hr_tipo_roles_id, 'default_date_start': date_start, 'default_date_end': date_end, 'default_struct_id': struct_id}</attribute>
            </xpath>
```

## EN EL PY DESTINO DEBEN EXISTIR ESOS FIELDS

```
class NmHrPayslipEmployees(models.TransientModel):
    _inherit = 'hr.payslip.employees'

    corp_hr_tipo_roles_id = fields.Many2one(string='Tipo de Nomina', comodel_name='corp.hr.tipo.roles', )
    date_start = fields.Date(string='Date From')
    date_end = fields.Date(string='Date To')
    struct_id = fields.Many2one('hr.payroll.structure', string='Salary Structure')
```
