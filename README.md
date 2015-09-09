Vagrant file for a GitHub Pages-compatible Jekyll environment
====================

Simple Vagrant file to build a GitHub Pages-compatible Jekyll environment. Uses the "official" github-pages gem. Use this environment to build and test your GitHub Pages-based Jekyll sites without polluting your host box.

Initializing the vm
-------------------

First, make sure you've installed [Vagrant](http://docs.vagrantup.com/v2/getting-started/index.html) and [VirtualBox](https://www.virtualbox.org/).

Next, download the [Vagrantfile](https://raw.githubusercontent.com/mikkorepolainen/vagrant-github-pages/master/Vagrantfile) and place it somewhere convenient.
These instructions assume that you have placed it in the root of your github-pages repository.
(The directory where the Vagrantfile is located is synced with the /vagrant directory on the vm by default.)  


Now, `cd` into the directory and start up the Vagrant vm...
```
cd <your-repo-path>
vagrant up
```
When asked to `Enter passphrase for key xxx"`press enter.
The default password for a vagrant vm is `vagrant`.

Building the vm takes a while, so I recommend suspending the vm instead of destroying it when done with it:
```
vagrant suspend
```
or
```
vagrant destroy
```

Using Jekyll
------------

To use Jekyll on the vm, you can ssh into it.
You can either do all your Jekyll-related work there, or use your host system tools to edit files and use the vm only for building/serving the site.
```
vagrant ssh
cd /vagrant
ls
```

Build the site
```
jekyll build [--watch] [--force_polling]
```
You can browse the generated site on the host system in the _site directory.

Run the jekyll server
```
jekyll serve [--watch] [--force_polling] -P 8124
```
The Vagrant vm is configured to forward port 8124 by default.
Navigate to `localhost:8124` on your host box to view the site through the server.

Use the `--watch` option for either command to automatically build the site when files change in the source directory.
Try adding the `--force_polling` option if the --watch option has no effect by itself (I need to use this switch when using windows 7 as the host).

Note on SSH-forwarding
---------------------
The Vagrantfile enables ssh-forwarding so that you can use your host ssh keys to authenticate with github. Make sure to add you keys to the agent with ```ssh-add``` before running ```vagrant ssh``` if your keys aren't automatically added to the agent.
