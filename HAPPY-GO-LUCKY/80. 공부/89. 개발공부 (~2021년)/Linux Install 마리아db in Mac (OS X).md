---
Created: Invalid date
Updated: Invalid date
---
# Install Mariadb in Mac (OS X)

Open command prompt (Terminal),  
1. run : brew update  
if you haven't installed brew, run this to install brew : ruby -e "$(curl -fsSL  
[https://raw.github.com/mxcl/homebrew/go/install](https://raw.github.com/mxcl/homebrew/go/install))"  
then run : brew update  
2. run : brew install mariadb  
3. run : unset TMPDIR  
4. run : mysql_install_db --basedir={Installed Directory}  
for example, mysql_install_db --basedir=/usr/local/Cellar/mariadb/5.5.32  
5. run : mysql.server start (in bin directory, usr/local/Cellar/mariadb/5.5.32/bin)  
6. to connect mariadb, run : mysql -uroot  
7. in order to set secure options, run : mysql_secure_installation  
you can set the options for security as well as password of root account.  
Have a good day!