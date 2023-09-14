# Crear Wizard de Confirmacion

Debemos crear un boton para llamar al action

```xml
     <button string="Finalizar Contrato" name="action_finalizar_contrato" type="object" class="oe_highlight" states="open"/>
```

De ahi vamos a crear el action **action_finalizar_contrato**

Este nombre lo buscamos en el codigo xml y obtendremos algo asi:
```python
 def action_finalizar_contrato(self):
        for record in self:
            return {
                'name': _('Finalización de Contrato'),
                'type': 'ir.actions.act_window',
                'res_model': 'hr.contract',
                'view_mode': 'form',
                'context': {'create': False},
                'views': [(self.env.ref('th_contratos.view_contrato_finalizacion_form').id, 'form')],
                'res_id': self.id,
                'target': 'new',
            }
```

Copiamos el record id="**action_report_payslip**"

