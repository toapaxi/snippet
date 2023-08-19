```python
.. code-block:: xml

   <field name="product_id_domain" invisible="1"/>
   <field name="product_id" domain="product_id_domain"/>


.. code-block:: python

   product_id_domain = fields.Char(
       compute="_compute_product_id_domain",
       readonly=True,
       store=False,
   )

   @api.multi
   @api.depends('name')
   def _compute_product_id_domain(self):
       for rec in self:
           rec.product_id_domain = json.dumps(
               [('type', '=', 'product'), ('name', 'like', rec.name)]
           )
```
