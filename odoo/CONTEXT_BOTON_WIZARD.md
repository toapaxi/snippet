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


## CONTEXT ENVIO DESDE PY
    def pagos_view(self):
        pagos_ids = self._get_pagos_conciliados_ids()
        domain = [('id', 'in', pagos_ids) ]
        return {
            'name'     : _('Pagos aplicados'),
            'domain'   : domain,
            'res_model': 'account.payment',
            'type'     : 'ir.actions.act_window',
            'views': [(self.env.ref('cxp_provisiones.view_account_payment_pagos_tree').id, 'tree'),
                      (self.env.ref('cxp_provisiones.view_account_payment_proveedor_form').id, 'form')],
            # 'view_id'  : False,
            'view_mode': 'tree,form',
            'limit'    : 80,
            'context'  : "{'default_FIELD_VIEW': '%s', 'default_FIELD2': '%s'}" % pagos_ids % domain,
            'context2':  "{'default_corp_hr_tipo_roles_id': corp_hr_tipo_roles_id, 'default_date_start': date_start}"
        }
