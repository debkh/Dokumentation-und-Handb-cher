Yii 2 Installing Project
===============================


PROJECT DEPLOYING
-----------------
 
### Linux/OS X

1) Run next commands in terminal

``` git clone https://github.com/project_name ```

``` cd project_name ```

``` git checkout work_branch_name ```

2) Ok, after that, we need a composer utility. Next commands will download composer and move them to global system namespace.

``` curl -s http://getcomposer.org/installer | php ```

``` mv composer.phar /usr/local/bin/composer ```


3) And we need to initialize our project with special init script in the project home directory (script will ask you about environment, please, choose development)

``` ./init ```


4) Yii2 also needs a composer plugin, you can install them with next command:

``` composer global require "fxp/composer-asset-plugin:1.0.0" ```


5) At last, let's install all dependencies from composer to our project

``` composer install --prefer-dist ```

6) Change DB configuration credentials in 

``` /common/config/main-local.php ```

7) Start migration in project directory

``` ./yii migrate ```

### Windows


1) Install XAMPP (or another server package) https://www.apachefriends.org/

2) Install GitHub Windows https://windows.github.com

3) Clone to your projects folder 

4) Install composer and init project ( you can find instructions in Linux/OS X manual )
 
4) Now, we need to configure virtual hosts for xampp. Run as administrator notepad, and open 

``` C:\windows\system32\drivers\etc\hosts ```

At the end of that file type:

``` 127.0.0.1      devinstance.dev ```

5) By default, xampp has only localhost host, we can add new one with following steps:
  * Open ``` C:\xampp\apache\conf\httpd.conf ``` and check line with ``` #Include etc/extra/httpd-vhosts.conf ``` they must be uncommented ```  Include etc/extra/httpd-vhosts.conf ```
  * Open ``` C:\xampp\appache\conf\extra\httpd-vhosts.conf ``` 
  * Add following lines for your new virtual host
  
  ```
  <VirtualHost *:80> 
      ServerName devinstance.dev 
      DocumentRoot "C:\projects\devinstance.dev" 
      <Directory "C:\projects\devinstance.dev"> 
          Options Indexes FollowSymLinks Includes ExecCGI 
          AllowOverride All 
          Require all granted 
      </Directory> 
      ErrorLog "logs/site.local-error_log" 
  </VirtualHost>
  ```
  * Restart your XAMPP server
  * Your can reach your project page by http://devinstance.dev



Git repository workflow
-----------------------

First of all, we need to pull latest changes from the server

``` git fetch ```

``` git rebase origin/development ```

``` git checkout -b feature_task_name ```

Now, you can add some new amazing stuff to project and make temp commits and push them via next commands

``` git add path_to_file or just . for all files ```

``` git commit -m "Feature task name comment" ```

``` git push origin development ```

When you finish work on task, just make commit&push as usually and make Pull Request on github.com.

All information about detailed framework architecture, configuration and workflow you can find at http://www.yiiframework.com/doc-2.0/guide-start-workflow.html

Also, you can ask any questions in slack chat room #general or by email dmitry.oplachko@faceit.com.ua


[![Latest Stable Version](https://poser.pugx.org/yiisoft/yii2-app-advanced/v/stable.png)](https://packagist.org/packages/yiisoft/yii2-app-advanced)
[![Build Status](https://travis-ci.org/yiisoft/yii2-app-advanced.svg?branch=master)](https://travis-ci.org/yiisoft/yii2-app-advanced)

DIRECTORY STRUCTURE
-------------------

```
common
    config/              contains shared configurations
    mail/                contains view files for e-mails
    models/              contains model classes used in both backend and frontend
console
    config/              contains console configurations
    controllers/         contains console controllers (commands)
    migrations/          contains database migrations
    models/              contains console-specific model classes
    runtime/             contains files generated during runtime
backend
    assets/              contains application assets such as JavaScript and CSS
    config/              contains backend configurations
    controllers/         contains Web controller classes
    models/              contains backend-specific model classes
    runtime/             contains files generated during runtime
    views/               contains view files for the Web application
    web/                 contains the entry script and Web resources
frontend
    assets/              contains application assets such as JavaScript and CSS
    config/              contains frontend configurations
    controllers/         contains Web controller classes
    models/              contains frontend-specific model classes
    runtime/             contains files generated during runtime
    views/               contains view files for the Web application
    web/                 contains the entry script and Web resources
    widgets/             contains frontend widgets
vendor/                  contains dependent 3rd-party packages
environments/            contains environment-based overrides
tests                    contains various tests for the advanced application
    codeception/         contains tests developed with Codeception PHP Testing Framework
```
