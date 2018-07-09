title: hbase utils
date: 2018-07-09 15:01:36
tags:
- hbase
---
# hbase filter
```bash
scan 'XXRPT_HGSTELEPHONYREPORT_2018-07-01', {COLUMNS => 'INFO:CONFID', FILTER => "ValueFilter( =, ‘substring:687754' )", LIMIT=>1}
```

```bash
scan 'XXRPT_HGSMEETINGREPORT_2018-06-25',{FILTER=>"SingleColumnValueFilter('INFO','SITEID',=,'binary:971082')"}
```