# DESCARGAR UN ARCHIVO XML
## CON EL XML CREADO

# FALTA VERIFICAR SI EXISTE EL ARCHIVO Y SOBREESCRIBIR
```python
def action_descargar_archivo(self):
            tree = ET.ElementTree()
            bytesxml = tree.getroot()
            xml_str = ET.tostring(tree.getroot(), encoding='UTF-8', method='xml')
            archivo = base64.b64encode(xml_str)

            base_url = self.env['ir.config_parameter'].get_param('web.base.url')
            attachment_obj = self.env['ir.attachment']
            # create attachment
            attachment_id = attachment_obj.create(
                {'name':nombrearchivo, 'datas': archivo})
            # prepare download url
            download_url = '/web/content/' + str(attachment_id.id) + '?download=true'
            # download
            return {
                "type": "ir.actions.act_url",
                "url": str(base_url) + str(download_url),
                "target": "new",
            }

```
