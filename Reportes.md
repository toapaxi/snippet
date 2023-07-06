# Copiar la funcionalidad de imprimir a un boton nuevo

Debemos buscar en Ajustes->Tecnico-> Informes
Buscar: colocamos el nombre del modelo Ejemplo: hr.payslip

De aqui tomamos el nombre de la plantilla: hr_payroll_community.report_payslip

Este nombre lo buscamos en el codigo xml y obtendremos algo asi:
``` 
<record id="action_report_payslip" model="ir.actions.report">
            <field name="name">Payslip</field>
            <field name="model">hr.payslip</field>
            <field name="report_type">qweb-pdf</field>
            <field name="report_name">hr_payroll_community.report_payslip</field>
            <field name="report_file">hr_payroll_community.report_payslip</field>
            <field name="binding_model_id" ref="model_hr_payslip"/>
            <field name="print_report_name">('Payslip - %s' % (object.employee_id.name))</field>
</record>
```

Copiamos el record id="**action_report_payslip**"

## CREACION DEL BOTON CON UN ACTION
donde necesitemos el boton lo crearemos de la sgte manera:
``` 
<button name="%(**action_report_payslip**)d" string="Generar Reporte" type="action" class="btn-primary"/>
```

## CREACION DE UN BOTON COMO OBJECT
> Esto sirve mas para agregar validaciones

Se debe crear una funcion en el modelo respectivo
```
    def do_print_nomina(self):
      for record in self:
            check_layout = 'hr_payroll_community.action_report_payslip'

            report_action = record.env.ref(check_layout, False)

            return report_action.report_action(record)
```

y donde necesitemos el boton lo crearemos de la sgte manera:
``` 
 <button string="IMPRIMIR NOMINA" name="do_print_nomina" type="object" class="oe_highlight"/>
```
