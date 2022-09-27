# Getting Started

Congratulations on your purchase of this script. This is an introduction on how to get started.

In order to run this script, you need to have a webserver that can run PHP code. 

Here are the requirements.

## Requirements
* PHP >= 7.4
* MySQL (PostgreSQL works too. You need to set up the connection parameters accordingly.)

## Steps to Deploy on Shared Hosting
To deploy on shared hosting:
1. Create a folder (say `crypto-hyip-online`) outside your webroot folder.
2. Copy / upload all files in `crypto-hyip-pro` folder from your extracted archive into it. If there is no `.env` file in the root folder, create a `.env` file and copy the contents of `.env.example` into it.
3. Move / copy all contents from `crypto-hyip-pro/public` into your webroot folder (`public_html` or `www` depending on your hosting company).
4. If you have purchased a theme, upload the folder to `crypto-hyip-online/themes/your-theme-name`. Also copy the `public` contents of the `public_html/themes/your-theme-name`
5. Edit `public_html/index.php` and do the following replacements.

```php
// from 
if (file_exists($maintenance = __DIR__.'/../storage/framework/maintenance.php')) {
    require $maintenance;
}
// to
if (file_exists($maintenance = __DIR__.'/../crypto-hyip-online/storage/framework/maintenance.php')) {
    require $maintenance;
}

// from
require __DIR__.'/../vendor/autoload.php';

// to
require __DIR__.'/../crypto-hyip-online/vendor/autoload.php';


// from 
$app = require_once __DIR__.'/../bootstrap/app.php';

// to 
$app = require_once __DIR__.'/../crypto-hyip-online/bootstrap/app.php';

```

5. Create a database, take note of the database `username`, `password`, `database name`. Be sure to grant the database user full privileges to the database.

6. Create an email account. Take note of the `smtp` settings.

7. Navigate to `https://yourdomain.com/install` to begin the installation process. Fill the form with the details noted earlier. Click the button to continue. You will be taken to step 2. Click on `Continue` to begin database migration and seeding. **Note that this might take a while depending on your server**.

8. Once it's done, you'll see buttons to Go to homepage or register page. The first account created will be assigned as the `admin` of the website. **Please use a very secure password here.**

**Note: To make any changes after installation, locate `/.env` file and make the corrections there.** 

9. Set your cron job as follows...
```bash
*/5 * * * * cd /path/to/your/crypto-hyip-online && /usr/local/bin/php artisan schedule:run >> /dev/null 2>&1

```

That is set to run once every 5 minutes. Please note that `minutely` plans in the admin panel will not work on shared hosting. So let your pricing plans start from hourly.

However if your hosting supports per minute run...
```bash
* * * * * cd /path/to/your/crypto-hyip-online && /usr/local/bin/php artisan schedule:run >> /dev/null 2>&1

```
**NOTE:** All cron job outputs are logged in `crypto-hyip-online/storage/logs/`. If you do not see `calculate_interest.log` file here, please check for error messages in `laravel.log`. It's possible you'll get this error message:
```
local.ERROR: The Process class relies on proc_open, which is not available on your PHP installation.
```

If that is the case, contact your hosting provider for assistance.

You can then proceed to [Admin Documentation](../02-admin-dashboard/README.md) to learn about the admin interface.

## Steps to Deploy on VPS
This script was built with Laravel. You need to have an idea of DevOps to put this up. There are also managed services as mentioned in the following article. [Follow this guide](https://sujipthapa.co/blog/how-to-deploy-laravel-application-to-vps-server) to get it up on your VPS Server.
Almost everything in `Deploy to Shared Hosting` above applies. Take note of these:
* You do not need to move files from `./public/` folder. Just proceed as normal Laravel App.
* You do not need to make changes to your `./public/index.php` file.
* Once you're done pushing the script online, visit `https://your-domain.com/install` to begin script installation.
* Follow through the form to complete the setup. Make sure to have created an email.
* You can set your cron jobs to run every minute. You can use all available investment settings, including `profit frequency` of `minutely`.

**Note: To make any changes after installation, locate `/.env` file and make the corrections there.** 

_Happy Hacking!!!_