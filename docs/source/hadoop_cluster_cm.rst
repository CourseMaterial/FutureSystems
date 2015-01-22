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

You expect the result similar to:

.. parsed-literal::

        +--------------------------------------+-------------------------------+------------------------------------+--------------------+----------------------+----------+
        | launcher_id                          | stack_name                    | description                        | stack_status       | creation_time        | cm_cloud |
        +--------------------------------------+-------------------------------+------------------------------------+--------------------+----------------------+----------+
        | 14ec7ceb-ce12-4b18-9c31-d398c6e76b78 | launcher-albert-hadoop-DB8JDK | Hadoop cluster with OpenStack Heat | CREATE_IN_PROGRESS | 2015-01-22T16:25:23Z | india    |
        +--------------------------------------+-------------------------------+------------------------------------+--------------------+----------------------+----------+

* CREATE_IN_PROGRESS: cluster is not available because creating the cluster is in progress.
* CREATE_COMPLETE: cluster has been created and it is ready to use.

Login Cluster
~~~~~~~~~~~~~~~~

We use ``cm vm login`` command to ssh to one of the nodes in the cluster.
Issue ``vm list`` first to see the list of virtual instances.

* Checking a login node name

::

        cm vm list

You expect the result similar to:

.. parsed-literal::

        +---------------------------+----------+----------------------------+----------+----------------------------+
        | name                      | status   | addresses                  | flavor   | image                      |
        +===========================+==========+============================+==========+============================+
        | **hadoop1**                   | ACTIVE   | 10.39.1.48, 149.165.159.02 | m1.small | futuresystems/ubuntu-14.04 |
        +---------------------------+----------+----------------------------+----------+----------------------------+
        | hadoop2                   | ACTIVE   | 10.39.1.52                 | m1.small | futuresystems/ubuntu-14.04 |
        +---------------------------+----------+----------------------------+----------+----------------------------+
        | hadoop3                   | ACTIVE   | 10.39.1.51                 | m1.small | futuresystems/ubuntu-14.04 |
        +---------------------------+----------+----------------------------+----------+----------------------------+
        | hadoop4                   | ACTIVE   | 10.39.1.53                 | m1.small | futuresystems/ubuntu-14.04 |
        +---------------------------+----------+----------------------------+----------+----------------------------+
        | hadoop5                   | ACTIVE   | 10.39.1.54                 | m1.small | futuresystems/ubuntu-14.04 |
        +---------------------------+----------+----------------------------+----------+----------------------------+
        | albert-server-54zmzloc5tp | ACTIVE   | 10.39.1.41, 149.165.159.01 | m1.small | cloudmesh/ipynb-n-java     |
        +---------------------------+----------+----------------------------+----------+----------------------------+


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


