---
layout: post
author: Chaz Lee
title: How to fix the issues while setting up
date: 2020-07-04T20:00:20.613Z
thumbnail: /assets/img/posts/hello.jpg
category: Tutorial
summary: Issues & links to fix them
---
#####  __Guides to set up the pages?__
#####   Solution: 
-  [Github url](https://github.com/sujaykundu777/devlopr-jekyll)
-  [Install Guides](https://devlopr.netlify.app/get-started/#/)
-  [Jekyll offical guides](https://jekyllrb.com/docs/themes/)
-  [Markdown cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#code)


&nbsp;
&nbsp;
#####  __There was an error while trying to write to ```path to .bundle/.bundle/cache/compact_index/rubygems.org.443.29b0360b937aa4d161703e6160654e47/versions‘```. It is likely that you need to grant write permissions for that path.__
#####   Solution: 
This is caused not correctly installed builder or ruby, so need to uninstall and reinstall the not correct one. Follow the link [uninstall gem](https://stackoverflow.com/questions/21384664/how-to-uninstall-all-gems-installed-using-bundle-install) and [here](https://stackoverflow.com/questions/37720892/you-dont-have-write-permissions-for-the-var-lib-gems-2-3-0-directory) to __install ruby in rbenv__ and install gem. 

__Uninstall gem__ ```gem list --no-versions | xargs gem uninstall -a```
&nbsp;
1.  First, update the packages index and install the packages required for the ruby-build tool to build Ruby from source:
```javascript 
sudo apt-get remove ruby
sudo apt update
sudo apt install git curl libssl-dev libreadline-dev zlib1g-dev autoconf bison build-essential libyaml-dev libreadline-dev libncurses5-dev libffi-dev libgdbm-dev
```
2.  Next, run the following curl command to install both rbenv and ruby-build:
```javascript
curl -sL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-installer | bash -
```
3.  Add $HOME/.rbenv/bin to the system PATH. If you are using Bash, run:
```javascript
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
source ~/.bashrc
```
    If you are using Zsh run:
```javascript
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(rbenv init -)"' >> ~/.zshrc
source ~/.zshrc
```
4.  Install the latest stable version of Ruby(2.7.2 for 07/2020) and set it as a default version with:

```javascript
rbenv install 2.7.1
rbenv global 2.7.1
```
   To list all available Ruby versions you can use: ```rbenv install -l```
5.  Verify that Ruby was properly installed by printing out the version number:
```ruby -v```

__How To Install rubygems__
```javascript
sudo apt-get install rubygems
```

&nbsp;
&nbsp;
#####  __You have already activated json 2.1.0, but your Gemfile requires json 2.3.1.__
#####   Solution: 
In Gemfile add below ``` gem 'json', '=2.1.0' ``` and run ```bundle update json ``` in terminal, would auto remove json 2.3.1.

&nbsp;
&nbsp;
#####  __You have already activated mercenary 0.4.0, but your Gemfile requires mercenary 0.3.6.__
#####   Solution: 
This is caused by configuration in Gemfile instead of version issue. Comment the ``` gem 'jekyll', '~> 4.0.0' ``` and uncomment ```gem "github-pages", group: :jekyll_plugins ```