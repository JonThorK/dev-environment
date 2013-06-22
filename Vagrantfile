# encoding: utf-8

# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "precise32"
  config.vm.box_url = "http://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-i386-vagrant-disk1.box"
  config.ssh.forward_agent = true
  config.vm.network :forwarded_port, guest: 80, host: 4567
  config.vm.network :private_network, ip: "192.168.2.1"
  config.vm.provision "chef_solo" do |chef|
    chef.cookbooks_path = ["cookbooks", "myscookbooks"]
    chef.add_recipe "apt"
    chef.add_recipe "nodejs"
    chef.add_recipe "build-essential"
    chef.add_recipe "python"
    chef.add_recipe "postgresql::server"
    chef.add_recipe "git"
    chef.add_recipe "apache2"
    chef.json = {
      :postgresql => {
        :config   => {
          :listen_addresses => "*",
          :port             => "5432"
        },
        :pg_hba   => [
          {
            :type   => "local",
            :db     => "postgres",
            :user   => "postgres",
            :addr   => nil,
            :method => "trust"
          },
          {
            :type   => "host",
            :db     => "all",
            :user   => "all",
            :addr   => "0.0.0.0/0",
            :method => "md5"
          },
          {
            :type   => "host",
            :db     => "all",
            :user   => "all",
            :addr   => "::1/0",
            :method => "md5"
          }
        ],
        :password => {
          :postgres => "password"
        }
      },
      :git        => {
        :prefix => "/usr/local"
      },
      :apache     => {
        :default_site_enabled => "true",
        :dir                  => "/etc/apache2",
        :log_dir              => "/var/log/apache2",
        :error_log            => "error.log",
        :user                 => "www-data",
        :group                => "www-data",
        :binary               => "/usr/sbin/apache2",
        :cache_dir            => "/var/cache/apache2",
        :pid_file             => "/var/run/apache2.pid",
        :lib_dir              => "/usr/lib/apache2",
        :listen_ports         => [
          "80"
        ],
        :contact              => "jonthork@gmail.com",
        :timeout              => "300",
        :keepalive            => "On",
        :keepaliverequests    => "100",
        :keepalivetimeout     => "5"
      },
      :dotfiles => {
        "user" => "vagrant",
        "group" => "vagrant",
        "public_key" => IO.read(File.expand_path("~/.ssh/id_rsa.pub")),
        "private_key" => IO.read(File.expand_path("~/.ssh/id_rsa"))
      }
    }
  end
  config.vm.provision :shell, :path => "bootstrap.sh"
end
