.. The contents of this file may be included in multiple topics (using the includes directive).
.. The contents of this file should be modified in a way that preserves its ability to appear in multiple topics.


When provisioning for SSH delivery, the placement of the keys is crucial. If you should find yourself getting an error like this:    

.. code-block:: bash

   Error executing action 'converge' on resource 'machine[chef-server-test3]'
    
   RuntimeError
    
   Machine chef-server-test3 ( on ssh:/home/mabrahms/delivery-cluster/.chef/provisioning/ssh)
   did not become ready within 120 seconds

Follow these steps to resolve the issue:

#. Verify that your SSH keys are the problem by attempting to log into your chef server over SSH. 

   If you cannot do that, then your SSH keys need to be re-synced. 

   If you can, then your SSH configuration may be wrong. In some environments the problem may be that the |chef delivery| server’s SSH key has changed for the hostname or IP address your chef server uses. Local |vagrant| clusters see this when the |chef server| ``box`` file changes (or when switching between |vmware| and |virtualbox|) because the SSH key is generated during the OS install.

#. When the server SSH key ​is the problem, the fix is to delete the entry for that machine from ``$HOME/.ssh/known_hosts``.

#. To create an SSH key (without a passphrase):

   .. code-block:: bash

      $ ssh-keygen -t rsa -b 4096 -C "you@example.com"

   The output is similar to:

   .. code-block:: bash

      Generating public/private rsa key pair.
      Enter file in which to save the key (/Users/username/.ssh/id_rsa): 
      Enter passphrase (empty for no passphrase): 
      Enter same passphrase again: 
      Your identification has been saved in /Users/path/to/.ssh/id_rsa.
      Your public key has been saved in /Users/path/to/.ssh/id_rsa.pub.
      The key fingerprint is:
      ac:8a:57:90:58:c1:cd:34:32:18:9d:f3:79:60:f3:41 your_email@chef.io
      The key's randomart image is:
      +--[ RSA 4096]----+
      |  .==*o.E        |
      |  . *o*..        |
      |   o + = .       |
      |  . o o.o        |
      |     . ..S       |
      |      ..         |
      |     ..          |
      |   .*o*.         |
      |  ...            |
      +-----------------+

#. Run the following:

   .. code-block:: bash

      $ cat .ssh/id_rsa.pub

   The output is similar to:

   .. code-block:: bash

      ssh-rsa
      AAAAB3NzaC1yc2EAAAADAQABAAACAQDa8BR/9bj5lVUfQP9Rsqon5qJMkiVm+JAtGi
      wnhxqgyRhkYLIzm6+gcifDgMOMuwZA88Ib5WNRhxjlmTseapower4rH/jAAczdp1h1
      7xLEEbUfQfkcqiy/Drp3k12345678ad234fgvdsasdfasdfR9ddNIeNvQ7OIpOCfLE
      PCyFz3aRRuhpM/5cySFT7bl1O44bNgfiuqRzcXFscZb03WPlhaPwCvL2uxaRzdrAGQ
      mE5jzCo6nORvKoGdVDa2++def33f3xPZCo3oJ08Q9XJ2CnfJlmyNe1hwI2NOQ3yRbc
      nfSMona7ccSyHRWGs5bS//u6P0NK5AqH5jK8pg3XwtHZqLwUVy1wX0WnnJWg9IWXf3
      2g3P4O4NJGVUeX33Czv32GK8YphuEweqFu/Ej7kQp1ppIxkEtrpBfMi3na0QqZlk6w
      wghZLa++DUfWOhGsuuBgnsocAR5rLGy+gkypdie1Ydoe8qjLVZR/jKybQfQjuZOS30
      fZnwJhl2ZaeraPfkEXlVhK02/8PIALGfeXdt9KvQN0p5c6lRoDxqBqslM+1KbKKcGd
      lSGEsAIP9OOWBECRxlOwqlqGHtrgWKOr376dntMIy2+fFD/74tJMjRwbRzm8IGWmj6
      OcF6EvTYYO4RmISD8G+6dm1m4MlxLS53aZQWgYWvRdfNB1DA
      Zo3h9Q== your_email@chef.io

#. Add the SSH public key to the user account.