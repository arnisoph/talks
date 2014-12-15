# Install mongodb, qpid

```
yum install mongodb-server qpid-cpp-server qpid-cpp-server-store

echo auth=no >> /etc/qpid/qpidd.conf

for s in mongod qpidd; do systemctl enable $s; systemctl start $s; done

yum groupinstall pulp-server-qpid pulp-admin
yum install pulp-rpm-admin-extensions pulp-rpm-plugins
```

Verify broker is running:

```
systemctl status qpidd
```

Optionally disabling SSLv3:
```
ed -s /etc/httpd/conf.d/ssl.conf <<< $',s/SSLProtocol all -SSLv2/SSLProtocol all -SSLv2 -SSLv3/g\nw'
```


Continue:

```
systemctl stop httpd
sudo -u apache pulp-manage-db

ed -s /etc/default/pulp_workers <<< $',s/# PULP_CONCURRENCY=4/PULP_CONCURRENCY=1/g\nw'

for s in pulp_workers httpd pulp_celerybeat pulp_resource_manager; do systemctl enable $s; systemctl restart $s; done
```

Verify pulp_workers is running
```
systemctl status pulp_worker-0
```

Don't do the following in production ;)
```
ed -s /etc/pulp/admin/admin.conf <<< $',s/verify_ssl = True/verify_ssl = False/g\nw'
```

Verify login works, default password is 'admin' (``grep pass /etc/pulp/server.conf``):
```
pulp-admin login -u admin
```
