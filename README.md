#### A small bash script to find top database users by MySQL queries in last 1m. I use this script on cPanel servers and with Zabbix as trigger. 

 * Create a directory for store txt files and script itself. For example, ```path/to/db_abusers/``` 
 * Make sure that your script has the appropriate executable permission ```chmod +x path/to/db_abusers/script.sh```
 * You can change the ```head -n 10``` for more results.  

## Usage
```sh /path/to/db_abusers/db-abusers.sh | sort -nr | head -n 10 > /path/to/db_abusers/$(date +%Y%m%d-%H-%M)-db_abusers.txt```

You can use this script standalone if you want. I use with [db_abusers-post.sh](https://github.com/yigitgokcu/cpanel-db_abusers/blob/main/db_abusers-post.sh) to send the list to a Mattermost channel when my Zabbix trigger "MySQL: Large number of queries on {HOST.NAME} in last 1m{host:mysql.queries.rate.last(1m)}>=1500" got activated. You must create a "Trigger Action" on Zabbix in order to use like this.  

 * Dont forget to copy the Webhook URL and Channel name from the Mattermost App created into the WEBHOOK_URL and CHANNEL portions of the [db_abuserspost.sh](https://github.com/yigitgokcu/cpanel-db_abusers/blob/main/db_abusers-post.sh)

This script can be useful when it comes to check accounts specifically. For example, some http requests (bots or other malicious requests...) can make unnecessary loads. Especially on accounts with unoptimized queries.
