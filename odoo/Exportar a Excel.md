# CREAR UN REPORTE EN EXCEL

### SE NECESITA EL MODULO lib_excel 
agregar en manifest en la seccion depends

### Para el ejemplo vamos a crear un reporte excel report_hr_payslip_run (en nm_catalogos, nomina en lotes).  
### Crear una carpeta xls.  <br>
> NOTA: no olvide el archivo __init__.py  
> y agregar la carpeta xls en el __init__.py general del modulo

### Crear el archivo **report_hr_payslip_run.py** donde se hara el reporte:  
 _name = "**report**.hr_payslip_run.excel"

> NOTA: El nombre debe iniciar con **report**  
> NOTA2: obj tiene los datos del modelo que se envie en el action


```python
from odoo import models
import time


class ReportHrPayslipRun(models.Model):
    _name = "report.hr_payslip_run.excel"
    _inherit = 'report.report_xlsx.abstract'
    _description = 'Reporte de ROL'

    def generate_xlsx_report(self, workbook, data, obj):
        # report_obj = self.env['report.cg_estadodecuentas.cg_reporte_estandar']
        # results = report_obj._get_report_values(obj, data)

        company_id = self.env.user.company_id.id
        if company_id:
            [run_data] = self.env['hr.payslip.run'].browse(company_id)

        sheet = workbook.add_worksheet()

        f_titulo_reporte_fondo = workbook.add_format(
            {'font_size': 14, 'bottom': True, 'right': True, 'left': True, 'top': True,
             'align': 'center', 'bold': True, 'bg_color': '#bfbfbf', 'valign': 'vcenter', 'font_color': 'blue'})
        f_cabecera_celda = workbook.add_format({'font_size': 12, 'align': 'left', 'right': True, 'left': True,
                                                'bottom': True, 'top': True, 'bold': True, 'bg_color': '#bfbfbf'})
        format3 = workbook.add_format({'font_size': 12, 'align': 'right', 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'bold': True, 'bg_color': '#bfbfbf'})
        f_celda_titulo = workbook.add_format(
            {'font_size': 10, 'align': 'left', 'bold': True, 'right': True, 'left': True,
             'bottom': True, 'top': True})
        format5 = workbook.add_format({'font_size': 10, 'align': 'right', 'bold': True, 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'font_color': 'blue', 'num_format': '0.00'})
        f_celda_texto = workbook.add_format(
            {'font_size': 10, 'align': 'left', 'bold': False, 'right': True, 'left': True,
             'bottom': True, 'top': True, 'text_wrap': 'true'})
        format7 = workbook.add_format({'font_size': 10, 'align': 'right', 'bold': False, 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'num_format': '0.00'})
        f_celda_fecha = workbook.add_format(
            {'font_size': 10, 'align': 'left', 'bold': False, 'right': True, 'left': True,
             'bottom': True, 'top': True, 'num_format': 'yyyy-mm-dd'})
        format9 = workbook.add_format({'font_size': 12, 'align': 'left', 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'bold': True, 'font_color': 'blue'})
        f_titulo_reporte = workbook.add_format(
            {'font_size': 14, 'bottom': True, 'right': True, 'left': True, 'top': True,
             'align': 'center', 'bold': True, 'valign': 'vcenter', 'font_color': 'blue'})

        sheet.set_row(0, 30)
        sheet.set_row(1, 30)
        sheet.set_column(0, 0, 15)
        sheet.set_column(1, 18, 20)


        colNomina = 0
        colSeccion = 1
        colDpto = 2

        colCedula = 3
        colApPaterno = 4
        colApMaterno = 5
        colNombres = 6

        colImprimir = 7
        if obj.ultima_quincena == 1:
            colAnticipo = colImprimir
        else:
            colSueldo = colImprimir
        colImprimir += 1
        colTotalIngreso = colImprimir
        colImprimir += 1
        # Columnas de Egreso
        colEAnticipo = colImprimir
        colImprimir += 1
        colEiess= colImprimir
        colImprimir += 1
        colTotalEgreso = colImprimir
        colImprimir += 1
        colARecibir = colImprimir
        colImprimir += 1
        colCiudad = colImprimir
        colImprimir += 1
        colEdad = colImprimir
        colImprimir += 1
        colFingreso = colImprimir
        colImprimir += 1
        colFsalida = colImprimir
        colImprimir += 1
        colEcivil = colImprimir
        colImprimir += 1
        colPTrabajo = colImprimir
        filaTitulo = 6
        # sheet.merge_range('A1:H1', data['form']['company_id'][1], f_titulo_reporte_fondo)
        sheet.merge_range('A1:Q1', self.env.user.company_id.name, f_titulo_reporte_fondo)
        sheet.merge_range('A2:Q2', obj.name, f_titulo_reporte)
        sheet.write('A3', "Periodo", f_celda_titulo)
        sheet.write('B3', obj.date_start, f_celda_fecha)
        sheet.write('C3', "al", f_celda_fecha)
        sheet.write('D3', obj.date_end, f_celda_fecha)
        sheet.write('F4', 'Estado', f_celda_titulo)
        sheet.write('G4', obj.state, f_celda_texto)
        sheet.write('F3', "Usuario", f_celda_titulo)
        sheet.write('G3', self.env.user.name, f_celda_texto)
        sheet.write('B7', "Sección ", f_cabecera_celda)
        sheet.write('C7', "Dpto", f_cabecera_celda)
        sheet.write('A7', "T. Nomina", f_cabecera_celda)
        sheet.write('D7', "Cedula", f_cabecera_celda)
        sheet.write('E7', "Apellido Paterno", f_cabecera_celda)
        sheet.write('F7', "Apellido Materno", f_cabecera_celda)
        sheet.write('G7', "Nombres", f_cabecera_celda)

        if obj.ultima_quincena == 1:
            sheet.write(filaTitulo, colAnticipo, "Quincena", f_cabecera_celda)
        else:
            sheet.write(filaTitulo, colSueldo, "Sueldo", f_cabecera_celda)
        sheet.write(filaTitulo, colTotalIngreso, "T. Ingreso", f_cabecera_celda)
        sheet.write(filaTitulo, colEAnticipo, "Anticipos", f_cabecera_celda)
        sheet.write(filaTitulo, colEiess, "IESS", f_cabecera_celda)
        sheet.write(filaTitulo,colTotalEgreso, "T. Egresos", f_cabecera_celda)
        sheet.write(filaTitulo,colARecibir, "A Recibir", f_cabecera_celda)
        sheet.write(filaTitulo,colCiudad, "Ciudad", f_cabecera_celda)
        sheet.write(filaTitulo, colEdad, "Edad", f_cabecera_celda)
        sheet.write(filaTitulo,colFingreso, "F. Ingreso", f_cabecera_celda)
        sheet.write(filaTitulo, colFsalida, "F. Salida", f_cabecera_celda)
        sheet.write(filaTitulo,colEcivil, "E. Civil", f_cabecera_celda)
        sheet.write(filaTitulo,colPTrabajo, "Puesto de Trabajo", f_cabecera_celda)

        row = 6
        col = 0
        regla_salarial = [(record.code, record.category_id.name) for record in obj.slip_ids.line_ids]
        unique_regla_salarial = list(set(regla_salarial))
        sorted_objs = obj.search([])
        sorted_slip_ids = sorted(obj.slip_ids, key=lambda slip: slip.employee_id.apellido_paterno)

        for payslip in sorted_slip_ids:
            row += 1
            sheet.write(row, col, payslip.employee_id.name, f_titulo_reporte)
            col = 1
            sheet.write(row, col, payslip.employee_id.iddocumento, f_titulo_reporte)
            if payslip.employee_id.corp_hr_seccion_id and payslip.employee_id.corp_hr_seccion_id.display_name:
                sheet.write(row, colSeccion, payslip.employee_id.corp_hr_seccion_id.display_name, f_celda_texto)
            if payslip.employee_id.department_id and payslip.employee_id.department_id.name:
                sheet.write(row, colDpto, payslip.employee_id.department_id.name, f_celda_texto)
            if payslip.employee_id.corp_hr_tipo_roles_id and payslip.employee_id.corp_hr_tipo_roles_id.display_name:
                sheet.write(row, colNomina, payslip.employee_id.corp_hr_tipo_roles_id.display_name, f_celda_texto)
            if payslip.employee_id.iddocumento:
                sheet.write(row, colCedula, payslip.employee_id.iddocumento, f_celda_texto)
            if payslip.employee_id.apellido_paterno:
                sheet.write(row, colApPaterno, payslip.employee_id.apellido_paterno, f_celda_texto)
            if payslip.employee_id.apellido_materno:
                sheet.write(row, colApMaterno, payslip.employee_id.apellido_materno, f_celda_texto)
            if payslip.employee_id.firstname:
                sheet.write(row, colNombres, payslip.employee_id.firstname, f_celda_texto)
            if payslip.employee_id.city:
                sheet.write(row, colCiudad, payslip.employee_id.city, f_celda_texto)
            if payslip.employee_id.edad:
                sheet.write(row, colEdad, payslip.employee_id.edad, f_celda_texto)
            if payslip.employee_id.fecha_ingreso:
                sheet.write(row, colFingreso, payslip.employee_id.fecha_ingreso, f_celda_fecha)
            if payslip.employee_id.fecha_salida:
                sheet.write(row, colFsalida, payslip.employee_id.fecha_salida, f_celda_fecha)
            if payslip.employee_id.marital:
                sheet.write(row, colEcivil, payslip.employee_id.marital, f_celda_texto)
            if payslip.employee_id.job_id and payslip.employee_id.job_id.name:
                sheet.write(row, colPTrabajo, payslip.employee_id.job_id.name, f_celda_texto)
            if obj.ultima_quincena == 1:
                sheet.write(row, colAnticipo, 0, f_celda_texto)
            else:
                sheet.write(row, colSueldo, 0, f_celda_texto)


            sheet.write(row, colEAnticipo, 0, f_celda_texto)
            regla_salarial = [record.code for record in payslip.line_ids]

            for regla_salarial in payslip.line_ids:
                if "QUINCENA" in regla_salarial.code:
                    sheet.write(row, colAnticipo, regla_salarial.total, f_celda_texto)
                if "SUELDO" in regla_salarial.code:
                    sheet.write(row, colSueldo, regla_salarial.total, f_celda_texto)
                if "ANTICIPO" in regla_salarial.code:
                    sheet.write(row, colEAnticipo, regla_salarial.total, f_celda_texto)
                if "IESS" in regla_salarial.code:
                    sheet.write(row, colEiess, regla_salarial.total, f_celda_texto)
            # Formula Total Ingreso
            formula = f'=SUM(H{row + 1}:H{row + 1})'
            sheet.write_formula(row, colTotalIngreso, formula, f_celda_texto)
            # Formula Total Egreso
            formula = f'=SUM(J{row + 1}:K{row + 1})'
            sheet.write_formula(row, colTotalEgreso, formula, f_celda_texto)
            # Formula Neto a Recibir
            formula = f'=I{row + 1}+L{row + 1}'
            sheet.write_formula(row, colARecibir, formula, f_celda_texto)
        row += 1
        sheet.write(row, colNombres, "TOTALES", f_celda_titulo)
        # Formula Total Empleados
        formula = f'=SUM(H8:H{row})'
        if obj.ultima_quincena == 1:

            sheet.write_formula(row, colAnticipo, formula, f_celda_texto)
        else:
            sheet.write_formula(row, colSueldo, formula, f_celda_texto)

        formula = f'=SUM(I8:I{row})'
        sheet.write_formula(row, colTotalIngreso, formula, f_celda_texto)
        formula = f'=SUM(J8:J{row})'
        sheet.write_formula(row, colEAnticipo, formula, f_celda_texto)
        formula = f'=SUM(K8:K{row})'
        sheet.write_formula(row, colEiess, formula, f_celda_texto)
        formula = f'=SUM(L8:L{row})'
        sheet.write_formula(row, colTotalEgreso, formula, f_celda_texto)
        formula = f'=SUM(M8:M{row})'
        sheet.write_formula(row, colARecibir, formula, f_celda_texto)


```

### Crear el archivo **report_hr_payslip_run.xml** donde estara el action:  

> Nota:  El nombre es el modelo que necesita
<br/>

```xml
<field name="model">hr.payslip.run</field>
```

> Nota: Colocar el nombre sin el prefijo **report**  ``` <field name="report_name">hr_payslip_run.excel</field>.  ```  
Debido a que en el Controller le agrega el prefijo **reporte.**  
Si quiere ver, busque => xlsx = report.with_context(**context)._render_xlsx(docids, data=data)[0]

```xml
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data>
        <record id="action_report_hr_payslip_run_excel" model="ir.actions.report">
             <field name="name">Reporte de Nominas</field>
             <field name="model">hr.payslip.run</field>
            <field name="report_type">xlsx</field>
            <field name="report_name">hr_payslip_run.excel</field>
            <field name="report_file">hr_payslip_run.excel</field>
             <field name="attachment_use">False</field>
        </record>

    </data>
</odoo>
```


