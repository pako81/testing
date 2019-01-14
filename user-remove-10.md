user remove test

Vor der Löschung des Users

```
MariaDB [owncloud]> select * from oc_share;
+----+------------+------------+-----------+---------------+--------+-----------+-------------+-------------+-------------+-------------------+-------------+------------+----------+------------+-------+-----------+------------+
| id | share_type | share_with | uid_owner | uid_initiator | parent | item_type | item_source | item_target | file_source | file_target       | permissions | stime      | accepted | expiration | token | mail_send | share_name |
+----+------------+------------+-----------+---------------+--------+-----------+-------------+-------------+-------------+-------------------+-------------+------------+----------+------------+-------+-----------+------------+
|  1 |          0 | oc1        | admin     | admin         |   NULL | file      | 23          | NULL        |          23 | /cawabanga.webp   |          19 | 1547473972 |        0 | NULL       | NULL  |         0 | NULL       |
|  2 |          0 | oc_2       | oc1       | oc1           |   NULL | file      | 34          | NULL        |          34 | /hidden-files.png |          19 | 1547474089 |        0 | NULL       | NULL  |         0 | NULL       |
+----+------------+------------+-----------+---------------+--------+-----------+-------------+-------------+-------------+-------------------+-------------+------------+----------+------------+-------+-----------+------------+
2 rows in set (0.00 sec)
```

Nach der Löschung des users:

```
MariaDB [owncloud]> select * from oc_share;
Empty set (0.00 sec)
```

----------------------------------------------------------------------------------------

Vor der Löschung des Users

```
MariaDB [owncloud]> select * from oc_preferences;
+--------+----------------+------------------------+---------------+
| userid | appid          | configkey              | configvalue   |
+--------+----------------+------------------------+---------------+
| admin  | core           | lang                   | de            |
| admin  | core           | timezone               | Europe/Berlin |
| admin  | firstrunwizard | show                   | 0             |
| oc1    | core           | lang                   | de            |
| oc1    | core           | timezone               | Europe/Berlin |
| oc1    | core           | username               | oc1           |
| oc1    | firstrunwizard | show                   | 0             |
| oc1    | user_ldap      | firstLoginAccomplished | 1             |
| oc_2   | core           | username               | oc_2          |
+--------+----------------+------------------------+---------------+
9 rows in set (0.00 sec)
```

Nach der Löschung des users:

```
MariaDB [owncloud]> select * from oc_preferences;
+--------+----------------+-----------+---------------+
| userid | appid          | configkey | configvalue   |
+--------+----------------+-----------+---------------+
| admin  | core           | lang      | de            |
| admin  | core           | timezone  | Europe/Berlin |
| admin  | firstrunwizard | show      | 0             |
| oc_2   | core           | username  | oc_2          |
+--------+----------------+-----------+---------------+
4 rows in set (0.00 sec)
```

---------------------------------------------------------------------------------------------------

Vor der Löschung des Users

```
MariaDB [owncloud]> select * from oc_storages;
+--------------------------------+------------+-----------+--------------+
| id                             | numeric_id | available | last_checked |
+--------------------------------+------------+-----------+--------------+
| home::admin                    |          1 |         1 |         NULL |
| local::/var/www/owncloud/data/ |          2 |         1 |         NULL |
| home::oc1                      |          3 |         1 |         NULL |
| home::oc_2                     |          4 |         1 |         NULL |
+--------------------------------+------------+-----------+--------------+
4 rows in set (0.00 sec)
```

Nach der Löschung des users:

```
MariaDB [owncloud]> select * from oc_storages;
+--------------------------------+------------+-----------+--------------+
| id                             | numeric_id | available | last_checked |
+--------------------------------+------------+-----------+--------------+
| home::admin                    |          1 |         1 |         NULL |
| local::/var/www/owncloud/data/ |          2 |         1 |         NULL |
| home::oc_2                     |          4 |         1 |         NULL |
+--------------------------------+------------+-----------+--------------+
3 rows in set (0.00 sec)
```

-------------------------------------------------------------------------------------------------------------

Vor der Löschung des Users

```
MariaDB [owncloud]> select * from oc_ldap_user_mapping;
+---------------+------------------------------------+--------------------------------------+
| owncloud_name | ldap_dn                            | directory_uuid                       |
+---------------+------------------------------------+--------------------------------------+
| oc1           | cn=oc1,ou=owncloud,dc=oc,dc=local  | F817C97B-4E64-42E1-90EB-CCC861282D25 |
| oc_2          | cn=oc_2,ou=owncloud,dc=oc,dc=local | 9DC1C24F-A349-4AA7-9F96-AB8AB5FBB046 |
+---------------+------------------------------------+--------------------------------------+
2 rows in set (0.00 sec)
```

Nach der Löschung des users:

```
MariaDB [owncloud]> select * from oc_ldap_user_mapping;
+---------------+------------------------------------+--------------------------------------+
| owncloud_name | ldap_dn                            | directory_uuid                       |
+---------------+------------------------------------+--------------------------------------+
| oc_2          | cn=oc_2,ou=owncloud,dc=oc,dc=local | 9DC1C24F-A349-4AA7-9F96-AB8AB5FBB046 |
+---------------+------------------------------------+--------------------------------------+
1 row in set (0.00 sec)
```

-----------------------------------------------------------------------------------------------------------------------------------------------------------

Vor der Löschung des Users

```
MariaDB [owncloud]> select * from oc_accounts;
+----+-------+---------+---------------+--------------+-------+------------+--------------------------+------------------------------+-------+
| id | email | user_id | lower_user_id | display_name | quota | last_login | backend                  | home                         | state |
+----+-------+---------+---------------+--------------+-------+------------+--------------------------+------------------------------+-------+
|  1 | NULL  | admin   | admin         | admin        | NULL  | 1547474099 | OC\User\Database         | /var/www/owncloud/data/admin |     1 |
|  2 | NULL  | oc1     | oc1           | oc1          | NULL  | 1547474077 | OCA\User_LDAP\User_Proxy | /var/www/owncloud/data/oc1   |     1 |
|  3 | NULL  | oc_2    | oc_2          | oc_2         | NULL  |          0 | OCA\User_LDAP\User_Proxy | /var/www/owncloud/data/oc_2  |     1 |
+----+-------+---------+---------------+--------------+-------+------------+--------------------------+------------------------------+-------+
3 rows in set (0.00 sec)
```

Nach der Löschung des users:

```
MariaDB [owncloud]> select * from oc_accounts;
+----+-------+---------+---------------+--------------+-------+------------+--------------------------+------------------------------+-------+
| id | email | user_id | lower_user_id | display_name | quota | last_login | backend                  | home                         | state |
+----+-------+---------+---------------+--------------+-------+------------+--------------------------+------------------------------+-------+
|  1 | NULL  | admin   | admin         | admin        | NULL  | 1547474099 | OC\User\Database         | /var/www/owncloud/data/admin |     1 |
|  3 | NULL  | oc_2    | oc_2          | oc_2         | NULL  |          0 | OCA\User_LDAP\User_Proxy | /var/www/owncloud/data/oc_2  |     1 |
+----+-------+---------+---------------+--------------+-------+------------+--------------------------+------------------------------+-------+
2 rows in set (0.00 sec)
```
