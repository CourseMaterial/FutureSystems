Deploying Virtual Cluster with Cloudmesh ``cm``
===============================================

To support the creation of a virtual compute cluster on Cloudmesh, the command
``cluster`` can be used to start, configure, manage or update a number of
virtual machines.

.. note:: Don't have Cloudmesh? see the `preparation <cm_preparation.html>`_

Create Virtual Cluster with 3 virtual machines
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You can create a virtual cluster with a group name *test* and 3 virtual instances.

.. code:: python

    cm "cluster create virtual_cluster --count=3 --ln=ubuntu"

You may also provide a cloud name, flavor or image as parameter in the
command if you do not want to use the defaults. For example you can use
the following do do so:

.. code:: python

    cm "cluster create virtual_cluster_ext --count=3 --ln=ubuntu --cloud=india --flavor=m1.small --image=futuresystems/ubuntu-14.04"

You can display the status of vms for the cluster with the ``vm list``
command:

.. code:: python

    cm "vm list --refresh --group=virtual_cluster"

Exercise
---------

- Try to access a master node of your cluster.
- Create a Virtual Cluster with 5 VMs

Cloudmesh ``cluster`` command
-----------------------------

To create, list, or remove clusters, try to use ``cm cluster`` command.

.. tip:: latest repository is required (dev1.3). Please `download latest cloudmesh <cm_download.html>`_

Create Cluster
~~~~~~~~~~~~~~~~~

Cloudmesh provides a simple command to create a virtual cluster.
``cluster create`` can be executed along with the following options:

| ``--count``
|  specify amount of VMs in the cluster

| ``--cloud``
|  specify a cloud name, e.g. india

| ``--flavor``
|  specify a flavor name among m1.tiny, m1.small, m1.medium, m1.large

| ``--ln``
|  login name for VMs, e.g. ubuntu

| ``--image``
|  specify an image name.  ``list image`` command allows you to find registered images.

List Cluster
~~~~~~~~~~~~

``cluster list [name]`` shows running clusters with a number of nodes.

Remove Cluster
~~~~~~~~~~~~~~

``cluster remove [name]`` automatically terminates all nodes of the cluster.

FAQ
----

- Q. How do I delete a Virtual Cluster?
- A. ``cluster remove [name]``

- Q. I cannot find ``cluster`` command on my cloudmesh.
  A. You need to download latest cloudmesh on Github. Please see `the download page <cm_download.html>`_

Other questions?
----------------

- Forum via Git Issues: `Git Issues <>`_
- Email: `Contact Us <contact.html>`_

Next Step
---------

In the next page, we deploy a Hadoop cluster on FutureSystems using Cloudmesh.

.. toctree::
   :maxdepth: 1

   hadoop_cluster
