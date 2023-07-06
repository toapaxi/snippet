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
Copiamos el: record id="**action_report_payslip**"

donde necesitemos el boton lo crearemos de la sgte manera:
``` 
<button name="%(**action_report_payslip**)d" string="Generar Reporte" type="action" class="btn-primary"/>
```
