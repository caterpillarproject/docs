Using MIT's Compute Cluster
========================

The MKI cluster (with respect to Caterpillar) at MIT has one login node
(``antares.mit.edu``) which connects to a three primary blocks of slave
nodes and one analysis node (``bigbang.mit.edu``).

.. raw:: html

   <center>

.. raw:: html

   </center>

Compute Nodes
--------------------------------------------------------

These nodes are accessed through  `antares.mit.edu (for farming jobs)`.

RegNodes
~~~~~~~~

Block 1: \* 22 nodes (176 cores) \* 8 core [2 Ghz] \* 16GB memory \* 1
Gbit interconnect

Block 2: \* 9 nodes (72 cores) \* 8 cores, 2.5 Ghz \* 16GB memory \* 1
Gbit interconnect

This partition should be used for *serial jobs*. All nodes can be
accessed via using the partition ``RegNodes``.

HyperNodes
~~~~~~~~~~

-  12 nodes (144 cores)
-  12 cores, 2.3 Ghz (24 with hyper-threading)
-  24GB memory
-  10 Gbit interconnect

This partition should only be used for *MPI enabled* codes as it has
faster interconnect.

AMD64
~~~~~

-  8 nodes, 512 cores
-  64 cores, 2.2 Ghz
-  256GB memory
-  10 Gbit interconnect

This partition should *only be used for extremely expensive runs which
require 100GB++ memory and for codes that are MPI enabled*. You can also
used openMP multi-threaded jobs which require large amounts of memory (1
job per node). At this stage, there are no time-limits or fixed memory
limits for each of the nodes.

Analysis Nodes
--------------

The two analysis nodes are Bigbang and Blender.

The Frebel group as MIT also has access to an analysis node which is connected to the Caterpillar data called ``bigbang``. It can be accessed via ssh ``username@bigbang.mit.edu``. See Data Access on this site to get started with your analysis once you understand the storage layout below.

Storage File Systems/Servers
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Frebel group has access to ~120GB RAID storage and 300TB+ of ZFS
tape storage. The ZFS tape storage consists of two 130TB servers
(``grinder`` and ``cruncher``). These are significantly slower to do I/O
from *the first time*. They each have solid state drives on them acting
as a large cache which makes reading data comparable to the RAID drives
if you are repeatedly accessing the same snapshot on the tape, for
example. The directory structure is as follows:

.. code:: bash

    login node: ssh username@bigbang.mit.edu

    # ZFS TAPE STORAGE SERVERS (not as fast as the RAID  slow to load)
     -> cruncher/
      -> caterpillar/
       -> parent/
       -> halos/
        -> H1079897/

     -> grinder/  # ZFS tape drive with 
      -> caterpillar/
       -> halos/
        -> H1387186
        ...
      -> aquarius/
       -> Aq-A/
       -> Aq-B/
       -> Aq-C/
       -> Aq-D/
       -> Aq-E/
       -> Aq-F/

    # RAID STORAGE
     -> data/AnnaGroup/     # RAID drive with all runs lower than LX14
      -> caterpillar/
       -> halos/            # master folder with all of the caterpillar data within
        -> H1079897/        # halos are named according to their folders
        ...
       -> ics/
        -> lagr/            # lagrangian volume files
       -> parent/           # parent simulation runs
        -> gL100X10/        # actual parent simulation (X10 refers to Level_max=10 in MUSIC)

Current Storage Options
--------------

We are quite limited with storage space and so we ask you to request
more storage if you need it. You will then be allocated a directory on
``bigbang/data/{username}/``. The current break down of the storage
capability is as follows:

.. code:: bash

    bigbang% df -h
    Filesystem            Size  Used Avail Use% Mounted on
    /dev/mapper/vg_bigbang-lv_home
                           57G  1.9G   52G   4% /home
    /dev/mapper/vg_bigdata-lv_bigdata
                          121T   93T   28T  78% /bigbang/data
    /cruncher/data
                          127T  114T   14T  90% /cruncher/data
    /grinder/data
                          127T   74T   54T  59% /grinder/data
    /spacebase/data
                           36T   33M   36T   1% /spacebase/data

Where is the data *actually* stored?
------------

Due to our storage limitations we have opted for the following strategy

-  you should only ever get your hpaths from haloutils via
   ``hpaths = haloutils.get_paper_paths_lx(14)``, for example. Do not
   get your halo paths from ever going into
   ``caterpillar/halos/middle_mass_halos/*``.
-  all simulation runs lower than LX14 (i.e. LX11,12,13) have been
   stored on the RAID drives.
-  all LX14 runs are *symbolically linked* on the RAID drives but might
   not actually exist physically on the drives.
-  all halo catalogues are on the RAID drives so access for these is
   very fast
-  all particle data *except* the last snapshot are actually stored on
   the ZFS tape drives (though it will appear in outputs/ as a symlink)
-  only the last snapshot of the particle data is actually stored on the
   RAID drives
-  all postprocessed catalogues in ``analysis/`` of each halo directory
   are on the RAID drives
-  all of the aquarius data is on the ZFS tape storage as this is not
   often used
-  the parent simulation (``gL100X10``) is stored in the same way as the
   LX14 runs: only the last snapshot of the particle data is stored on
   the RAID drives, everything else is on the ZFS tape drives.

Submitting Jobs
========================

Example SLURM Submission Scripts
--------------------------------

Scripts can be submitted via using the command ``sbatch sub.script``.
There are a number of options you can specify but the key ones are
listed here.

-  ``#SBATCH -n 1`` This line sets the number of cores that you're
   requesting. Make sure that your tool can use multiple cores before
   requesting more than one.

-  ``#SBATCH -t 5`` This line specifies the running time for the job in
   minutes. If your job runs longer than the value you specify here, it
   will be cancelled. There is currently no time limit to jobs so you
   can leave this out for now.

-  ``#SBATCH -p RegNodes`` This line specifies the SLURM partition (AKA
   queue) under which the script will be run. The RegNodes partition is
   good for routine jobs that can handle being occasionally stopped and
   restarted. PENDING times are typically short for this queue as it has
   the most number of cores.

-  ``#SBATCH -o hostname.out`` This line specifies the file to which
   standard out will be appended. If a relative file name is used, it
   will be relative to your current working directory.

-  ``#SBATCH -e hostname.err`` This line specifies the file to which
   standard error will be appended. SLURM submission and processing
   errors will also appear in the file.

-  ``#SBATCH --mail-user=ajk@123.com`` The email address to which the
   --mail-type messages will be sent.

-  ``#SBATCH --mail-type=END`` Because jobs are processed in the
   "background" and can take some time to run, it is useful send an
   email message when the job has finished (--mail-type=END). Email can
   also be sent for other processing stages (START, FAIL) or at all of
   the times (ALL)

Here a few example scripts. Contact [mailto:brendan.f.griffen@gmail.com
Brendan Griffen] if you would like help constructing something more
specific. [https://rc.fas.harvard.edu/resources/running-jobs/ Harvard
FAS] has a great number of examples and useful tips.

-  I have a simple serial job which doesn't require much memory.

.. code:: bash

    #!/bin/bash
    #SBATCH -n 1
    #SBATCH -o jobname.o%j
    #SBATCH -e jobname.e%j
    #SBATCH -p RegNodes
    #SBATCH -J jobname
    #SBATCH --share

    ./job.exe

-  I have an openMP task which requires a large amount of memory (up to
   256GB).

.. code:: bash

    #!/bin/bash
    #SBATCH -N 1 -n 64
    #SBATCH -o jobname.o%j
    #SBATCH -e jobname.e%j
    #SBATCH -p AMD64
    #SBATCH -J jobname

    export OMP_NUM_THREADS=64
    ./job.exe

-  I have a MPI job which doesn't use much memory.

.. code:: bash

    #!/bin/bash
    #SBATCH -N 2 -n 16
    #SBATCH -o jobname.o%j
    #SBATCH -e jobname.e%j
    #SBATCH -p RegNodes
    #SBATCH -J jobname

    mpirun -np 16 ./P-Gadget3 param.txt 1>OUTPUT 2>ERROR

-  I have a job which is requires lots of IO between MPI tasks but
   doesn't consume much memory.

.. code:: bash

    #!/bin/bash
    #SBATCH -n 16
    #SBATCH -o jobname.o%j
    #SBATCH -e jobname.e%j
    #SBATCH -p HyperNodes
    #SBATCH -J jobname

    mpirun -np 16 ./job.exe

-  I have a MPI job which requires a very large amount of memory.

.. code:: bash

    #!/bin/bash
    #SBATCH -n 128
    #SBATCH -o jobname.o%j
    #SBATCH -e jobname.e%j
    #SBATCH -p RegNodes
    #SBATCH -J jobname

    mpirun -np 128 ./job.exe

Visualizing Cluster Usage
-------------------------

The cluster now can be visualized interactively. Just type ``> sview``
in the command prompt on antares.mit.edu and you'll see the an
infographic.

Alternatively, you can use Ganglia which can be found here:
http://antares.mit.edu/ganglia/

SLURM Status & Error Help
-------------------------

Status Messages
~~~~~~~~~~~~~~~

When you type ``squeue -u username`` you should see a shortened version
of one of the following (e.g. PD for PENDING). You can also see these in
the ``sview``.

-  ``PENDING`` Job is awaiting a slot suitable for the requested
   resources. Jobs with high resource demands may spend significant time
   PENDING.

-  ``RUNNING`` Job is running.

-  | ``COMPLETED``
   | Job has finished and the command(s) have returned successfully
     (i.e. exit code 0).

-  | ``CANCELLED``
   | Job has been terminated by the user or administrator using scancel.

-  | ``FAILED``
   | Job finished with an exit code other than 0.

Error Messages
~~~~~~~~~~~~~~

-  | ``JOB <jobid> CANCELLED AT <time> DUE TO TIME LIMIT``
   | You did not specify enough time in your batch submission script.
     The -t option sets time in minutes, or can also take
     hours:minutes:seconds form (12:30:00 for 12.5 hours)

-  | ``Job <jobid> exceeded <mem> memory limit, being killed``
   | Your job is attempting to use more memory than you've requested for
     it. Either increase the amount of memory requested by ``--mem`` or
     ``--mem-per-cpu`` or, if possible, reduce the amount your
     application is trying to use. For example, many Java programs set
     heap space using the ``-Xmx`` JVM option. This could potentially be
     reduced.

-  | ``slurm_receive_msg: Socket timed out on send/recv operation``
   | This message indicates a failure of the SLURM controller. Though
     there are many possible explanations, it is generally due to an
     overwhelming number of jobs being submitted, or, occasionally,
     finishing simultaneously. If you want to figure out if SLURM is
     working use the ``sdiag`` command. ``sdiag`` should respond quickly
     in these situations and give you an idea as to what the scheduler
     is up to.

-  ``JOB <jobid> CANCELLED AT <time> DUE TO NODE FAILURE`` This message
   may arise for a variety of reasons, but it indicates that the host on
   which your job was running can no longer be contacted by SLURM.

Again, see the `Harvard FAS SLURM
website <https://rc.fas.harvard.edu/resources/running-jobs/>`__ for
extra information and help.

