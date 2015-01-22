Deploying Hadoop Cluster with Cloudmesh ``launcher``
====================================================

To support a compute cluster (e.g. Hadoop or Slurm) with applications,
Cloudmesh provides a new command ``launcher`` to start, configure, manage or
update compute nodes (VMs) with selected applications. ``launcher`` command
applies default settings to configure clusters with applications so users can
avoid hassles of building clusters.

Tutorial: Deploying Hadoop Cluster with ``cm launcher``
------------------------------------------------------

.. tip:: approximate time 15-20 minutes

In this tutorial, we are going to deploy a Hadoop cluster using Cloudmesh
``launcher`` command.

Start Cluster
~~~~~~~~~~~~~~

``launcher start`` command deploys a cluster with a selected application.

::

        cm launcher start hadoop

Check Status of Cluster
~~~~~~~~~~~~~~~~~~~~~~~

Initializing a cluster requires some time for installing packages, configuring networks, etc.
While it is initiated, you can check the status of your cluster deployment.

::

        cm launcher list

* CREATE_IN_PROGRESS: cluster is not available because creating the cluster is in progress.
* CREATE_COMPLETE: cluster has been created and it is ready to use.

Login Cluster
~~~~~~~~~~~~~~~~

We use ``cm vm login`` command to ssh to one of the nodes in the cluster.
Issue ``vm list`` first to see the list of virtual instances.

::

        cm vm list

::

        cm vm login [node name]

Terminate Cluster
~~~~~~~~~~~~~~~~~

Once you completed your task on the cluster, you can terminate the cluster with
``cm launcher stop [name]`` command.

::

        cm launcher stop [name]


* DELETE_IN_PROGRESS: shutting down instances is in progress.
* DELETE_COMPLETE: the lease of resources is ended, all resources are returned.

Next Step
---------

In the next page, we deploy a Sharded MongoDB cluster on FutureSystems using Cloudmesh.

.. toctree::
   :maxdepth: 1

   mongodb_cluster

Using Cluster on Cloud IaaS Platform
------------------------------------

Many cloud platforms such as OpenStack, Eucalyptus, AWS, etc. support a
compute cluster on their virtualized environments with orchestration
tools like Docker, Puppet or Chef. It typically, however, requires
additional tasks to configure networks and support large number of
clusters manually. Cloudmesh offers ``launcher`` command with OpenStack
Heat and Chef recipes to provide automated and scalable clusters.

Provisioning Virtual Machines for Cluster
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To create a virtual machine(s) for a cluster, we use OpenStack Heat.
Heat is the OpenStack Orchestration tool which creates compute
environments with its template on OpenStack platform. The template
contains information about cloud resources such as virtual machines,
floating IP addresses, security groups, key-pairs, volumes, etc. With the
OpenStack Heat Template, a master node and a worker node(s) can be
configured differently with its settings for the cloud resources.

Communication (SSH) across multiple nodes
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

In a cluster environment, every node needs to communicate with each
other. Cloudmesh Cluster automatically sets up for you by utilizing
OpenStack Heat Template. We have added a ssh-copy-id like script inside
of Cloudmesh cluster command and the newly generated ssh keypair is
propagated through OpenStack Heat Template. get\_param or get\_file in
the template allows to inject the keypair to each node of the cluster.
We also update the system hosts files in each cluster node so that they
can login each other with its own hostname i.e. hadoop1 or master. This
is also done by OpenStack Heat Template. We placed an injection script
in the last node of cluster so when the user\_data is being executed,
the last node propagates all the hostnames with their private IP
addresses to /etc/hosts on the rest of nodes. This completes configuring
ssh password-less connection across the cluster node(s).

Configuration for master and worker node
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To setup a cluster with master and worker node(s), configuration and
installation are different in the master and the worker node. Cloudmesh
cluster allows you to provide a separated installation script with stdin
or a file as a user script to run on the node. With this isolated user
space for installing and configuring packages, you can easily setup a
master and a worker node in Cloudmesh. If you need to install program a
on a master node, for example, you can simply call
``cluster write [cluster name] master`` with
``apt-get install program a`` on a ubuntu image. We treat that there is
a single master and all worker node(s) are same.

Confirmation of the cluster installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To ensure everything is properly installed and configured, Cloudmesh
tries to check the installation with a few options. A Cloudmesh user can
define what to expect as a result so ``cloudmesh cluster`` can
understand whether it is successfully installed or not. Also, testing
command or script can be executed to verify the installation with
``cloudmesh cluster``. If there was error occurred, rollback would be
performed.
