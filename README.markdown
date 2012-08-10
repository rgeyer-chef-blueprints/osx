# Description

This is a set of Chef recipes that I use to configure an OSX system to my liking.  There are some configurable options in the example node.json.* files.

# Requirements

* Chef 0.10.x or Chef 10.x (Tested with Chef Solo, and will probably work best that way)
* An OSX computer.  Tested on OSX 10.5, probably similarly compatible with later versions

# Usage

Assuming you've got Chef already installed..

Clone this repo...

```
git clone git://github.com/rgeyer-chef-blueprints/osx.git ~/osx_blueprint
```

Configure a Chef Solo file to point to those cookbooks...
```
require 'rubygems'
require 'ohai'
o = Ohai::System.new
o.all_plugins

file_cache_path "~/.chef/cache"
cookbook_path ["~/osx_blueprint/cookbooks"]
```

_Pro Tip:_ You should probably use the full path to your home dir, rather than ~/.

Configure the example/chef-solo/node.json.sudo to your desired configuration...

Run Chef Solo as sudo, so that stuff requiring root access can be done...
```
chef-solo -c /path/to/solo.rb -j ~/osx_blueprint/examples/chef-solo/node.json.sudo
```

Configure one of the example/chef-solo/node.json.* files to your desired configuration...
```
cp ~/osx_blueprint/examples/chef-solo/node.json.basic ~/osx_blueprint/examples/chef-solo/node.json.mine
vim ~/osx_blueprint/examples/chef-solo/node.json.mine
```

Run Chef Solo as the user you want to receive all of the goodness...
```
chef-solo -c /path/to/solo.rb -j ~/osx_blueprint/examples/chef-solo/node.json.mine
```