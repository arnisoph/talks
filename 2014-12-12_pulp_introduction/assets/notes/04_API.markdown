```
tail -f /var/log/httpd/*log

yum install python-yaml

pulp-admin rpm repo create --repo-id=custom-head-rhel-7.0-x86_64-standard --relative-url=customrepo/ --serve-http=true --serve-https=true
python pulp.py -v -c pulp.yaml -s /var/tmp/status
```



```
pulp-admin rpm repo create --repo-id=epel-head-el-7-x86_64-standard --feed=http://download.fedoraproject.org/pub/epel/7/x86_64/ --relative-url=epel/ --serve-http=true --serve-https=true
pulp-admin rpm repo create --repo-id=os-head-centos-7.0-x86_64-standard --feed=http://mirror.eu.oneandone.net/linux/distributions/centos/7.0.1406/os/x86_64/ --relative-url=centos/ --serve-http=true --serve-https=true

```
