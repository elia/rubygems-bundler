# rubygems-bundler && Noexec

Let's stop using bundle exec, kthx.

## Installation

    gem install rubygems-bundler

Next run (once):

    gem regenerate_binstubs

And you're done!

## Configuration

Though you can let noexec do it's own thing and rely on looking up your binary via your Gemfile, 
you can also specify which binaries you want included or excluded. 
Create a .noexec.yaml file along side any Gemfiles you want to use. 
Then, to enable (or disable) the usage of your particular binary into your bundle, 
add an include or exclude section. For example:

### .noexec.yaml

    exclude: [rake]

Or, 

    include: [haml]

## Problems?

Things not going the way you'd like? Try your command again with 
NOEXEC_DEBUG=1 set and create a ticket. I'll fix it right away!

### IRC support:

[#rubygems-bundler on irc.freenode.net](http://webchat.freenode.net/?channels=#rubygems-bundler)


## How does this work (ruby_noexec_wrapper)

It modifies gem wrappers shebang to load `ruby_noexec_wrapper`.
Then, when you run gem binaries, it takes a look at your working directory,
and every directory above it until it can find a `Gemfile`. 
If the executable you're running is present in your Gemfile, 
it switches to using that `Gemfile` instead (via `Bundle.setup`).

Rubygems and Bundler integration, makes executable wrappers
generated by rubygems aware of bundler.

# Uninstallation

Before uninstalling change a line in `~/.gemrc` to:

    custom_shebang: $env ruby

and run

    rubygems-bundler --uninstall

this will set all gems to `/usr/bin/env ruby` which is one of the safest choices (especially when using rvm).

# Authors

 - Joshua Hull <joshbuddy@gmail.com>
 - Michal Papis <mpapis@gmail.com>

# Thanks

 - Carl Lerche     : help with the noexec code
 - Evan Phoenix    : support on rubygems internalls
 - Yehuda Katz     : the initial patch code
 - Loren Segal     : shebang customization idea and explanations
 - Wayne E. Seguin : support in writing good code
 - Andre Arko      : claryfications how rubygems/bundler works
