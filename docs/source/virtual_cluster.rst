Deploying Virtual Cluster with Cloudmesh ``cm``
===============================================

To support the creation of a virtual compute cluster on cloudmesh, the command
``cluster`` can be used to start, configure, manage or update a number of
virtual machines.

.. note:: Don't have Cloudmesh? see the `preparation <cm-preparation.html>`_

Create Virtual Cluster
----------------------

Cloudmesh provides a simple command to create a virtual cluster.
``cluster create`` can be executed along with the following options:

| ``--count``
|  specify amount of VMs in the cluster

| ``--group``
|  specify a group name of the cluster, make sure it's UNIQUE

| ``--ln``
|  login name for VMs, e.g. ubuntu

Create 3 virtual machines
~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: python

    Let us create a cluster with the group name test that contains 3 virtual machines.

.. code:: python

    cm "cluster create --count=3 --group=test --ln=ubuntu"

You may also provide a cloud name, flavor or image as parameter in the
command if you do not want to use the defaults. For example you can use
the following do do so:

.. code:: python

    cm "cluster create --count=3 --group=test0 --ln=ubuntu --cloud=india --flavor=m1.small --image=futuregrid/ubuntu-14.04"

You can display the status of vms for the cluster with the ``vm list``
command:

.. code:: python

    cm "vm list --refresh --group=test"

Exercise
---------

- Try to access a master node of your cluster.
- Create a Virtual Cluster with 5 VMs

FAQ
----

- Q. How do I delete a Virtual Cluster?
- A. ``cluster delete --group=[name]``

Other questions?
----------------

- Forum via Git Issues: `Git Issues <>`_
- Email: `Contact Us <contact.html>`_
