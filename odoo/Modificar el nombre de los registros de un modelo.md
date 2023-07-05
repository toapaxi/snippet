class MyModel(models.Model):
    _name = 'my.model'

    name = fields.Char(string='Name', required=True)

    def name_get(self):
        result = []
        for record in self:
            name = record.name  # Customize the display name based on your requirements
            result.append((record.id, name))
        return result

Tambien puede ser:
@api.depends('name', 'code')
    def name_get(self):
        result = []
        for account in self:
            name = account.code + ' ' + account.name
            result.append((account.id, name))
        return result