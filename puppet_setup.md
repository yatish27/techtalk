# Puppet Setup

## Puppet Master
- Update the packages on the Linux server

    ```
    sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y dist-upgrade && sudo apt-get -y autoremove && sudo reboot
    ```

- Download the .deb package from the official repository

    ```
    sudo wget http://apt.puppetlabs.com/puppetlabs-release-precise.deb
    sudo dpkg -i puppetlabs-release-precise.deb
    sudo apt-get update && sudo apt-get -y install puppetmaster
    ```

-  Setting up a default manifest file
    
    ```
    sudo touch /etc/puppet/manifests/site.pp
    ```

- Puppet's main configuration is found in `/etc/puppet/puppet.conf`. It has three section [main], [agent], and [master]

- Add `server=puppet.devops.com` in `/etc/puppet/puppet.conf` file

- Add DNS entry or manually add the hosts in `etc/hosts`

    ```
     Your system has configured 'manage_etc_hosts' as True.
    # As a result, if you wish for changes to this file to persist
    # then you will need to either
    # a.) make changes to the master file in /etc/cloud/templates/hosts.tmpl
    # b.) change or remove the value of 'manage_etc_hosts' in
    #     /etc/cloud/cloud.cfg or cloud-config from user-data
    127.0.1.1 puppet puppet
    127.0.0.1 localhost
    104.131.125.90 puppet.devops.com puppet
    104.236.86.45  puppet-client.devops.com puppet-client
    ```

## Puppet Client
- Install puppet agent on node/client

    ```
    sudo wget http://apt.puppetlabs.com/puppetlabs-release-precise.deb
    sudo dpkg -i puppetlabs-release-precise.deb
    sudo apt-get update && sudo apt-get -y install puppet
    ```

- Add server hostname in conf of puppet

    ```
    //client puppet.conf
    ```

- Add host details in etc/hosts

- Test communication between client and server
    ```
    puppet agent --server puppet --waitforcert 60 --test
    ```
    While on the master you need to sign the certificate
    ```
    puppet cert --list
    puppet cert --sign puppet-client
    ```

- Now, we need to configure the Puppet client to start automatically, with the following command:
    ```
    vim /etc/default/puppet
    START=yes  
    ```

## Using Puppet
