
            
            with self.pool.cursor() as cr:  # Crear un nuevo cursor independiente
                cr.execute("SET TRANSACTION ISOLATION LEVEL READ COMMITTED;")  # Configurar el nivel de aislamiento
                cr.execute(sql)
                result = cr.dictfetchall()
