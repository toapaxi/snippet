# Heredar roll de grupo a otro grupo 

 Ejemplo
    Al grupo bco_grupo_tesorero se le asignara  **eval="[(4, ref('account.group_account_invoice'))]"**

Ejemplo completo 
```xml
<record id="bco_grupo_tesorero" model="res.groups">
            <field name="name">Tesorero</field>
            <field name="category_id" ref="bco_security"/>
            <field name="implied_ids" eval="[(4, ref('account.group_account_invoice'))]"/>
</record>
```
