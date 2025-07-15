# Creacion de un usuario ADMIN para un reino
Buscar el usuario en el reino que desea
Ir a Role Mappings

Escoger en Roles de Cliente -> realm-management
de los roles disponibles escoger: 
manage-users
view-users
manage-realm
view-realm
manage-clients
view-clients
manage-events

 # **Ingreso de usuarios NORMALES**

<https://key-stg.armada.mil.ec/realms/armada/account/>


KEYCLOAK sin acceso a la consola de administración

**Descripcion:** no se podia ingresar a la consola de keycloak
Al verificar el html se encontro lo siguiente:
<script type="text/javascript">
        var authServerUrl = 'https://key-des.armada.mil.ec/xxx';
        var authUrl = 'https://key-des.armada.mil.ec';
        var consoleBaseUrl = '/admin/master/console/';
        var resourceUrl = '/resources/l20lt/admin/keycloak';
        var masterRealm = 'master';
        var resourceVersion = 'l20lt';
    </script>

La variable authServerUrl habia sido cambiada.

Se busco el parámetro en la base de datos keycloak
**SELECT name, realm_id, value
	FROM public.realm_attribute
	where name = 'frontendUrl'**


el value decia https://key-des.armada.mil.ec/xxx

y se actualizo a el value decia https://key-des.armada.mil.ec

**	UPDATE public.realm_attribute SET VALUE= 'https://key-des.armada.mil.ec'
	where name = 'frontendUrl'**
