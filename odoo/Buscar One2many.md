# Activar busqueda de una compra por nombre de proveedor

```python
@api.model
    def name_search(self, name='', args=None, operator='ilike', limit=100):
        args = args or []
        domain = args + ['|', ('name', operator, name), ('purchase_order_id.partner_id.name', operator, name)]
        return self.search(domain, limit=limit).name_get()
```
