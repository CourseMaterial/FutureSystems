Cloudmesh Preparation
----------------------

Cloudmesh needs to be configured on your desired machine to use Cloudmesh
interactive shell commands. With a proper installation and configuration, you
are ready to create a virtual machine (vm) or a virtual cluster on
FutureSystems.

.. note:: Don't have an FutureSystems account? Please `register <account.html>`_

Active cloud
~~~~~~~~~~~~
Before starting any command, please make sure you have an active cloud (IaaS).
For example, you can simple choose *india* as your active cloud host:

.. code:: python

    cm "cloud on india"

Activation however does not select the cloud as the default cloud to
start virtual machines. This can be achieved by the ``select`` command

.. code:: python

    cm "cloud select india"

.. note: this is a bit unintuitive and shold probably be done with

Also, new command is available:

.. code:: python

    cm "cloud default india"

Default keypair
~~~~~~~~~~~~~~~

To gain access to the virtual machines, you need to have a key
registered with the cloud. If you don't have a default keypair, you need
to set or need to specify which keypair you are going use for the vm.

.. code:: python

    cm "key default test-key"

VM Name
~~~~~~~

You can also define the name of VMs which contains a prefix and an index
with the ``label`` command. However, the name of the vms must be unique.
By default your username and a number will be used that will be
automatically increased. Thus we recommend that you avoid using this
command.

.. code:: python

    cm "label --prefix=test --id=1"

Default Image
~~~~~~~~~~~~~

You can choose a default image to create a virtual machine. In this
example, we use ubuntu-14.04 image as a default.

.. code:: python

    cm "default image --name=futuregrid/ubuntu-14.04"

Default Flavor
~~~~~~~~~~~~~~

You can chose a default flavor. However, make sure that the falvor
actially works with the specified image. Some images require a minimal
flavor.

.. code:: python

    cm "default flavor --name=m1.small"

Exercise
--------

* Can you create a virtual machine?
* Can you see a list of running virtual machine?
