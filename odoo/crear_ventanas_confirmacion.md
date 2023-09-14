# Crear Wizard de Confirmacion

Debemos crear un boton para llamar al action

```xml
     <button string="Finalizar Contrato" name="action_finalizar_contrato" type="object" class="oe_highlight" states="open"/>
```
## Crear el ACTION
De ahi vamos a crear el action **action_finalizar_contrato**

Aqui se realiza la accion de abrir un wizard **view_contrato_finalizacion_form**
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
 **'context': {'create': False},** para que no cree un registro nuevo
 
 **'target': 'new',** esto hace que se muestre como popup
 
## Crear el wizard

De ahi vamos a crear el wizard **view_contrato_finalizacion_form**

```xml
<record id="view_contrato_finalizacion_form" model="ir.ui.view">
           <field name="name">Finalización de Contrato</field>
            <field name="model">hr.contract</field>
            <field name="mode">primary</field>
            <field name="priority">12</field>
            <field name="arch" type="xml">
                <form duplicate="0">
                    <sheet>
                        <group>
                            <field name="motivo_finalizacion" required="1" force_save="1" />
                            <field name="date_end" required="1" force_save="1" />
                        </group>
                         <footer>
                            <button name="action_close_contrato" string="Finalizar Contrato" type="object" default_focus="1" class="oe_highlight" data-hotkey="q"/>
                            <button string="Cancelar" class="btn btn-secondary" special="cancel" data-hotkey="z"/>
                         </footer>
                    </sheet>
                </form>
            </field>
        </record>
```

**motivo_finalizacion y date_end** Son los campos que necesitamos agregar

**action_close_contrato** permite cerrar el wizard y guardar los campos

## Crear ACTION cierre wizard

De ahi vamos a crear el action  **action_close_contrato**

```python
    def action_close_contrato(self):
        return self.write({'state': 'close'})
```


