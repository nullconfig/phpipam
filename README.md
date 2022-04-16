# phpipam

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.5](https://img.shields.io/badge/AppVersion-1.5-informational?style=flat-square)


**Homepage:** <https://phpipam.net>

## Maintainers

| Name | Email | 
| ---- | ------ |
| bgalloway | <nullconfig@gmail.com> |

## Source Code

* <https://github.com/nullconfig/phpipam>

## Requirements

Kubernetes: `^1.19.0-0`

Create the mariadb secret
```
kubectl create secret generic mysql-password --from-literal='password=<password>' -n phpipam
```

Installing phpipam 
```console
helm repo add phpipam https://nullconfig.github.io/phpipam/stable
helm repo update
helm install --namespace phpipam --create-namespace phpipam phpipam/phpipam
```


Creating a backup of the database
```
mysqldump phpipam -u phpipam -p > phpipam_migration_database.sql
```
Restore database backup
```
mysql -u phpipam -p phpipam < phpipam_migration_database.sql
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| namespace | string | `"phpipam"` |  |
| nodeSelector | object | `{}` |  |
| phpipamCron.env[0].name | string | `"IPAM_DATABASE_HOST"` |  |
| phpipamCron.env[0].value | string | `"phpipam-db"` |  |
| phpipamCron.env[1].name | string | `"IPAM_DATABASE_PASS"` |  |
| phpipamCron.env[1].valueFrom.secretKeyRef.key | string | `"password"` |  |
| phpipamCron.env[1].valueFrom.secretKeyRef.name | string | `"mysql-password"` |  |
| phpipamCron.env[2].name | string | `"SCAN_INTERVAL"` |  |
| phpipamCron.env[2].value | string | `"1h"` |  |
| phpipamCron.env[3].name | string | `"TZ"` |  |
| phpipamCron.env[3].value | string | `"America/Los_Angeles"` |  |
| phpipamCron.image.pullPolicy | string | `"IfNotPresent"` |  |
| phpipamCron.image.repository | string | `"phpipam/phpipam-cron"` |  |
| phpipamCron.image.tag | string | `"1.5x"` |  |
| phpipamCron.name | string | `"phpipam-cron"` |  |
| phpipamCron.resources | object | `{}` |  |
| phpipamMariadb.env[0].name | string | `"MARIADB_ROOT_PASSWORD"` |  |
| phpipamMariadb.env[0].valueFrom.secretKeyRef.key | string | `"password"` |  |
| phpipamMariadb.env[0].valueFrom.secretKeyRef.name | string | `"mysql-password"` |  |
| phpipamMariadb.image.pullPolicy | string | `"IfNotPresent"` |  |
| phpipamMariadb.image.repository | string | `"mariadb"` |  |
| phpipamMariadb.image.tag | string | `"10.7.3"` |  |
| phpipamMariadb.name | string | `"phpipam-db"` |  |
| phpipamMariadb.persistentVolume.enabled | bool | `false` |  |
| phpipamMariadb.resources | object | `{}` |  |
| phpipamMariadb.service.port | int | `3306` |  |
| phpipamMariadb.service.type | string | `"ClusterIP"` |  |
| phpipamMariadb.volumeMounts | object | `{}` |  |
| phpipamWeb.env[0].name | string | `"TZ"` |  |
| phpipamWeb.env[0].value | string | `"America/Los_Angeles"` |  |
| phpipamWeb.env[1].name | string | `"IPAM_DATABASE_HOST"` |  |
| phpipamWeb.env[1].value | string | `"phpipam-db"` |  |
| phpipamWeb.env[2].name | string | `"IPAM_DATABASE_WEBHOST"` |  |
| phpipamWeb.env[2].value | string | `"%"` |  |
| phpipamWeb.env[3].name | string | `"IPAM_DATABASE_PASS"` |  |
| phpipamWeb.env[3].valueFrom.secretKeyRef.key | string | `"password"` |  |
| phpipamWeb.env[3].valueFrom.secretKeyRef.name | string | `"mysql-password"` |  |
| phpipamWeb.image.pullPolicy | string | `"IfNotPresent"` |  |
| phpipamWeb.image.repository | string | `"phpipam/phpipam-www"` |  |
| phpipamWeb.image.tag | string | `"1.5x"` |  |
| phpipamWeb.ingress.annotations | object | `{}` |  |
| phpipamWeb.ingress.enabled | bool | `false` |  |
| phpipamWeb.ingress.extraLabels | object | `{}` |  |
| phpipamWeb.ingress.host | string | `"phpipam.example.local"` |  |
| phpipamWeb.ingress.path | string | `"/"` |  |
| phpipamWeb.ingress.pathType | string | `"Prefix"` |  |
| phpipamWeb.ingress.pathType | string | `"Prefix"` |  |
| phpipamWeb.ingress.tls | list | `[]` |  |
| phpipamWeb.name | string | `"phpipam-web"` |  |
| phpipamWeb.resources | object | `{}` |  |
| phpipamWeb.service.port | int | `80` |  |
| phpipamWeb.service.type | string | `"ClusterIP"` |  |
| replicaCount | int | `1` |  |
| tolerations | object | `{}` |  |

----------------------------------------------

