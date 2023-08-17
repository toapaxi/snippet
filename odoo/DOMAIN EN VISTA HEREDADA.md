# ELABORAR UN DOMAIN(NO PERMITE SELECCIONAR EL MISMO ITEM) EN UN DETALLE HEREDADO

## Ejemplo creamos en domain en la clase heredada

```python
class Invbpmline(models.Model):
    _inherit = ['mrp.bom.line']
    @api.depends('product_id')
```

## DOMAIN NO PERMITE SELECCIONAR EL MISMO PRODUCTO

```python
    def _compute_producto(self):
      for record in self:
        all_caracteristicas = self.env['product.product'].search([])
        listado_caracteristicas = record.bom_id.bom_line_ids.product_id
        restantes = all_caracteristicas - listado_caracteristicas
        record.domain_producto_id = json.dumps([('id', 'in', restantes.ids)])
```

## EN EL VIEW HEREDADO

```xml
<xpath expr="//field[@name='bom_line_ids']//tree//field[@name='product_id']" position="replace">
                      <field name="domain_producto_id" invisible="1" />
                     <field name="product_id" domain="domain_producto_id" force_save="1" attrs="{'readonly': [('inv_state_det', '!=', False)]}" 
                     options="{'no_create_edit': True, 'no_create': True, 'no_quick_create': True , 'no_open': True}"/>
                </xpath>
```
