# JONY5 :: Website Configuration Instructions
### Difficulty Level :: Beginner (takes me 10-20 min + FTP time for 1.3GB)

##### Note: For simplicity of instruction, this configuration README expects the files to run from the root web directory of a subdomain or primary domain. The files can be placed deeper in the directory structure, but no instruction will be given here for that kind of implementation.

##### Note: Total file size is about 1.34GB with over 50% (862.2MB) from 3400+ rotating JPG images from jony5_files/common/imgs/banner_1180x250/. DON'T delete any PHP files here. Delete some of those JPG, if you lack sufficient server hard drive space. I deleted all but 16 banner JPG images, and the total file size dropped to 486.9MB.

##### Note: The Wordpress blog UI is busted. Sorry! New site is in the works, tho.  :)

## INSTRUCTIONS :: 
**1)** Download this repository.
**2)** Create a new MySQL database and a new user/password...,and keep this info handy.
**3)** Update the CRNRSTN :: database configuration file with the database information from step 2. "CYEXX_SOLUTIONS" is my PRODUCTION environment key, and I recommend one to use this addConnection() method call. Just replace the database specific information with your own. Then close the file (file path below).

> CRNRSTN :: Database Configuration File:
> jony5_files/config.database.secure/_crnrstn.db.config.inc.php

**4)** Using PHPMyAdmin (or whatever) and looking at the new database, cut and paste the database SQL file contents (file path below) into SQL editor, and run it. One could also do a SQL file import of this SQL table export to the same database. So many options here. 

> Database SQL file:
> jony5_database/jonyfivc_prod01.sql

**5)** Open the CRNRSTN :: configuration file (file path below), and prepare to configure the site to run from your domain or subdomain.

> CRNRSTN :: Configuration File:
> jony5_files/_crnrstn.config.inc.php

**6)** Uncomment _crnrstn.config.inc.php line 95, and put your email here. This is just for significant error notifications.
> Line 95 = $oCRNRSTN->initLogging('CYEXX_SOLUTIONS', 'EMAIL', 'your@email.com');

**7)** Update the path to the CRNRSTN :: database configuration file on _crnrstn.config.inc.php line 103 to match your production hosting PATH to the same file. Ya'll, I always screw this step up with new sites...and then, the site does not work as expected the first time in production; localhost still works though...because all my sh1t uses the same config path on VM. 
> Line 103 = $oCRNRSTN->addDatabase('CYEXX_SOLUTIONS', '/home2/jonyfivc/public_html/config.database.secure/_crnrstn.db.config.inc.php');

**8)** Update _crnrstn.config.inc.php lines 260 to 272 to match the domain, IP, and path values of the website production environment. Heads up, people...I always screw up the server value for DOCUMENT_ROOT, and the site breaks (same issue as in step 7 due to my dev setup). Also, DON'T add a trailing slash IF there is no slash (and vice-versa). OK. Lines reproduced below for reference:

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'DOMAIN', 'github.jony5.com');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'SERVER_NAME', 'github.jony5.com');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'SERVER_ADDR', '162.241.252.206');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'SERVER_PORT', '80');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'SERVER_PROTOCOL', 'HTTP/1.1');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'SSL_ENABLED', false);

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'DOCUMENT_ROOT', '/home2/jonyfivc/public_html/github.jony5.com');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'DOCUMENT_ROOT_DIR', '');		// FYI, this is for an install deeper than root directory. Use NO trailing slash.

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'ROOT_PATH_CLIENT_HTTP', 'http://github.jony5.com/');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'ROOT_PATH_CLIENT_HTTP_DIR', '');   // FYI, this is for HTTP access to install deeper than root directory. DO ADD trailing slash

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'PROXY_BANNER_IMAGES_ENDPOINT', 'http://github.jony5.com/common/imgs/banner_1180x250/_proxy_xml_request.php');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'WSDL_URI_MGMT', 'http://github.jony5.com/soa/crnrstnmgmt/1.0.0/wsdl/index.php?wsdl');

> $oCRNRSTN->defineEnvResource('CYEXX_SOLUTIONS', 'WSDL_URI', 'http://github.jony5.com/soa/crnrstn/1.0.0/wsdl/index.php?wsdl');

**9)** Save and close _crnrstn.config.inc.php, and then FTP the files to your web server.

**10)** Test the site by loading in web browser. The Wordpress blog UI is busted (no way to fix given my situation...and besides, a new Wordpress compatible site is in the works!), but if the rest works...it works.

# = = = = = = = = = = = = = = = = = = = = 
## CRON SYN FOR GLOBAL NAVIGATION BASSDRIVE SHOW INFORMATION :: 
> jony5_files/_cron/bassdrive_sync/?auth=xxxxsecret_keyxxxxx

## THE ACTUAL CRON CALL FROM JONY5 PRODUCTION ::
> */5	*	*	*	*	/usr/bin/curl http://github.jony5.com/_cron/bassdrive_sync/?auth=xxxxsecret_keyxxxxx > /dev/null 2>&1

# = = = = = = = = = = = = = = = = = = = =
## PATH TO BASSDRIVE META FILE OVERWRITES FROM CRON FIRE (WRITE PERMISSIONS HERE) ::  
>jony5_files/_proxy/bassdrive_sync/

## FILES THAT ARE UPDATED BY CRON ::
> jony5_files/_proxy/bassdrive_sync/stream_info.txt
> jony5_files/_proxy/bassdrive_sync/bassdrive_stats.txt
> jony5_files/_proxy/bassdrive_sync/bassdrive_broadcast_nation.txt


