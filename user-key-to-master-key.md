# User-Key 

### Check Status

`occ encryption:status`

### Decrypt

```
occ maintenance:singleuser --on
occ encryption:decrypt-all
#enter **Recovery Key** for **each user**
# Recovery Key is a password set by the admin
occ maintenance:singleuser --off
```

### Deactivation

```
occ encryption:disable
# ignore the "already disabled" message
occ app:disable encryption
```

# Master Key


## Remove encryption remnants

### Clean the database

`select * from oc_appconfig where appid='encryption';`

```
+------------+----------------------+----------------------+
| appid      | configkey            | configvalue          |
+------------+----------------------+----------------------+
| encryption | enabled              | no                   |
| encryption | installed_version    | 1.3.1                |
| encryption | masterKeyId          | master_dbba3376      |
| encryption | publicShareKeyId     | pubShare_dbba3376    |
| encryption | recoveryAdminEnabled | 1                    |
| encryption | recoveryKeyId        | recoveryKey_dbba3376 |
| encryption | types                | filesystem           |
| encryption | userSpecificKey      | 1                    |
+------------+----------------------+----------------------+
```

delete from oc_appconfig where appid='encryption';

### Clean storage

`find /var/www/owncloud/data -type d -name "files_encryption" -exec rm -R {} +`
`ls /var/www/owncloud/data/$user/`

Check if folder with encryption keys was deleted
