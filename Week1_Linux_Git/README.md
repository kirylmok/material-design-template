### 1. For git and nginx installation I was using this commands:

```bash
sudo apt update 
sudo apt upgrade
sudo apt install nginx
sudo apt install git
```

### After git installation I configure global config file with this commands:

```git
git config --global user.name "Kiryl Makeichau" 
git config --global user.email "kirylm@playtika.com"
```

### 2. After configuring git I generate ssh key and clone repo:

```bash
ssh-keygen
```
```git
git clone git@github.com:kirylmok/material-design-template.git
```

### 3. Then I setup cron job to checkout main branch every minute:

```bash
crontab -e
```

### Edit crontab file like this:

```bash
* * * * * cd /home/kirylm/assessement/material-design-template && git pull git@github.com:kirylmok/material-design-template.git
```

### With this command I check that cron job was configured successfully:

```bash
sudo cat /var/log/syslog 
```

<img src="./.images/cron%20log.png"
	alt="Cron log screenshot"
	style="float: left;" />

### 4. Then I changed index.html file and push changes to git:

```git
nano index.html
git add .
git commit -m "Changes in index.html"
git push origin master
```

### After pushing changes I fixed nginx config to see changes at template:

nginx config located in /etc/nginx/sites-enabled/default, with nano I edited it

```bash
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	#Changed this root to template 
	root /home/kirylm/assessement/material-design-template/www;

	index index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {
		try_files $uri $uri/ =404;
	}
```

### ** To squash all my commits in one I used this command:

```git
git rebase -i 
```

<img src="./.images/git%20log%20before%20squash.png"
     alt="Git log before squash screenshot"
     style="margin-left: auto;
  margin-right: auto; width:600px; height:400px;" />

<img src="./.images/git%20log%20after%20squash.png"
     alt="Git log after squash screenshot"
     style="margin-left: auto;
  margin-right: auto; width:600px; height:400px;" />