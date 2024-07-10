# Ejecutar lo siguiente

hostname=cluster.armada.mil.ec
port=443
trust_cert_file_location='/etc/ssl/certs/cluster.crt'
#trust_cert_file_location='/etc/ssl/certs/ca-certificates.crt'
#trust_cert_file_location='curl-config --ca'


sudo bash -c "echo -n | openssl s_client -showcerts -connect $hostname:$port -servername $hostname \
    2>/dev/null  | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p'  \
    >> $trust_cert_file_location"

update-ca-certificates
