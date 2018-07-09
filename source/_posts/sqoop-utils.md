title: sqoop utils
date: 2018-07-09 16:53:47
tags:
- sqoop
- spark
---
```bash
sqoop import -Dhbase.zookeeper.quorum={{zkAddr}} --connect jdbc:oracle:thin:@//{{host}}:{{port}}/{{serviceName}} --username {{username}} --password {{password}} --query "{{sql}}
 and \$CONDITIONS" --fields-terminated-by "\t" --lines-terminated-by "\n" --hbase-table {{tableName}} --column-family INFO --hbase-row-key SITEID -m 1  --hbase-create-table
```
