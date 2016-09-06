# Rails-Ruby-Redis (3R) with GitHub on CentOS 7
### Rails version 5.0.0.1
### Ruby version 2.3.0
### Redis version 2.8.19

## Software Installation and Setup
### Redis
- yum install redis

### Ruby
- yum install ruby

### Rails
- become root user or run each command with su -c "command"
- yum install gcc-c++ patch readline readline-devel zlib zlib-devel
- yum install libyaml-devel libffi-devel openssl-devel make
- yum install bzip2 autoconf automake libtool bison iconv-devel
- curl -sSL https://rvm.io/mpapis.asc | gpg --import -
- curl -L get.rvm.io | bash -s stable
- vi /etc/group (add username to rvm group)
- id username (to check the user's group)
- source /etc/profile.d/rvm.sh
- /usr/local/rvm/bin/rvm reload
- /usr/local/rvm/bin/rvm requirements run
- /usr/local/rvm/bin/rvm install 2.3.0
- /usr/local/rvm/bin/rvm use 2.3.0 --default
- cd /usr/bin; mv ruby ruby.old; ln -s /usr/local/rvm/rubies/ruby-2.3.0/bin/ruby .
- gem install rails
- gem install json
- gem install executable-hooks
- gem update bundler
- cd /usr/local/bin; ln -s /usr/local/rvm/rubies/ruby-2.3.0/bin/bundler .
- cd /usr/local/bin; ln -s /usr/local/rvm/rubies/ruby-2.3.0/bin/bundle .
- cd /usr/local/bin; ln -s /usr/local/rvm/rubies/ruby-2.3.0/bin/rails .
- cd /usr/local/bin; ln -s /usr/local/rvm/rubies/ruby-2.3.0/bin/rake .
- cd /usr/local/bin; ln -s /usr/local/rvm/rubies/ruby-2.3.0/bin/ruby_executable_hooks .
- exit root user



## Creating First Ruby-Rails Application
- cd into working directory to create a new application in new folder Ruby-Rails-Redis
- rails new Ruby-Rails-Redis
- cd Ruby-Rails-Redis
- su -c "/usr/local/bin/bundle install"
- bundle show
- /usr/local/bin/bundler update


## Ruby + Rails + Redis
- cd Ruby-Rails-Redis
- Create file ./config/initializers/redis.rb and add the following line:
  $redis = Redis.new(:host => 'localhost', :port => 6379)
- Update file Gemfile
  Add line:  gem 'redis'
- su -c "gem install redis"
- su -c "gem install redis-namespace"
- su -c "service redis restart"
- ps -ef | grep redis


## Running First Ruby-Rails Application
- cd Ruby-Rails-Redis
- ./bin/rails server
- this starts the Rails web server listening on default port 3000
- browse localhost:3000
- CTRL-C to stop web server



## Login into GitHub
- Create GitHub repository, for example, Ruby-Rails-Redis
- https://github.com/lancenle/Ruby-Rails-Redis.git (replace lancenle with your user name)

- echo "# Ruby-Rails-Redis" >> README.md
- git init
- git add README.md
- git commit -m "first commit"
- git remote add origin https://github.com/lancenle/Ruby-Rails-Redis.git
- git push -u origin master

- git remote add origin https://github.com/lancenle/Ruby-Rails-Redis.git
- git push -u origin master




On GitHub:
- create new repository named Ruby-Rails-Redis
- do not create ReadMe


On Local Server after creating GitHub repository
- git init
- git config --global user.email "username@domain.com"
- git config --global user.name "lancenle" 
- git add .
- git status
- git commit -m "initial commit"
- git log


## Optional GitHub private-public key set up
- ssh-keygen -t rsa -b 2048 -f ./githubkey
- mv githubkey ~/.ssh/githubprivatekey.pem

- Log into GitHub and put the public key (githubkey.pub) on GitHub (Edit profile->SSH and GPG keys)

- ssh -T git@github.com (test connection to github if private key is in default ~/.ssh/rd_rsa file)
- ssh -i ~/.ssh/githubprivatekey.pem git@github.com  (test connection to github if private key is in ~/.ssh/githubprivatekey.pem)



### Push to GitHub (with manual password or private key stored in default file ~/.ssh/id_rsa)
- git remote add origin https://github.com/lancenle/Ruby-Rails-Redis.git
- git push -u origin master


### Push to GitHub (with private key stored in ~/.ssh/githubprivatekey.pem)
- git remote add origin git@github.com/lancenle/Ruby-Rails-Redis.git
- ssh -i ~/.ssh/githubprivatekey.pem git@github.com "git push -u origin master"


### Update between HTTPS and SSH pushes
- git remote -v
- git remote set-url origin git@github.com:lancenle/Ruby-Rails-Redis.git
- git remote set-url origin https://github.com/lancenle/Ruby-Rails-Redis.git
