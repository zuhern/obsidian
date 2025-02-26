---
Created: Invalid date
Updated: Invalid date
---
ps -ax | grep mysql

//stop and kill any MySQL processes

brew remove mysql

brew cleanup

sudo rm /usr/local/mysql

sudo rm -rf /usr/local/var/mysql

sudo rm -rf /usr/local/mysql*

sudo rm ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist

sudo rm -rf /Library/StartupItems/MySQLCOM

sudo rm -rf /Library/PreferencePanes/My*

launchctl unload -w ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist

sudo vim /etc/hostconfig

//and remove the line MYSQLCOM=-YES-

rm -rf ~/Library/PreferencePanes/My*

sudo rm -rf /Library/Receipts/mysql*

sudo rm -rf /Library/Receipts/MySQL*

sudo rm -rf /private/var/db/receipts/*mysql*

//restart your computer just to ensure any MySQL processes are killed

//try to run mysql, it shouldn't work

brew doctor //and fix any errors

brew update

brew install mysql

mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql

mysql.server start