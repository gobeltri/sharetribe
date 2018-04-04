# Sharetribe (7.3.0)

## Development

### C9: Rails workspace (Ubuntu 14.04)

```bash
# New git repo from Sharetribe v7.3.0
git clone https://github.com/sharetribe/sharetribe.git
git checkout tags/v7.3.0 -b v7.3.0
rm -Rf .git
git init . && git add . && git commit -m "Init from Sharetribe 7.3.0: https://github.com/sharetribe/sharetribe/tree/v7.3.0"
```


```bash
# Dependencies
lsb_release -a
nvm install 7.8 && nvm use 7.8
sudo apt-get update
sudo apt-get install imagemagick
sudo apt-get install sphinxsearch
```

```bash
# MySQL 5.7
wget http://dev.mysql.com/get/mysql-apt-config_0.6.0-1_all.deb
sudo dpkg -i mysql-apt-config_0.6.0-1_all.deb
sudo apt-get update
sudo apt-get install mysql-server
mysql --version
sudo mysql_upgrade
```

```bash
# Packages
bundle install
npm install
```

```bash
# Create MySQL DBs and users && Update database.yml file
cp config/database.example.yml config/database.yml
mysql -u root -p
```

```sql
CREATE DATABASE sharetribe_test CHARACTER SET utf8 COLLATE utf8_general_ci;
CREATE DATABASE sharetribe_development CHARACTER SET utf8 COLLATE utf8_general_ci; 
GRANT all privileges ON sharetribe_development.* TO 'sharetribe'@'localhost' IDENTIFIED BY 'secret';
GRANT all privileges ON sharetribe_test.* TO 'sharetribe'@'localhost' IDENTIFIED BY 'secret';
```

```bash
# Start app
bundle exec rake db:create db:structure:load
bundle exec rake assets:precompile
bundle exec rake ts:index
bundle exec rake ts:start
# ***(NOT WORKING)*** foreman start -f Procfile.static
bundle exec rake jobs:work
bundle exec rails server -p $PORT -b $IP
```

```ruby
# Configure from webpage and wait till breaks. Then change this on DB and reload webpage.
# http://<c9-workspace>-<c9-username>.c9users.io
# bundle exec rails c
c.domain = '<c9-workspace>-<c9-username>.c9users.io'
c.use_domain = true
c.save
```
