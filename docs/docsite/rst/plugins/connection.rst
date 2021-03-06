.. contents:: Topics


Connection Plugins
------------------

These plugins are in charge of enabling Ansible to connect to the target hosts so it can execute tasks on them.
Ansible ships we many connection plugins but only one can be used per host at a time.

By default, the configuration uses a 'smart' value, which means Ansible will decide to use the 'ssh' or 'paramiko' (python version of ssh client)
depending on what it detects on your system capabilities, it normally chooses 'ssh' if OpenSSH supports ControlPersist.

The basics of these connection types are covered in the :doc:`../intro_getting_started` section.

.. contents:: Topics

.. _ssh_plugins:

The ssh Plugins
++++++++++++++++

Since ssh is the default protocol used in system administration it is also the most used and prevalent in Ansible,
so much so that ssh options are included in the command line tools unlike other plugins, see :doc:`../ansible-playbook` for more details.


.. _using_connection_plugins:

Using Connection Plugins
++++++++++++++++++++++++

The transport can be changed via :doc:`configuration <../config>`, in the command line (``-c``, ``--connection``), as a keyword (:ref:`connection`)
in your play or by setting the a connection variable (:ref:`ansible_connection`), most often, in your inventory.
For example, for windows machines you might want o use the :doc:`winrm <connection/winrm>` plugin instead.

Most connection plugins can operate with a minimum configuration, by defaul they use the :ref:`inventory_hostname` and defaults to find the target host.
Each plugin documents it's configuration options and how to set, the following are 'connection variables' common to most:

:ref:ansible_host
    The name of the host to connect to, if different from the :ref:`inventory_hostname`.
:ref:ansible_port
    The ssh port number, for :doc:`ssh <connection/ssh>` and :doc:`paramiko <connection/paramiko>` it defaults to 22.
:ref:ansible_user
    The default user name to log in as, most plugins defaul to the 'current user running Ansible'

Each plugin might also have a specific version that overrides the general one. i.e :ref:`ansible_ssh_host` for the :doc:`ssh <connection/ssh>` plugin.

Enabling Connection Plugins
+++++++++++++++++++++++++++

Should you want to extend Ansible to support other transports (SNMP, Message bus, etc) it's as simple as dropping a custom plugin
into the ``connection_plugins`` directory.

Plugin List
+++++++++++

You can use ``ansible-doc -t connection -l`` to see the list of available plugins,
use ``ansible-doc -t connection <plugin name>`` to examine detailed documentation and examples.


.. toctree:: :maxdepth: 1
    :glob:

    connection/*


.. seealso::

   :doc:`../playbooks`
       An introduction to playbooks
   :doc:`callback`
       Ansible callback plugins
   :doc:`../playbooks_filters`
       Jinja2 filter plugins
   :doc:`../playbooks_tests`
       Jinja2 test plugins
   :doc:`../playbooks_lookups`
       Jinja2 lookup plugins
   :doc:`vars`
       Ansible vars plugins
   `User Mailing List <http://groups.google.com/group/ansible-devel>`_
       Have a question?  Stop by the google group!
   `irc.freenode.net <http://irc.freenode.net>`_
       #ansible IRC chat channel
