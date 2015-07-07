# Deploy mongodb replica set cluster with authentication / authorization

## Init Vagrant boxes and start VMs
4 boxes are declare in vagrant/Vagrantfile
- primary : primary mongo instance
- secondary1 : one of replicaset
- secondary2 : an other replicaset
- arbiter : the arbiter (if 2 instances of mongo die! For more info : http://docs.mongodb.org/manual/core/replica-set-arbiter/)

You can set IP of boxes if you want to change!

To start boxes :
- go to vagrant folder
    cd folder
- start all boxes
    vagrant up
Note : You certainely need to answer to network choice

## Typical usage with vagrant boxes

    1. Set ip in of the vagrant boxes in inventory/test.ini
    2. Run: ansible-playbook -i inventory/test.ini -k -u vagrant -s init.yml
    3. Run: ansible-playbook -i inventory/test.ini main.yml

Note: other options are detailled below to bootstrap this cluster on non vagrant boxes

## Inventory

The inventory/ENVIRONMENT.ini file defines the hosts (primary and secondaries) used for the replica set.  
On top the host decalration, some databasqe parameters are defined

eg:  
    
    [primary]
    192.168.1.200
    
    [secondary]
    192.168.1.201
    192.168.1.202
    
    [primary:vars]
    db_user_admin_password=ADMINPASSWORD
    db_root_admin_password=ROOTPASSWORD
    db_name=DBNAME
    db_user_name=DBUSERNAME
    db_user_password=DBUSERPASS

## Nodes initialisation

This first task initiate the server creating a user named mongors
- mongors user will be given sudo right with no password needed when running sudo commands
- current machine ssh key is copied over to the authorized_keys of the server that is beeing provisionned

Several possible cases  

### Usage of Vagrant VM 

    ansible-playbook -i inventory/ENVIRONMENT.ini -k -u vagrant -s init.yml

note: vagrant ssh password will be requested (sudo password not requested as vagrant user is authorized to sudo without any password by default)

### Usage of VPS with root access

    ansible-playbook -i inventory/ENVIRONMENT.ini -k -u root init.yml

note: root ssh password will be requested

### Usage of a user with sudo rights

    ansible-playbook -i inventory/ENVIRONMENT.ini -k -K -u USER -s init.yml

note: both user's ssh password + sudo password will be requested

## Replica set setup

Once the nodes are registered, the replica set can be created using the following command:  

    ansible-playbook -i inventory/ENVIRONMENT.ini main.yml

## License

MIT License - Copyright © 2015 GridPocket

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
