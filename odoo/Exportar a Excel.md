# CREAR UN REPORTE EN EXCEL


Para el ejemplo vamos a crear un reporte excel report_hr_payslip_run (en nm_catalogos, nomina en lotes)
Crear una carpeta xls
dentro el archivo report_hr_payslip_run.py donde se hara el reporte

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
        # if data['form']['display_account'] == 'all':
        #     sheet.write('C4', 'Todas las cuentas', format6)
        # if data['form']['display_account'] == 'movement':
        #     sheet.write('C4', 'Con movimiento', format6)
        # if data['form']['display_account'] == 'not_zero':
        #     sheet.write('C4', 'Con saldo no igual a cero', format6)
        # if data['form']['display_account'] == 'por_rango':
            # sheet.write('C4', results['print_cuenta_inicial'] + "-" + results['print_cuenta_final'], format6)

        sheet.write('F4', 'Estado', format4)
        # if data['form']['target_move']== 'all':
        #     sheet.merge_range('G4:H4', 'Todos', format6)
        # elif data['form']['target_move'] == 'posted':
        #     sheet.merge_range('G4:H4', 'Publicados', format6)

        sheet.write('F3', "Usuario", format4)
        # sheet.merge_range('G3:H3', results['docs']['write_uid']['display_name'], format6)
        # if data['form']['date_from']:
        #     sheet.merge_range('A5:B5', "Desde:", format4)
        #     sheet.write('C5', data['form']['date_from'], format6)
        # if data['form']['date_to']:
        #     sheet.write('F5', "Hasta:", format4)
        #     sheet.merge_range('G5:H5', data['form']['date_to'], format6)
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


        # for account in results['Accounts']:
        #     sheet.merge_range(row, col, row, col + 4, account['code'] + " " + account['name'], format4)
        #     for localidad in account['localidad_res']:
        #         for line in localidad['localidad_lines']:
        #             col = 0
        #             row += 1
        #             sheet.write(row, col, line['ldate'], format8)
        #             if line['lname'] == 'Saldo Inicial:':
        #                 sheet.write(row, col + 1, "", format6)
        #             else:
        #               sheet.write(row, col + 1, line['lcode'] + "-" + line['move_name'], format6)
        #
        #             if line['lname'] == 'Saldo Inicial:':
        #                 sheet.write(row, col + 2, "", format6)
        #             elif  line['estado']=='draft':
        #                   sheet.write(row, col + 2, "Borr", format6)
        #             else:
        #                   sheet.write(row, col + 2, "Publ", format6)
        #             if line['lname'] == 'Saldo Inicial:':
        #                 sheet.write(row, col + 3, "", format6)
        #             else:
        #               sheet.write(row, col + 3, line['localidad_codigo'] or '', format6)
        #             sheet.write(row, col + 4, line['lname'], format6)
        #             if line['lname'] == 'Saldo Inicial:':
        #                 sheet.write(row, col + 5, "", format7)
        #             else:
        #               sheet.write(row, col + 5, line['debit'], format7)
        #             if line['lname'] == 'Saldo Inicial:':
        #                 sheet.write(row, col + 6, "", format7)
        #             else:
        #                 sheet.write(row, col + 6, line['credit'], format7)
        #             if line['lname'] == 'Saldo Inicial:':
        #                 sheet.write(row, col + 7, line['balance'], format7)
        #             else:
        #               sheet.write(row, col + 7, line['balance'], format7)
        #         row += 1
        #     sheet.merge_range(row, col, row, col + 4,"TOTAL DE " + account['code'] + " " + account['name'], format9)
        sheet.write(row, col + 5, "account['debit']", format5)
        # sheet.write(row, col + 6, account['credit'], format5)
        # sheet.write(row, col + 7, account['balance'], format5)
        row += 1
```
