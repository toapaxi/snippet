# METODO ON_LOAD PARA LOS MODELOS
## Al tener mi clase th_empleados
class th_empleados(models.Model):
    _inherit = 'hr.employee'

## Crear la funcion def read(self, fields=None, load='_classic_read'):
### Se debe comprobar la existencia del campo
#### if 'corp_hr_empleado_id' in record:

    def read(self, fields=None, load='_classic_read'):
        # Llama al método padre para realizar la operación de lectura predeterminada
        records = super(th_empleados, self).read(fields=fields, load=load)

        # Agrega la lógica para cargar automáticamente los datos que deseas
        for record in records:
            # empleado_corpo = self.env["corp.hr.empleado"].search([('id', '=', record.corp_hr_empleado_id.id)])
            if 'corp_hr_empleado_id' in record:
                empleado_corpo = self.env["corp.hr.empleado"].search([('id', '=', record['corp_hr_empleado_id'][0])])
                for record_empleado_corpo in empleado_corpo:
                    # Aquí puedes agregar la lógica para cargar automáticamente los datos
                    record['gender'] = record_empleado_corpo.gender#'Datos cargados automáticamente'
        return records
