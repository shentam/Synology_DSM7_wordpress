# Synology_DSM7_wordpress

Synology changed folder name"web" into "web_packages"
the folder name changing made wordfence out of work.

After turn on xdebug and display_errors in application centre->webstation->script language setting->wordpress,I found following code display on my site.

then I've tried to find out what's the problem about the wordfence. Since 1 165164 @135645 Aug 17, 2021 said that Synology change the folder "web_packages", I guess it maybe path issue, so I've changed several files such as

/volume1/web_packages/wordpress/user.ini line3 into "auto_prepend_file = '/volume1/web_packages/wordpress/wordfence-waf.php'"

/volume1/web_packagesr/wordpress/wordfence-waf.php line 4 into

"if (file_exists('/volume1/web_packages/wordpress/wp-content/plugins/wordfence/waf/bootstrap.php')) {
define("WFWAF_LOG_PATH", '/var/services/web_packages/wordpress/wp-content/wflogs/');
include_once '/volume1/web_packages/wordpress/wp-content/plugins/wordfence/waf/bootstrap.php';"

/volume1/web_packages/wordpress/wp-config.php line24 into

"define( 'WPCACHEHOME', '/volume1/web_packages/wordpress/wp-content/plugins/wp-super-cache/' );"



Eventually it's working now.

https://community.synology.com/enu/forum/10/post/144882?page=1&reply=458086
