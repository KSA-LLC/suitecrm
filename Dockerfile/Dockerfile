# Apply image 10.0.14393.0
# Install update 10.0.14393.1480
# c:\windows\system32\cmd.exe
# c:\windows\system32\cmd.exe
# c:\windows\system32\cmd.exe
# c:\windows\system32\cmd.exe

FROM nanoserver/mysql
MAINTAINER git@ksa.llc

# ADD https://s3.amazonaws.com/assets.ksa.llc/suitecrm/suitecrm-7.11.zip suitecrm.zip
ADD https://s3.amazonaws.com/assets.ksa.llc/suitecrm.zip suitecrm.zip
ADD https://getcomposer.org/download/1.10.8/composer.phar composer.phar

RUN MySQL --user=root --password="2v3%ZRe#vHhG" --connect-expired-password -Bse "ALTER USER 'root'@'localhost' IDENTIFIED BY 'Password123';" & \
MySQL --user=root --password="Password123" -Bse "CREATE DATABASE suitecrm CHARACTER SET utf8 COLLATE utf8_bin;" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'crm'@'localhost' IDENTIFIED BY 'crm2020!';" & \
MySQL --user=root --password="Password123" -Bse "CREATE USER 'crm'@'%' IDENTIFIED BY 'crm2020!';" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `suitecrm` . * TO 'crm'@'localhost' IDENTIFIED BY 'crm2020!' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "GRANT ALL PRIVILEGES ON `suitecrm` . * TO 'crm'@'%' IDENTIFIED BY 'crm2020!' WITH GRANT OPTION;" & \
MySQL --user=root --password="Password123" -Bse "SHOW DATABASES;"

RUN powershell -Command \
  New-Item -ItemType "directory" -Path "c:\bin" ; \
  Copy-Item -Path c:\composer.phar -Destination c:\bin\composer.phar ; \
  Expand-Archive -Path c:\suitecrm.zip -DestinationPath C:\inetpub\wwwroot ; \
  Rename-Item -Path C:\inetpub\wwwroot\dunbarton -NewName "suitecrm" ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /INHERITANCE:R ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /T /C /L /Q /GRANT BUILTIN\IIS_IUSRS:F ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /T /GRANT Administrators:F ; \
  ICACLS C:\inetpub\wwwroot\suitecrm /setowner BUILTIN\IIS_IUSRS /T /C /L /Q
RUN powershell -command rm -Recurse c:\*.zip -Force
RUN powershell -command rm -Recurse c:\*.phar -Force


# 7.11
# RUN powershell -Command \
#   New-Item -ItemType "directory" -Path "c:\bin" ; \
#   Copy-Item -Path c:\composer.phar -Destination c:\bin\composer.phar ; \
#   Expand-Archive -Path c:\suitecrm.zip -DestinationPath C:\inetpub\wwwroot ; \
#   Rename-Item -Path C:\inetpub\wwwroot\SuiteCRM-master -NewName "suitecrm" ; \
#   ICACLS C:\inetpub\wwwroot\suitecrm /INHERITANCE:R ; \
#   ICACLS C:\inetpub\wwwroot\suitecrm /T /C /L /Q /GRANT BUILTIN\IIS_IUSRS:F ; \
#   ICACLS C:\inetpub\wwwroot\suitecrm /T /GRANT Administrators:F ; \
#   ICACLS C:\inetpub\wwwroot\suitecrm /setowner BUILTIN\IIS_IUSRS /T /C /L /Q
# RUN powershell -command rm -Recurse c:\*.zip -Force
# RUN powershell -command rm -Recurse c:\*.phar -Force
