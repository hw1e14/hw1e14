title: bash utils
date: 2018-07-09 14:52:49
tags:
- bash
- shell
---
# common utils:
- to lower case:
  > echo Happy | tr "[:upper:]" "[:lower:]"


# file operations:
- show file size with human readable format
  ```bash
  ls -lash
  ```
- List your top 10 favorite commands
  ```bash
  history | awk '{print $2}' | sort | uniq -c | sort -rn | head
  ```
- get  disk used percent
  ```bash
  df -hP {{disk_path}} | awk '{print $5}' |tail -1|sed 's/%$//g'
  ```
- sum total for column 4
  ```
  awk -F"\t" '{print;x+=$4}END{print "Total " x}' 2018-07-06.csv
  ```
- count file column number
  ```
  head -1 targetfile | sed 's/[^,]//g'|wc -c
  ```
- filter data rows
  ```
  cat jmtdata_AllSites_2018-07-06.csv |awk '{if($1=="303790" && $9=="2018-07-06") print $1,$9}'|wc -l
  ```
- send email
  ```
  echo -e "All CSV files are generated successfully \n Date: $2 $(date "+%H:%M:%S") \n Thanks, \n Test"| mail -s "Success" test@gmail.com
  ```
- sql insert
  ```
  echo -e "UPSERT INTO SAP_DATATELEMETRY VALUES('${rowKey}','${datatype}','0','${jobEndTIME}','0','${dataEntry}','$4');" > insert_jmt_telemetry.sql
  /opt/cloudera/parcels/APACHE_PHOENIX/lib/phoenix/bin/psql.py sap-zookeeper1-gsb:2181 insert_jmt_telemetry.sql
  ```

# Loop Func:
```shell
#!/usr/bin/env bash
# usage:
Usage () {
    echo -e "Usage: ./test.sh 2018-07-08 or ./test.sh 2018-07-08 2018-07-09"
}
Loop() {
    #do logic here
    jobtype=( daily weekly monthly )
    for i in "${jobtype[@]}"
    do
        hdfs dfs -getmerge /user/test/test.csv test.csv
    done
}

if [ "$#" -eq 1 ]
then
    Loop $1
elif [ "$#" -eq 2 ]
then
    startdate=$1
    enddate=$2

    curr="$startdate"
    while true; do
        echo "$curr"
        Loop $curr
        [ "$curr" \< "$enddate" ] || break
        curr=$( date +%Y-%m-%d --date "$curr +1 day" )
    done
else
    Usage
fi
```