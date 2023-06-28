# README

## CLI Commands

```bash
#
# ssh ec2-user@ip-10-15-2-237
#
sudo ansible-playbook playbook_with_vars.yml -e druid_host_vpc=15 -e druid_host_subnet=12 -e druid_host_instance=118
#
sudo cp wild.dev.tortuga.systems.cert.pem druid_cert.pem
sudo cp wild.dev.tortuga.systems.key.pem druid_key.pem
sudo cp wild.dev.tortuga.systems.csr.pem druid_csr.pem
sudo chown -R ec2-user:ec2-user druid*
sudo openssl pkcs12 -inkey druid_key.pem -in druid_cert.pem -export -out druidkey.p12 -name druid
# druid1password
sudo keytool -importkeystore -destkeystore druid-keystore.jks -srckeystore druidkey.p12 -srcstoretype PKCS12
# druid1password
sudo keytool -import -alias druid -file druid_cert.pem -keystore druid-truststore.jks
# druid1password
sudo cp druid-* /mnt/efs/apache/apache-jks/
#
# ssh ubuntu@10.15.12.118 
#
sudo su - druid
#
cd /mnt/efs/apache/apache-jks
mkdir -p ip-10-15-12-118
sudo mv druid*.jks ip-10-15-12-118
sudo chown -R druid:druid ip-10-15-12-118/
#
# Go to druid query server ip-10-15-12-118 and restart the query server
#
```
