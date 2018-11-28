# Icinga2 Deployment
```
NOTE: This should probably not be used in any capacity, it has been made as a proof of concept
```

Icinga2 deployment uses `docker-boshrelease`, `bosh-dns-aliases`, and `icinga2-boshrelease`

## Deploy cf-mysql
Deploy a MySQL cluster using cf-mysql-deployment
```
git clone https://github.com/cloudfoundry/cf-mysql-deployment
cd cf-mysql-deployment
bosh --deployment=cf-mysql deploy cf-mysql-deployment.yml \
  -o operations/bosh-lite.yml \
  -o operations/add-tls.yml \
  -v cf_mysql_host=bosh-lite.com
```

## Deploy Icinga2
Need to specify the icinga2 hostname when deploying so that the certificate and dashboard work, must be resolvable if you want the dashboard to work though
`operations/mysql-admin-password.yml` needs to be modified to point to the cf-mysql admin password from a config server (credhub)
```
bosh --deployment=icinga2 deploy icinga2.yml \
  -o operations/mysql-admin-password.yml \
  -v icinga_hostname=icinga2.local
```

