Monkeysphere
============

This role installs and configures monkeysphere.
With Monkeysphere, you use the PGP Public key infrastructure to distribute your public ssh keys and to trust servers, without previous connections just because the servers key has been signed by somebody you trust.
For more information, see [Monkeysphere](http://web.monkeysphere.info) for more information.

**Note:** If you plan to publish your ssh server key to the PGP Public Key Infrastructure, Ansible won't run fully automatic any longer. At one moment, Ansible will pause and ask you to sign the newly uploaded key with your key. This only happens once.

**Note:** After this, you can only log in via ssh keys distributed by monkeysphere.

**Note:** As you are messing with authorization, there is a slight chance that something goes wrong and you won't be able to access the server via ssh any longer. Be prepared for that case.

This role has only been testet with Ubuntu 13.10. and 12.04. For older Releases and Debian, I have checked, that the packages exist. According the the Monkeysphere website, monkeysphere packages exist for 

- FreeBSD
- Slackware
- Redhat Fedora
- ArchLinux
- Gentoo

It might be, that this role works on these distributions without changes.

Requirements
------------

You should be a bit familiar with Websphere. Everybody who wants to access the server has to do some preparations on their own computer. What needs to be done is well explained at the [Monkeysphere](http://web.monkeysphere.info) Site. Your users should have created a file 

    ~/.monkeysphere/authorized_user_ids 
    
with their user ids before this role is run.

Role Variables
--------------

You must declare your certifiers fingerprints, else no key will be trusted. The variable name is named `monkeysphere_certifiers_fingerprints`. See the [Monkeysphere](http://web.monkeysphere.info) on Details about the fingerprint. It is not the short gpg id!
By default, this role will _not_ upload you servers ssh key to a Keyserver. If you want it, define `monkeysphere_publish_hostkey` as True:

    - {role: do3cc.monkeysphere, monkeysphere_certifiers_fingerprints: ["47CE085311CEC1E1EE4FA99DDA9ED7C1671A13DE"], monkeysphere_publish_hostkey: True}

Dependencies
------------

There are no dependencies.

License
-------

BSD
