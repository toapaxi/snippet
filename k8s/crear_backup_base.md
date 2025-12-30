kubectl -n postgres exec postgresql-fbdbfd4ff-mb8vl -- pg_dump -U odoo -F c odoo-ares > odoo-ares.dump
