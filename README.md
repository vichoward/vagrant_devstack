## DevStack with Vagrant!

### Step 1: Install Vagrant
Vagrant uses VirtualBox to handle creation of the actual virtual machines. Head over to `https://www.virtualbox.org/wiki/Downloads` to find the appropriate installer for your system.

If you're running Mac OS X, you'll also need to install Xcode. If you're running Lion, the simplest method is to use the App Store. You can also grab the installer from `http://developer.apple.com/xcode/`.

Once you've got VirtualBox and Xcode installed, you're ready to install Vagrant. The simplest way to get Vagrant is to use ruby's gem installer :

    gem update --system
    gem install vagrant

NOTE: This project is intended to work with Vagrant v0.9.X

### Step 2: Check Out the Code
Now would be a good time to actually check out the project :

    git clone http://github.com/bcwaldon/vagrant_devstack

The project also requires a local copy of the `devstack_cookbooks` project. The location to put those is directly inside the vagrant\_devstack directory :

    cd vagrant_devstack
    git clone http://github.com/bcwaldon/devstack_cookbooks

### Step 3: Set up a Box
This project depends on having an Ubuntu 11.10 image (aka 'box') available in VirtualBox with the Guest Additions already installed. Run the following command to download a safe base box and make it availble under the name 'oneiric' :

    vagrant box add oneiric http://images.ansolabs.com/vagrant/oneiric64.box

### Step 4: Configuration
You can set up a local config file to override the default settings used with the project. See a sample config at `etc/vagrant.yaml.sample`. Place your own copy at `etc/vagrant.yaml`, or set a custom location in the environment variable `VD_CONF`.

If you decide to place the cookbooks you checked out in setp 2 in a non-default location, you must set the `devstack_cookbooks_dir` attribute to point to the proper directory.

Additionally, if the box you with to use has a different name than 'oneiric', make sure you set the `box_name` attribute in your config file.

DevStack also allows you to define a `localrc` file. This file will be injected into your environmant and sourced before the environment is built. You can use this to override settings such as `MYSQL_PASSWORD` or `NOVA_REPO`. See http://devstack.org for more information. You can create an `etc/localrc` file, or point to a custom loation with `VD_LOCALRC`.

### Step 5: Execution
At this point you can run `vagrant up` and ssh into your DevStack environment!
