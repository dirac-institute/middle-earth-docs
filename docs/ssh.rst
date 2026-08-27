##############
Setting up SSH
##############

An user account is required to gain access to DiRAC infrastructure.
See :ref:`user_account_creation_ref` for details.

There are two aspects to setting up SSH:
    - creating and sharing SSH keys
    - configuring the SSH client

Creating an SSH key consist of creating two related, specially encrypted, strings.
Sharing the SSH key means giving someone, or something, one of those two strings.
SSH keys can be used to, for example, login onto systems in a more secure way and
without having to constantly type or copy/paste a password at every login.

To make this experience even less miserable you want to configure your SSH agent
with aliases, shorthands and other configuration options that allow you to further
customize your experience with SSH and make your life easier.

.. _using_ssh:

-------------
Using SSH/SCP
-------------

The basic usage pattern is:

.. code-block:: bash

    ~:$ ssh user@destination

where the destination is usually an URL such as ``epyc.astro.washington.edu``,
``arnor.astro.washington.edu`` or ``gondor.astro.washington.edu``, but it can be an
IP address, or an alias etc.

To copy a file from a remote location to a local destination (or vice-versa) you
can use ``scp`` as:

.. code-block:: bash

    ~:$ scp user@destination:/location1/file destination/

or

.. code-block:: bash

    ~:$ scp ~/location/file user@destination:/some/path/

If you have more than a few files to move then it's better to look into ``rsync``
which is out of scope for this document. As you can imagine this can quickly
become really rather long and burdensome:

.. code-block:: bash

    scp -r iluvatar@arda.astro.washington.edu:~/ainulindale/ainur .

and then you need to input a password for each file/directory you download in this way.
Creating and configuring SSH agent can help you shorten this into:

.. code-block:: bash

    scp -r arda:~/ainulindale/ainur .

and makes your life easier in the future.

.. _ssh_config:

---------------
Configuring SSH
---------------

In this section we will just assume that you are using OpenSSH agent. This is what
most modern OS systems ship with and it's probably safe to assume you are using it.
If you are working from Putty, Keepass or Secretive - refer to their documentation
to see how to configure them.

The canonical position for all-things SSH related is ``~/.ssh``; the hidden ssh
directory usually found in your home directory. **It is normal if sometimes
this directory doesn't exist.** Simply create one if it doesn't exist:

.. code-block:: bash

    ~:$ mkdir -p ~/.ssh

That directory is usually the place where you want to keep all of your SSH keys
and usually a few additional files exist in the directory:

- ``config``
- ``known_hosts``
- ``authorized_keys``

The files that are interesting to us are the ``config`` and ``authorized_keys``.
**It is normal if sometimes these files do not exist.** If ``config`` file does
not exist, simply create one using your favorite text editor (vi, vim, emacs,
nano, or run ``touch ~/.ssh/config`` and then edit the file). An example of a
complete config file is:

.. code-block:: bash

    Host epyc
        User iluvatar
        HostName epyc.astro.washington.edu
        IdentityFile ~/.ssh/arda_login

    Host arnor
        User iluvatar
        HostName arnor.astro.washington.edu
        IdentityFile ~/.ssh/arda_login

    Host gondor
        User iluvatar
        HostName gondor.astro.washington.edu
        IdentityFile ~/.ssh/arda_login

The name that follows the ``Host`` line becomes an alias. When your agent sees
an alias, it expands fields such as ``User`` and ``HostName`` to save you the
effort of having to type it yourself.

The ``IdentityFile`` field in the ``config`` tells SSH agent which SSH key it
should use to log into/gain access to that system. In this case it points to a
file in the same directory called ``arda_login``. We will create this file in
the following section (:ref:`creating_ssh`).

.. _creating_ssh:

-----------------
Creating SSH Keys
-----------------

SSH keys consist of two parts: the private key and the public key.
These keys will present themselves as two separate files:

- the public key will have an extension ``.pub``
- and the private one will have no extension

There are 2 steps to using SSH keys:

- creating the keys and
- sharing them.

**You only ever want to share the public key**.
Both keys are created at the same time via ``ssh-keygen`` command:

.. code-block:: bash

    ~:$ cd ~/.ssh
    ~/.ssh:$ ssh-keygen

    Generating public/private ed25519 key pair.
    Enter file in which to save the key (/home/iluvatar/.ssh/id_ed25519): arda_login
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in arda_login
    Your public key has been saved in arda_login.pub
    The key fingerprint is:
    SHA256:0MK8PbfjflN08NhlWFjWfnif8+f9sI9wNQ9BIHpIkjg iluvatar@arda
    The keys randomart image is:
    +--[ED25519 256]--+
    |     .... . ...==|
    |    Eo.+ o . .+.+|
    |     .= + .   .O.|
    |       = .    +.B|
    |      . S .  ..+=|
    |         o .  .=+|
    |          o ..o +|
    |         . .oo ++|
    |         .o. .ooB|
    +----[SHA256]-----+

The process is interactive and you will be asked several questions along the way:

- Firstly, it will ask you for the name of the key.
- Secondly, it will query you for a passphrase.

The key name is used as the filename, so naming it after the destination helps
you remember their purpose when you eventually revisit the directory to tidy it up.

If you chose no passphrase, by leaving the passphrase section empty and pressing
enter to continue forward, then the SSH key will be saved to the two files un-encrypted.

If you chose to add a passphrase, then the *key files themselves* will be encrypted.
Thus, next time your system (f.e. linux, mac) needs to read the file it will
prompt you for a password to first un-encrypt the file so that it may then read
and use the SSH key itself. See :ref:`ssh_passphrases` on how to deal with some
potentially annoying side-effects of using passphrases.

----------------
Sharing SSH keys
----------------

Now that we have crated the SSH keys we have to let the destination also know
about them. This consists of sharing the public portion of the key. The public
key generally looks something like:

.. code-block:: bash

    ssh-rsa AAAABAAAAAAKHADGBSIDAYSDBAIS…..ASDHASIDH= iluvatar@arda

The key can be uploaded onto the destination by using ``ssh-copy-id`` command:

.. code-block:: bash

     ~/.ssh:$ ssh-copy-id -i arda_login  iluvatar@gondor.astro.washington.edu

Sometimes the ``ssh-copy-id`` is not available on your system (old macs, windows
etc.). The bullet-proof way is to just log into the destination and then copy
the key into the ``authorized_keys`` at the destination.

.. code-block:: bash

    ~:$ ssh iluvatar@arnor.washington.astro.edu
    Enter password: ...

    iluvatar@arnor $:> cd ~/.ssh/
    kbmod@arnor $:> nano authorized_keys
    [paste and save with ctrl+x]
    [disconnect with ctrl+d]

This is the other the other interesting file next to ``config`` we mentioned
earlier and it lets the destination system encrypt and un-encrypt communication
between your laptop and the destination.

----------------
File permissions
----------------

Obviously, the SSH key should be a well guarded secret. For this reason your system
(mac, linux...) will complain if the files are not restricted to be only readable
by certain people. The following set of permissions is required, or attempting to use
ssh command will result in an error:

.. code-block:: bash

    # Only owner can read/write/execute in this directory
    chmod 700 ~/.ssh

    # Only owner can read and write (private key)
    chmod 600 ~/.ssh/arda_login

    # Owner can read and write, others can only read (public key)
    chmod 644 ~/.ssh/arda_login.pub

    # Only owner can read/write (it is ok if this file does not exist on your laptop/PC/notebook)
    chmod 600 ~/.ssh/authorized_keys

    # Only owner can read/write
    chmod 600 ~/.ssh/config


-------
Summary
-------

1. Create ``.ssh`` directory and ``config`` file if they don't exist:

.. code-block:: bash

                mkdir -p ~/.ssh
                touch ~/.ssh/config

2. Create your new SSH key (f.e. with name ``arda_login`` and without a passphrase):

.. code-block:: bash

                cd ~/.ssh
                ssh-keygen

3. Add aliases to ``config`` file pointing to the newly generated SSH key

.. code-block:: bash

                Host epyc
                  User iluvatar
                  HostName epyc.astro.washington.edu
                  IdentityFile ~/.ssh/arda_login

                Host arnor
                  User iluvatar
                  HostName arnor.astro.washington.edu
                  IdentityFile ~/.ssh/arda_login

                Host gondor
                  User iluvatar
                  HostName gondor.astro.washington.edu
                  IdentityFile ~/.ssh/arda_login

4. Set up correct file permissions on your local machine

.. code-block:: bash

                chmod 700 ~/.ssh
                chmod 600 ~/.ssh/arda_login
                chmod 644 ~/.ssh/arda_login.pub
                chmod 600 ~/.ssh/config

5. Copy the contents of the public key (``arda_login.pub`` in this example) into
   the ``authorized_keys`` at the destination:

.. code-block:: bash

                ssh-copy-id -i arda_login  arnor


If step 5 fails for you for whatever reason. You must log into the destination
system (``arnor`` in this example), create the ``.ssh`` directory and the
``authorized_keys`` file, manually copy the contents of the public key
``arda_login.pub`` file into it, and then finally set the correct permissions on
these files:

.. code-block:: bash

                ssh iluvatar@arnor.astro.washington.edu
                <give correct password to the prompt>
                mkdir -p ~/.ssh
                touch ~/.ssh/authorized_keys
                <copy contents of the arda_login.pub> into authorized_keys using nano/vi/vim/emacs>
                chmod 700 ~/.ssh
                chmod 600 ~/.ssh/authorized_keys

6. Validate that the process was successful by logging in as ``ssh arnor``

----
Tips
----

.. _ssh_passphrases:

***************
SSH Passphrases
***************

**Using passphrases is the safer and recommended option**. But it can be annoying
because it will query you for a passphrase *every time* it needs to read
the key. So, for example, if its an SSH key to your Git repo then it will prompt
you at every ``git clone``, ``git push`` etc. The "fix" for this is to add the key
to your **authentication agent**. Again, we'll just assume we're all using OpenSSH
agent. With OpenSSH the key can be added *to the session* with the command:

.. code-block:: bash

    ~/.ssh:$ ssh-add ~/.ssh/arda_login

and the passphrase will not have to be retyped again *within that session*. If you
would like this to happen every time you use a key automatically then you need to
configure your authentication agent. For example, for OpenSSH again, add the
following to the top of the ``~/.ssh/config`` file:

.. code-block:: bash

    Host *
        AddKeysToAgent yes

There are several config values for this field, please see ``ssh man page <https://man.openbsd.org/ssh_config.5#AddKeysToAgent>``
for details of the other options (``yes``, ``ask``, ``confirm``, and ``no``). If you're
confused by this section and are not sure what ``~/.ssh/config`` is or looks like
see the previous (:ref:`ssh_config`) section.


**********************
Config string-matching
**********************

The SSH config allows for pattern matching. This can yield in some clever ways
to configure your SSH connections. Take the following config file as an example:

.. code-block:: bash

    Host *
        # use compression
        Compression yes
        # really really compress it
        CompressionLevel 9

    Host gondolin-gate*
        User maeglin
        HostName gondolin.astro.washington.edu
        IdentityFile ~/.ssh/arda_login

    Host gondolin-gate01
        HostName wood-gate.tumladen.beleriand.edu
    Host gondolin-gate02
        HostName stone-gate.tumladen.beleriand.edu
    Host gondolin-gate03
        HostName bronze-gate.tumladen.beleriand.edu
    Host gondolin-gate04
        HostName writhen-iron-gate.tumladen.beleriand.edu
    Host gondolin-gate05
        HostName silver-gate.tumladen.beleriand.edu
    Host gondolin-gate06
        HostName gold-gate.tumladen.beleriand.edu
    Host gondolin-gate07
        HostName steel-gate.tumladen.beleriand.edu
        Compression no

In this example, first, We use an empty ``*`` alias to match "on every connection".
In other words we have turned on data compression to max on every single SSH
connection we have defined, unless those connections explicitly override the
configuration value (f.e. like gondolin-gate07 does).

Then we have the traitorous user ``maeglin``, who has stolen the ``arda_login``
key  and simultaneously configured security permissions on all 7 gates of
Gondolin, allowing Morgoth's forces to sack and burn the city down and marking
the beginning of the end of the Elves in Beleriand. Your mileage may vary.

Finally, note that the string-matching works against the other defined aliases,
not against the ``HostName`` values.
