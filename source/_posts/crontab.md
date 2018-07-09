title: crontab
date: 2018-07-09 16:58:26
tags:
- crontab
- shell
---
# commands:
- crontab -l
- crontab -e

# set up:
```bash
0 2 * * * sh /home/test/scripts/test.sh `date --date='-1 day' +%Y-%m-%d` > /home/test/logs/test.log 2>&1
```