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
	...
	'storage' => [
	
	        'uploads' => [
	            'disk'   => 's3',
	            'folder' => 'uploads',
	            'path'   => 'https://s3-'.env('FILE_AWS_REGION','').'.amazonaws.com/'.env('FILE_AWS_BUCKET', '').'/uploads/',
	        ],
	
	        'media' => [
	            'disk'   => 's3',
	            'folder' => 'media',
	            'path'   => 'https://s3-'.env('FILE_AWS_REGION','').'.amazonaws.com/'.env('FILE_AWS_BUCKET', '').'/media/',
	        ],
	
	    ],
```
**database.php**
```
	'host'      => env('DB_HOST', 'localhost'),
	...
	'database'  => env('DB_DATABASE', 'homestead'),
	'username'  => env('DB_USERNAME', 'homestead'),
	'password'  => env('DB_PASSWORD', 'secret'),
```
**filesystem.php**
```
	'default' => env('FILE_DEFAULT', 'local'),
	...
	's3' => [
            'driver' => env('FILE_AWS_DRIVER', 's3'),
            'key'    => env('FILE_AWS_KEY', ''),
            'secret' => env('FILE_AWS_SECRET', ''),
            'region' => env('FILE_AWS_REGION', ''),
            'bucket' => env('FILE_AWS_BUCKET', ''),
        ],
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

FILE_DEFAULT='s3'
FILE_AWS_DRIVER='s3'
FILE_AWS_KEY=''
FILE_AWS_SECRET=''
FILE_AWS_REGION=''
FILE_AWS_BUCKET=''
```

6. create a database with homestead
6. run the `php artisan october:up` command in initialize October CMS
7. login to the website and change default admin details
```
username: admin
password: admin
```
8. create a new blank theme, activate it and delete the demo theme
9. update the `.gitignore` file
```
# Numerous always-ignore extensions
*.bak
*.diff
*.err
*.orig
*.log
*.rej
*.swo
*.swp
*.vi
*.idea
.sass-cache
composer.phar
.env
.env.*.php
.env.php
php_errors.log
nginx-error.log
nginx-access.log
nginx-ssl.access.log
nginx-ssl.error.log
php-errors.log
sftp-config.json
selenium.php
composer.lock

# OS or Editor folders
.DS_Store
._*
Thumbs.db
.cache
.project
.settings
.tmproj
nbproject
*.sublime-project
*.sublime-workspace

# Dreamweaver added files
_notes
dwsync.xml

# folders to ignore
node_modules
bower_components
/bootstrap/compiled.php
/vendor

# for netbeans
nbproject

# more folders
/themes/**/assets/node_modules
/themes/demo
```
10. clear the `README.md` file
11. remove the `October.Demo` plugin
12. create a project at [October CMS - Projects](https://octobercms.com/account/project/dashboard)
13. add all required plugins to the project [October CMS Plugins](https://octobercms.com/plugins)
14. sync the plugins to local
15. clone any private plugins from Git then run `php artisan october:up`
16. add git repo into desktop app, commit to `master` then sync
17. create `dev` and `web` branch and publish to github


4. make new forge site
5. remove "public" Web Directory
7. connect to `web` repo
8. uncheck "Install Composer Dependencies" repository
9. edit deploy script: remove 2 lines:
```
php artisan migrate --force
```
add line:
```
php artisan october:up
```
10. Turn on Quick Deploy in Forge
11. Deploy now (this will fail)
12. stop NGIX and MySQL services and run `composer install`
13. restart Ngix and MySQL services
14. create a `.env` for production
14. run `php artisan october:up`
15. setup SSL certificate
16. set your active theme `php artisan theme:use myproject-theme`
17. login to the website and change default admin details
```
username: admin
password: admin
```
18. attach forge install to project
19. download plugins
20. clone any private plugins from Git then run `php artisan october:up`


# sync from forge
1. commit changes from server and push to `web` branch
2. using desktop app sync `web` branch then merge it into `dev` branch
3. to complete merge `dev` into `master`

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
# Numerous always-ignore extensions
*.bak
*.diff
*.err
*.orig
*.log
*.rej
*.swo
*.swp
*.vi
*.idea
.sass-cache
composer.phar
.env
.env.*.php
.env.php
php_errors.log
nginx-error.log
nginx-access.log
nginx-ssl.access.log
nginx-ssl.error.log
php-errors.log
sftp-config.json
selenium.php
composer.lock

# OS or Editor folders
.DS_Store
._*
Thumbs.db
.cache
.project
.settings
.tmproj
nbproject
*.sublime-project
*.sublime-workspace

# Dreamweaver added files
_notes
dwsync.xml

# folders to ignore
node_modules
bower_components
/bootstrap/compiled.php
/vendor

# for netbeans
nbproject
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

FILE_DEFAULT='s3'
FILE_AWS_DRIVER='s3'
FILE_AWS_KEY=''
FILE_AWS_SECRET=''
FILE_AWS_REGION=''
FILE_AWS_BUCKET=''
```
