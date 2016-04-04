1. make new empty repo in github
2. install October CMS locally (removing existing VSC when promoted)
```
composer create-project october/october myproject dev-master
```
3. clone the repo to a temp dir then move `.git` folder
```
git clone --no-checkout repo-to-clone myproject/myproject.tmp
mv myproject/myproject.tmp/.git myproject/
rmdir myproject/myproject.tmp
cd myproject
```
4. update config files

**app.php**
```
    'url' => env('APP_URL', 'http://localhost'),
```
**cms.php**
```
	'enableRoutesCache' => env('CMS_ROUTE_CACHE', false),
	...
	'enableAssetCache' => env('CMS_ASSET_CACHE', false),
```
**database.php**
```
	'host'      => env('DB_HOST', 'localhost'),
	...
	'database'  => env('DB_DATABASE', 'homestead'),
	'username'  => env('DB_USERNAME', 'homestead'),
	'password'  => env('DB_PASSWORD', 'secret'),
```
**mail.php**
```
	'driver' => env('MAIL_DRIVER', 'mailgun'),
	...
	'from' => ['address' => env('MAIL_ADDRESS', 'no-reply@domain.com'), 'name' => env('MAIL_NAME', 'Administrator')],
	...
	'pretend' => env('MAIL_PRETEND', false),
```
**services.php**
```
	'mailgun' => [
		'domain' => env('SERVICES_MAILGUN_DOMAIN', ''),
		'secret' => env('SERVICES_MAILGUN_SECRET', ''),
	],
```
5. create local `.env` file with the following:
```
DB_HOST=localhost
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret

CMS_ROUTE_CACHE=false
CMS_ASSET_CACHE=false
CMS_CSRF=false
CMS_LINK_POLICY='detect'

APP_URL='http://www.yourdomain.com'
APP_LOCALE=en

MAIL_DRIVER=mailgun
MAIL_ADDRESS='no-reply@domain.com'
MAIL_NAME='Administrator'
MAIL_PRETEND=false

SERVICES_MAILGUN_DOMAIN=''
SERVICES_MAILGUN_SECRET=''
```

6. run the `php artisan october:up` command in initialize October CMS
7. login to the website and change default admin details
```
username: admin
password: admin
```
8. create a new blank theme, activate it and delete the demo theme
9. update the `.gitignore` file
```
...
# more folders
/themes/**/assets/node_modules
/themes/demo
/plugins
```
10. clear the `README.md` file
11. remove the `October.Demo` plugin
12. add git repo into desktop app, commit to `master` then sync
13. create `dev` and `web` branch and publish to github



4. commit all changes and push to repo
3. create `dev` and `web` branch and publish to github
4. make new forge site:
5. remove "public" Web Directory
6. make site
7. connect to `web` repo
8. uncheck "Install Composer Dependencies" repository
9. edit deploy script: remove 2 lines:
```
composer install --no-interaction --no-dev --prefer-dist
php artisan migrate --force
```
add line:
```
php artisan october:up
```
10. Turn on Quick Deploy in Forge
11. download october installer on local system
12. push to github
13. deploy once in forge
14. Install a site locally and install a site on your forge location ("from scratch")
15. delete `config` folder on forge
```
rm -rf config/
```
15. Delete install.php and /install_files locally
16. create .gitignore locally:
```
.env
.DS_Store
*.log
/vendor
/storage
/plugins
/themes/demo
/themes/**/assets/node_modules
.htaccess
artisan
index.php
```
17. update config files

**app.php**
```
    'url' => env('APP_URL', 'http://localhost'),
```
**cms.php**
```
	'enableRoutesCache' => env('CMS_ROUTE_CACHE', false),
	...
	'enableAssetCache' => env('CMS_ASSET_CACHE', false),
```
**database.php**
```
	'host'      => env('DB_HOST', 'localhost'),
	...
	'database'  => env('DB_DATABASE', 'homestead'),
	'username'  => env('DB_USERNAME', 'homestead'),
	'password'  => env('DB_PASSWORD', 'secret'),
```
**mail.php**
```
	'driver' => env('MAIL_DRIVER', 'mailgun'),
	...
    'from' => ['address' => env('MAIL_ADDRESS', 'no-reply@domain.com'), 'name' => env('MAIL_NAME', 'Administrator')],
    ...
    'pretend' => env('MAIL_PRETEND', false),
```
**services.php**
```
    'mailgun' => [
        'domain' => env('SERVICES_MAILGUN_DOMAIN', ''),
        'secret' => env('SERVICES_MAILGUN_SECRET', ''),
    ],
```
1. create local and production `.env` files with the following:
```
DB_HOST=localhost
DB_DATABASE=homestead
DB_USERNAME=homestead
DB_PASSWORD=secret

CMS_ROUTE_CACHE=false
CMS_ASSET_CACHE=false
CMS_CSRF=false

APP_URL='http://www.yourdomain.com'
APP_LOCALE=en

MAIL_DRIVER=mailgun
MAIL_ADDRESS='no-reply@domain.com'
MAIL_NAME='Administrator'
MAIL_PRETEND=false

SERVICES_MAILGUN_DOMAIN=''
SERVICES_MAILGUN_SECRET=''
```
