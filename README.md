hxarc-provision
===============

ansible playbooks for [hxarc webapp](https://github.com/nmaekawa/hxarc)

# disclaimer
for demo purposes only! provided to show how to setup a hxarc vagrant
installation and support to this repo is OUT-OF-SCOPE at this time.


# for local vagrant hxarc

you'll need:

- vagrant
    - install dns plugin landrush: `$> vagrant plugin install landrush`
- virtualbox
- ansible 2.4.0

## start vagrant instances

the Vagrantfile provided in this repo will start 1 ubuntu xenial instance:

    - hxarc.vm

    $> git clone https://github.com/nmaekawa/hxarc-provision.git
    $> cd hxarc-provision
    $> vagrant up

this will only start the box, so it doesn't have anything installed yet.
you can change the tld and assigned local ip in the `Vagrantfile`.

login into the box like below, so the ssh host key
fingerprint is stored in `~/.ssh/known_hosts`. This helps with ansible-playbook
when installing hxarc:

    $> ssh vagrant@hxarc.vm -i ~/.vagrant.d/insecure_private_key
    ...


## provision the instance

run:

    # install external ansible roles
    $> ansible-galaxy -r roles/requirements.yml
    
    # set vagrant insecure key in your env
    $> ssh-add ~/.vagrant.d/insecure_private_key
    $> ansible-playbook -i hosts/vagrant.ini hxarc_play.yml
    
    # or specify it in the command line
    $> ansible-playbook -i hosts/vagrant.ini --private-key ~/.vagrant.d/insecure_private_key hxarc_play.ym


the default configuration:

- find hxarc and hxpy-utils in /opt/hxarc and /opt/hxpy: virtualenv,
  logs, repo clone, config/dotenv files
- hxarc flask app will run with gunicorn; check
  `/opt/hxarg/venv/bin/gunicorn_start`
- gunicorn is configured to talk to nginx via a socket at
  `/opt/hxarc/venv/run/gunicorn.sock`
- default user is 'user:password'
- nginx for dev env uses HTTP

if all goes well, you should be able to check it out at
http://hxarc.vm


