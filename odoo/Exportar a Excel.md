# CREAR UN REPORTE EN EXCEL


Para el ejemplo vamos a crear un reporte excel report_hr_payslip_run (en nm_catalogos, nomina en lotes).  
Crear una carpeta xls.  <br>

Crear el archivo **report_hr_payslip_run.py** donde se hara el reporte:  
 _name = "**report**.hr_payslip_run.excel"

> NOTA: El nombre debe iniciar con **report**


```
from odoo import models
import time

class ReportHrPayslipRun(models.Model):
    _name = "report.hr_payslip_run.excel"
    _inherit = 'report.report_xlsx.abstract'
    _description = 'Reporte de ROL'

    def generate_xlsx_report(self, workbook, data, obj):
        # report_obj = self.env['report.cg_estadodecuentas.cg_reporte_estandar']
        # results = report_obj._get_report_values(obj, data)
        active_id = self.env.context.get('active_id')
        if active_id:
            [run_data] = self.env['hr.payslip.run'].search(active_id)

        sheet = workbook.add_worksheet()


        format1 = workbook.add_format({'font_size': 14, 'bottom': True, 'right': True, 'left': True, 'top': True,
                                       'align': 'center', 'bold': True, 'bg_color': '#bfbfbf', 'valign': 'vcenter','font_color': 'blue'})
        format2 = workbook.add_format({'font_size': 12, 'align': 'left', 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'bold': True, 'bg_color': '#bfbfbf'})
        format3 = workbook.add_format({'font_size': 12, 'align': 'right', 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'bold': True, 'bg_color': '#bfbfbf'})
        format4 = workbook.add_format({'font_size': 10, 'align': 'left', 'bold': True, 'right': True, 'left': True,
                                       'bottom': True, 'top': True})
        format5 = workbook.add_format({'font_size': 10, 'align': 'right', 'bold': True, 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'font_color': 'blue','num_format': '0.00'})
        format6 = workbook.add_format({'font_size': 10, 'align': 'left', 'bold': False, 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'text_wrap':'true'})
        format7 = workbook.add_format({'font_size': 10, 'align': 'right', 'bold': False, 'right': True, 'left': True,
                                       'bottom': True, 'top': True,'num_format': '0.00'})
        format8 = workbook.add_format({'font_size': 10, 'align': 'left', 'bold': False, 'right': True, 'left': True,
                                       'bottom': True, 'top': True, 'num_format': 'yyyy-mm-dd'})
        format9 = workbook.add_format({'font_size': 12, 'align': 'left', 'right': True, 'left': True,
                               'bottom': True, 'top': True, 'bold': True, 'font_color': 'blue'})
        format10 =  workbook.add_format({'font_size': 14, 'bottom': True, 'right': True, 'left': True, 'top': True,
                                       'align': 'center', 'bold': True, 'valign': 'vcenter','font_color': 'blue'})

        sheet.set_row(0, 40)
        sheet.set_row(1, 40)
        sheet.set_column(0, 0,15)
        sheet.set_column(1, 4, 25)
        sheet.set_column(5, 7, 15)

        # sheet.merge_range('A1:H1', data['form']['company_id'][1], format1)
        sheet.merge_range('A1:H1', obj.anio, format1)
        sheet.merge_range('A2:H2', "Estado de Cuenta Estandar", format10)
        sheet.merge_range('A3:B3', "Fecha de Emisión", format4)
        sheet.write('C3', time.strftime('%Y-%m-%d %H:%M:%S'), format6)
        sheet.merge_range('A4:B4', "Cuentas Contables", format4)

        sheet.write('F4', 'Estado', format4)

        sheet.write('F3', "Usuario", format4)
        sheet.write('A7', "Fecha ", format2)
        sheet.write('B7', "# Comprobante", format2)
        sheet.write('C7', "Estado", format2)
        sheet.write('D7', "Localidad", format2)
        sheet.write('E7', "Glosa", format2)
        sheet.write('F7', "Débito", format3)
        sheet.write('G7', "Crédito", format3)
        sheet.write('H7', "Balance", format3)
        row = 7
        col = 0
        for payslip in obj.slip_ids:
            row += 1
            sheet.write(row, col, payslip.employee_id.name, format10)
            col = 1
            sheet.write(row, col, payslip.employee_id.iddocumento, format10)


```
