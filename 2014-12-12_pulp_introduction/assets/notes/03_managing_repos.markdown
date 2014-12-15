# Mirror a repository
```
pulp-admin rpm repo create --repo-id=foreman --feed=http://yum.theforeman.org/releases/1.1/el6/x86_64/ --relative-url=foreman --serve-http=true --serve-https=true
pulp-admin rpm repo sync run --repo-id=foreman
```

Verify: http://127.0.0.1:80/pulp/repos/



# Create a repository
```
pulp-admin rpm repo create --repo-id=mycustomrepo --relative-url=custom/repo/ --serve-http=true --serve-https=true
pulp-admin rpm repo publish run --repo-id=mycustomrepo
```

Verify: http://127.0.0.1:80/pulp/repos/

```
yum install --downloadonly --downloaddir=/var/tmp/saltpkgs/ salt-minion
pulp-admin rpm repo uploads rpm --repo-id=mycustomrepo --dir=/var/tmp/saltpkgs/
pulp-admin rpm repo publish run --repo-id=mycustomrepo
```

Verify: http://127.0.0.1:80/pulp/repos/


# List available repositories

## List IDs and names only:
```
pulp-admin repo list -s
```

## More details:
```
pulp-admin repo list
```

## Even more details:
```
pulp-admin repo list --details
```

# Search for packages
```
pulp-admin rpm repo content rpm --repo-id=mycustomrepo --match='name=salt.*'
```

# Copy packages
```
pulp-admin rpm repo copy rpm --from-repo-id=foreman --to-repo-id=mycustomrepo --match='name=foreman-libvirt.*'
pulp-admin rpm repo publish run --repo-id=mycustomrepo
```

Verify: http://127.0.0.1:80/pulp/repos/custom/repo/

# Remove packages
```
pulp-admin rpm repo remove rpm --repo-id=mycustomrepo --match='name=foreman-libvirt.*'
pulp-admin rpm repo publish run --repo-id=mycustomrepo
```

Verify: http://127.0.0.1:80/pulp/repos/custom/repo/

# Remove repository
```
pulp-admin rpm repo delete --repo-id=foreman
```

Verify: http://127.0.0.1:80/pulp/repos/

