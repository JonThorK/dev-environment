# My vagrant dev-environment

## About

This repo contains my config files for Vagrant that I use as a development environment.
It uses [Vagrant][] to manage the VMs and [Chef][] for handling provisioning.

It configures:
* my [dotfiles][]
* It installs git, python, apache2, nodejs, postgresql

It's currently configured to use the Ubuntu Precise (32bit) Vagrant base box.

Used [this][post] blog post as a refrence for setting up the dotfiles.

## Usage

Download cookbooks used by chef solo
'''bash
librarian-chef install --clean
'''
Start vagrant
'''bash
vagrant up
'''

## Uses
* [Vagrant]
* [Chef]
* [Librarian-chef]

[Vagrant]: http://vagrantup.com/
[Chef]: http://opscode.com/
[dotfiles]: http://github.com/JonThorK/dotfiles
[post]: http://nickcharlton.net/posts/test-environments-with-vagrant-and-chef.html
[Librarian-chef]: http://github.com/applicationsonline/librarian-chef