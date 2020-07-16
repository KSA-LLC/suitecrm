FROM spencerfirmllc/mysql
MAINTAINER git@ksa.llc

ADD https://s3.amazonaws.com/assets.ksa.llc/suitecrm.zip suitecrm.zip

RUN MySQL --user=root --password="2v3%ZRe#vHhG" --connect-expired-password -Bse "ALTER USER 'root'@'localhost' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "CREATE DATABASE suitecrm CHARACTER SET utf8 COLLATE utf8_bin;" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'crm'@'localhost' IDENTIFIED BY 'crm2020!';" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'crm'@'%' IDENTIFIED BY 'crm2020!';" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `suitecrm` . * TO 'crm'@'localhost' IDENTIFIED BY 'crm2020!' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `suitecrm` . * TO 'crm'@'%' IDENTIFIED BY 'crm2020!' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "SHOW DATABASES;"

RUN powershell -Command \
  Expand-Archive -Path c:\suitecrm.zip -DestinationPath C:\inetpub\wwwroot ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /INHERITANCE:R ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /T /C /L /Q /GRANT BUILTIN\IIS_IUSRS:F ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /T /GRANT Administrators:F ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /setowner BUILTIN\IIS_IUSRS /T /C /L /Q
RUN powershell -command rm -Recurse c:\*.zip -Force
