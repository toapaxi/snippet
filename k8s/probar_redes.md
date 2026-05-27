especificar el namespace keycloak
y el pod pod/keycloak-584967cd65-rppkn


kubectl -n keycloak debug -it pod/keycloak-584967cd65-rppkn \
                               --image=nicolaka/netshoot \
                               --target=keycloak -- bash
