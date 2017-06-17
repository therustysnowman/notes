Summary of site deployment using git

# Overview

Site developed in git

Expected web server folder layout:

* ```/<root>/repo/<site>.git``` - git repo on web server
* ```/<root>/www/<site>``` - git content on web server

# Web server setup

```
mkdir /<root>/repo/<site>.git
cd /<root>/repo/<site>.git

git init --bare

cat >> hooks/post-receive << EOF
#!/bin/sh
git --work-tree=/<root>/www/<site> --git-dir=/<root>/repo/<site>.git checkout -f
EOF

chmod +x hooks/post-receive
```

# Deploying a repository to the site

```
git remote add <alias> ssh://<user>@<server>/<root>/repo/<site>.git
git push <alias> <branch>
```
