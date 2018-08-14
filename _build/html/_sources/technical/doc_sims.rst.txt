========================
Creating The Suite
========================

Initial Conditions
========================

Overview
--------

We use the multi-scale cosmological initial conditions creator MUSIC.
MUSIC is a computer program to generate nested grid initial conditions
for high-resolution "zoom" cosmological simulations. A detailed
description of the algorithms can be found in Hahn & Abel (2011). You
can download the user's guide
`here <https://bitbucket.org/ohahn/music/downloads/MUSIC_Users_Guide.pdf>`__
or obtain a copy of the code
`here <https://people.phys.ethz.ch/~hahn/MUSIC/>`__. Any questions
should be directed to `Brendan Griffen <brendan.f.griffen@gmail.com>`__
and then if that fails, `Oliver Hahn <hahn@phys.ethz.ch>`__.

Parameters
----------

These are the parameter files which were used to generate the initial
coditions for the *Caterpillar* project. We adopt the raw Planck (2013)
cosmology and do not use 2nd order lagrangian perturbation theory. The
`user
guide <https://bitbucket.org/ohahn/music/downloads/MUSIC_Users_Guide.pdf>`__
contains all the information required to understand the following
parameter files. Within each simulation directory, there is a file named
``OUTPUTmusic`` which gives the log of the construction of the initial
conditions.

Parent Simulation
--------

First we constructed a parent simulation of sufficient size to include
thousands of Milky Way sized systems but also of sufficient resolution
to construct good lagrangian volumes. We decided on ~10,000 particles
per Milky Way-sized host and a 100 Mpc/h volume. Our ``level_max`` is 10
below, which means our parent simulation's effective resolution is
(210)3 = (1024)3 (i.e. a particle mass of 8.72 x 107
\\(M\_:raw-latex:`\odot`/h\\).

If you have access to the MIT cluster (``bigbang.mit.edu``), you can
access the parent simulation data here:
``/bigbang/data/AnnaGroup/caterpillar/parent/gL100X10/``. Within this
folder you'll find the following file (within ``ics/``):

.. code:: bash

    # parentics.conf
    [setup]
    boxlength               = 100
    zstart                  = 127
    levelmin                = 10
    levelmin_TF             = 10
    levelmax                = 10
    padding                 = 8
    overlap                 = 4
    ref_center              = 0.5, 0.5, 0.5
    ref_extent              = 0.2, 0.2, 0.2
    align_top               = yes
    baryons                 = no
    use_2LPT                = no
    use_LLA                 = no
    periodic_TF             = yes

    [cosmology]
    Omega_m                 = 0.3175      
    Omega_L                 = 0.6825       
    Omega_b                 = 0.049     
    H0                      = 67.11         
    sigma_8                 = 0.8344        
    nspec                   = 0.9624        
    transfer                = eisenstein

    [random]
    seed[10]                = 34567

    [output]
    format                  = gadget2
    filename                = ./ics
    gadget_num_files        = 128

    [poisson]
    fft_fine                = yes
    accuracy                = 1e-5
    pre_smooth              = 3
    post_smooth             = 3
    smoother                = gs
    laplace_order           = 6
    grad_order              = 6

Zoom-in "Caterpillar" Simulations
--------

Each simulation folder has a configuration file for MUSIC (e.g.
``H1079897_EX_Z127_P7_LN7_LX14_O4_NV4.conf``) which was used to
construct the initial conditions.

There are a few things to note about the zoom-in paramter files when
compared to the parent volume parameter file. First is we now specify a
``region_point_file`` which defines the x,y,z (normalized to the box
width) of the particles to be resampled. We have added the parameter
``hipadding`` which our own modification to allow for expanded regions.
1.05, for example, represents an expanded ellipsoid (by 5%). See Section
2.3 of `Griffen et al.
(2015) <http://adsabs.harvard.edu/cgi-bin/bib_query?arXiv:1509.01255>`__
for a more detailed description of these geometries and their impact on
contamination.

We also draw the reader's attention to the seed values. Note that we do
not set the seed values for any level lower than the parent volume (10)
which makes MUSIC smooth out any levels lower than 10. The seed values
at 11 are simply the halo numbers and then each level higher scales by a
factor of 2 of this original number. This was required because the ICs
were generated through our automatic pipeline and each simulation needs
unique values to seed the random noise field. The ``levelmin_TF`` is
also set to be the same as the parent volume (10). The padding and
overlap parameters are the same for all simulations.

.. code:: bash

    # H1079897_EX_Z127_P7_LN7_LX14_O4_NV4.conf
    [setup]
    boxlength            = 100
    zstart               = 127
    levelmin             = 7
    levelmin_TF          = 10
    levelmax             = 14
    padding              = 7
    overlap              = 4
    region               = ellipsoid
    hipadding            = 1.05
    region_point_file    = /n/home01/bgriffen/data/caterpillar/ics/lagr/H1079897NRVIR4
    align_top            = no
    baryons              = no
    use_2LPT             = no
    use_2LLA             = no
    periodic_TF          = yes

    [cosmology]
    Omega_m              = 0.3175
    Omega_L              = 0.6825
    Omega_b              = 0.049
    H0                   = 67.11
    sigma_8              = 0.8344
    nspec                = 0.9624
    transfer             = eisenstein

    [random]
    seed[10]              = 34567
    seed[11]              = 1079897
    seed[12]              = 2159794
    seed[13]              = 3239691
    seed[14]              = 4319588

    [output]
    format               = gadget2_double
    filename             = ./ics
    gadget_num_files     = 8
    gadget_spreadcoarse  = yes

    [poisson]
    fft_fine             = yes
    accuracy             = 1e-05
    pre_smooth           = 3
    post_smooth          = 3
    smoother             = gs
    laplace_order        = 6
    grad_order           = 6


Parent Simulation
========================

The parent simulation was setup primarily to find Milky Way-sized
candidates at z = 0. All the parameters used for the construction of the
simulation were oriented around this goal.

Overview
--------

.. raw:: html

   <center>

+--------+--------+--------+--------+--------+
| Volume | #      | \\(m\_ | \\(m\_ | \\(:ra |
| *h*\ ^ | partic | {dm}\\ | {dm}\\ | w-late |
| 3      | les    | )      | )      | x:`\ep |
| Mpc^3  |        | 10^7   | 10^7   | silon` |
|        |        | *h*\ ^ | \\(M\_ | \_{dm} |
|        |        | -1     | :raw-l | \\)    |
|        |        | \\(M\_ | atex:` | pc     |
|        |        | :raw-l | \odot` |        |
|        |        | atex:` | \\)    |        |
|        |        | \odot` |        |        |
|        |        | \\)    |        |        |
+========+========+========+========+========+
| 100^3  | 1024^3 | 9      | 12     | 2441   |
+--------+--------+--------+--------+--------+

.. raw:: html

   </center>

{{site.data.alerts.note}} The parent simulation initial conditions were
run on an older version of MUSIC.{{site.data.alerts.end}}

Volume
------

The volume of the parent simulation was selected to be 100 Mpc/h as this
allows for roughly ~6500 Milky Way-sized (i.e. 10^12 Msol) systems to be
found. After a gentle selection over local environment (i.e. making sure
no halos were near clusters) 2122 candidates were used to select
*Caterpillar* candidates.

Mass Resolution
---------------

We required a resolution which allowed us to resolve 10^12 Msol halos
with 10,000 particles so as to construct well defined lagrangian
volumes. This resulted in us selecting a resolution of 10243 or a
particle mass of 8.72 x 107 \\(M\_:raw-latex:`\odot`/h\\).

Halo Selection
--------------

We selected halos with the following environmental requirements:

-  halos between 0.7 - 3 x 1012 \\(M\_:raw-latex:`\odot`\\) (6564
   candidates)
-  no halos larger than 7 x 1013 \\(M\_:raw-latex:`\odot`\\) within 7
   Mpc
-  no halos larger than 7 x 1012 \\(M\_:raw-latex:`\odot`\\) within 2.8
   Mpc (2122 candidates)

This is roughly in line with Tollerud et al. (2012), Boylan-Kolchin et
al. (2013), Fardal et al. (2013), Pfiffel et al. (2013), Li & White
(2008), van der Marel et al. (2012), Karachentsev et al. (2004) and
Tikhonov & Klypin (2009). This avoids Milky Way-sized systems near
clusters but does not make them overly isolated necessarily. Halos were
also selected to not be preferentially near the very edge of the
simulation volume as a matter of convenience. The first 24 *Caterpillar*
halos are highlighted within the parent volume below.

.. raw:: html

   <center>

.. raw:: html

   </center>

Temporal Resolution
-------------------

The time steps were set to be log of the expansion factor, following a
similar convention to that used by the *Millenium* and *Millenium-II*
simulations. The following table shows the various measures for
time/size at each snapshot.

.. TIP::
    Be sure to use the halo utility module (haloutils) in Python for quickly getting the temporal quantity for a given snapshot. See data access for more information.

.. raw:: html

   <center>

 Download CSV

+--------+----------------+------------+-----------+
| Snap   | Scale Factor   | Redshift   | Time      |
+========+================+============+===========+
| 0      | 0.0213         | 46.0000    | 0.0535    |
+--------+----------------+------------+-----------+
| 1      | 0.0290         | 33.5029    | 0.0851    |
+--------+----------------+------------+-----------+
| 2      | 0.0367         | 26.2557    | 0.1212    |
+--------+----------------+------------+-----------+
| 3      | 0.0444         | 21.5245    | 0.1613    |
+--------+----------------+------------+-----------+
| 4      | 0.0521         | 18.1929    | 0.2051    |
+--------+----------------+------------+-----------+
| 5      | 0.0598         | 15.7199    | 0.2522    |
+--------+----------------+------------+-----------+
| 6      | 0.0675         | 13.8114    | 0.3025    |
+--------+----------------+------------+-----------+
| 7      | 0.0752         | 12.2940    | 0.3557    |
+--------+----------------+------------+-----------+
| 8      | 0.0829         | 11.0586    | 0.4117    |
+--------+----------------+------------+-----------+
| 9      | 0.0906         | 10.0333    | 0.4704    |
+--------+----------------+------------+-----------+
| 10     | 0.0983         | 9.1687     | 0.5316    |
+--------+----------------+------------+-----------+
| 11     | 0.1060         | 8.4297     | 0.5952    |
+--------+----------------+------------+-----------+
| 12     | 0.1138         | 7.7909     | 0.6612    |
+--------+----------------+------------+-----------+
| 13     | 0.1215         | 7.2331     | 0.7294    |
+--------+----------------+------------+-----------+
| 14     | 0.1292         | 6.7419     | 0.7998    |
+--------+----------------+------------+-----------+
| 15     | 0.1369         | 6.3060     | 0.8723    |
+--------+----------------+------------+-----------+
| 16     | 0.1446         | 5.9166     | 0.9469    |
+--------+----------------+------------+-----------+
| 17     | 0.1523         | 5.5666     | 1.0234    |
+--------+----------------+------------+-----------+
| 18     | 0.1600         | 5.2503     | 1.1018    |
+--------+----------------+------------+-----------+
| 19     | 0.1677         | 4.9630     | 1.1821    |
+--------+----------------+------------+-----------+
| 20     | 0.1754         | 4.7011     | 1.2642    |
+--------+----------------+------------+-----------+
| 21     | 0.1831         | 4.4611     | 1.3481    |
+--------+----------------+------------+-----------+
| 22     | 0.1908         | 4.2406     | 1.4337    |
+--------+----------------+------------+-----------+
| 23     | 0.1985         | 4.0371     | 1.5210    |
+--------+----------------+------------+-----------+
| 24     | 0.2062         | 3.8489     | 1.6098    |
+--------+----------------+------------+-----------+
| 25     | 0.2139         | 3.6742     | 1.7003    |
+--------+----------------+------------+-----------+
| 26     | 0.2216         | 3.5117     | 1.7923    |
+--------+----------------+------------+-----------+
| 27     | 0.2294         | 3.3601     | 1.8858    |
+--------+----------------+------------+-----------+
| 28     | 0.2371         | 3.2184     | 1.9808    |
+--------+----------------+------------+-----------+
| 29     | 0.2448         | 3.0856     | 2.0772    |
+--------+----------------+------------+-----------+
| 30     | 0.2525         | 2.9608     | 2.1749    |
+--------+----------------+------------+-----------+
| 31     | 0.2602         | 2.8435     | 2.2741    |
+--------+----------------+------------+-----------+
| 32     | 0.2679         | 2.7330     | 2.3745    |
+--------+----------------+------------+-----------+
| 33     | 0.2756         | 2.6286     | 2.4762    |
+--------+----------------+------------+-----------+
| 34     | 0.2833         | 2.5299     | 2.5792    |
+--------+----------------+------------+-----------+
| 35     | 0.2910         | 2.4364     | 2.6834    |
+--------+----------------+------------+-----------+
| 36     | 0.2987         | 2.3477     | 2.7888    |
+--------+----------------+------------+-----------+
| 37     | 0.3064         | 2.2635     | 2.8953    |
+--------+----------------+------------+-----------+
| 38     | 0.3141         | 2.1835     | 3.0029    |
+--------+----------------+------------+-----------+
| 39     | 0.3218         | 2.1072     | 3.1116    |
+--------+----------------+------------+-----------+
| 40     | 0.3295         | 2.0346     | 3.2213    |
+--------+----------------+------------+-----------+
| 41     | 0.3372         | 1.9652     | 3.3321    |
+--------+----------------+------------+-----------+
| 42     | 0.3449         | 1.8990     | 3.4438    |
+--------+----------------+------------+-----------+
| 43     | 0.3527         | 1.8356     | 3.5565    |
+--------+----------------+------------+-----------+
| 44     | 0.3604         | 1.7750     | 3.6701    |
+--------+----------------+------------+-----------+
| 45     | 0.3681         | 1.7169     | 3.7846    |
+--------+----------------+------------+-----------+
| 46     | 0.3758         | 1.6612     | 3.9000    |
+--------+----------------+------------+-----------+
| 47     | 0.3835         | 1.6077     | 4.0161    |
+--------+----------------+------------+-----------+
| 48     | 0.3912         | 1.5563     | 4.1331    |
+--------+----------------+------------+-----------+
| 49     | 0.3989         | 1.5069     | 4.2508    |
+--------+----------------+------------+-----------+
| 50     | 0.4066         | 1.4594     | 4.3693    |
+--------+----------------+------------+-----------+
| 51     | 0.4143         | 1.4137     | 4.4884    |
+--------+----------------+------------+-----------+
| 52     | 0.4220         | 1.3696     | 4.6082    |
+--------+----------------+------------+-----------+
| 53     | 0.4297         | 1.3271     | 4.7287    |
+--------+----------------+------------+-----------+
| 54     | 0.4374         | 1.2861     | 4.8497    |
+--------+----------------+------------+-----------+
| 55     | 0.4451         | 1.2465     | 4.9714    |
+--------+----------------+------------+-----------+
| 56     | 0.4528         | 1.2083     | 5.0936    |
+--------+----------------+------------+-----------+
| 57     | 0.4605         | 1.1713     | 5.2163    |
+--------+----------------+------------+-----------+
| 58     | 0.4683         | 1.1356     | 5.3395    |
+--------+----------------+------------+-----------+
| 59     | 0.4760         | 1.1010     | 5.4632    |
+--------+----------------+------------+-----------+
| 60     | 0.4837         | 1.0675     | 5.5873    |
+--------+----------------+------------+-----------+
| 61     | 0.4914         | 1.0351     | 5.7118    |
+--------+----------------+------------+-----------+
| 62     | 0.4991         | 1.0037     | 5.8367    |
+--------+----------------+------------+-----------+
| 63     | 0.5068         | 0.9732     | 5.9620    |
+--------+----------------+------------+-----------+
| 64     | 0.5145         | 0.9437     | 6.0876    |
+--------+----------------+------------+-----------+
| 65     | 0.5222         | 0.9150     | 6.2135    |
+--------+----------------+------------+-----------+
| 66     | 0.5299         | 0.8871     | 6.3396    |
+--------+----------------+------------+-----------+
| 67     | 0.5376         | 0.8601     | 6.4660    |
+--------+----------------+------------+-----------+
| 68     | 0.5453         | 0.8338     | 6.5927    |
+--------+----------------+------------+-----------+
| 69     | 0.5530         | 0.8082     | 6.7195    |
+--------+----------------+------------+-----------+
| 70     | 0.5607         | 0.7834     | 6.8465    |
+--------+----------------+------------+-----------+
| 71     | 0.5684         | 0.7592     | 6.9737    |
+--------+----------------+------------+-----------+
| 72     | 0.5761         | 0.7357     | 7.1010    |
+--------+----------------+------------+-----------+
| 73     | 0.5838         | 0.7128     | 7.2284    |
+--------+----------------+------------+-----------+
| 74     | 0.5916         | 0.6905     | 7.3559    |
+--------+----------------+------------+-----------+
| 75     | 0.5993         | 0.6687     | 7.4835    |
+--------+----------------+------------+-----------+
| 76     | 0.6070         | 0.6475     | 7.6111    |
+--------+----------------+------------+-----------+
| 77     | 0.6147         | 0.6269     | 7.7387    |
+--------+----------------+------------+-----------+
| 78     | 0.6224         | 0.6067     | 7.8663    |
+--------+----------------+------------+-----------+
| 79     | 0.6301         | 0.5871     | 7.9939    |
+--------+----------------+------------+-----------+
| 80     | 0.6378         | 0.5679     | 8.1215    |
+--------+----------------+------------+-----------+
| 81     | 0.6455         | 0.5492     | 8.2490    |
+--------+----------------+------------+-----------+
| 82     | 0.6532         | 0.5309     | 8.3764    |
+--------+----------------+------------+-----------+
| 83     | 0.6609         | 0.5131     | 8.5038    |
+--------+----------------+------------+-----------+
| 84     | 0.6686         | 0.4956     | 8.6310    |
+--------+----------------+------------+-----------+
| 85     | 0.6763         | 0.4786     | 8.7581    |
+--------+----------------+------------+-----------+
| 86     | 0.6840         | 0.4619     | 8.8851    |
+--------+----------------+------------+-----------+
| 87     | 0.6917         | 0.4456     | 9.0119    |
+--------+----------------+------------+-----------+
| 88     | 0.6994         | 0.4297     | 9.1385    |
+--------+----------------+------------+-----------+
| 89     | 0.7072         | 0.4141     | 9.2649    |
+--------+----------------+------------+-----------+
| 90     | 0.7149         | 0.3989     | 9.3912    |
+--------+----------------+------------+-----------+
| 91     | 0.7226         | 0.3840     | 9.5172    |
+--------+----------------+------------+-----------+
| 92     | 0.7303         | 0.3694     | 9.6430    |
+--------+----------------+------------+-----------+
| 93     | 0.7380         | 0.3551     | 9.7685    |
+--------+----------------+------------+-----------+
| 94     | 0.7457         | 0.3410     | 9.8938    |
+--------+----------------+------------+-----------+
| 95     | 0.7534         | 0.3273     | 10.0188   |
+--------+----------------+------------+-----------+
| 96     | 0.7611         | 0.3139     | 10.1436   |
+--------+----------------+------------+-----------+
| 97     | 0.7688         | 0.3007     | 10.2680   |
+--------+----------------+------------+-----------+
| 98     | 0.7765         | 0.2878     | 10.3922   |
+--------+----------------+------------+-----------+
| 99     | 0.7842         | 0.2752     | 10.5160   |
+--------+----------------+------------+-----------+
| 100    | 0.7919         | 0.2627     | 10.6395   |
+--------+----------------+------------+-----------+
| 101    | 0.7996         | 0.2506     | 10.7627   |
+--------+----------------+------------+-----------+
| 102    | 0.8073         | 0.2386     | 10.8855   |
+--------+----------------+------------+-----------+
| 103    | 0.8150         | 0.2269     | 11.0081   |
+--------+----------------+------------+-----------+
| 104    | 0.8228         | 0.2154     | 11.1302   |
+--------+----------------+------------+-----------+
| 105    | 0.8305         | 0.2042     | 11.2520   |
+--------+----------------+------------+-----------+
| 106    | 0.8382         | 0.1931     | 11.3734   |
+--------+----------------+------------+-----------+
| 107    | 0.8459         | 0.1822     | 11.4944   |
+--------+----------------+------------+-----------+
| 108    | 0.8536         | 0.1715     | 11.6151   |
+--------+----------------+------------+-----------+
| 109    | 0.8613         | 0.1611     | 11.7354   |
+--------+----------------+------------+-----------+
| 110    | 0.8690         | 0.1508     | 11.8552   |
+--------+----------------+------------+-----------+
| 111    | 0.8767         | 0.1406     | 11.9747   |
+--------+----------------+------------+-----------+
| 112    | 0.8844         | 0.1307     | 12.0938   |
+--------+----------------+------------+-----------+
| 113    | 0.8921         | 0.1209     | 12.2124   |
+--------+----------------+------------+-----------+
| 114    | 0.8998         | 0.1113     | 12.3307   |
+--------+----------------+------------+-----------+
| 115    | 0.9075         | 0.1019     | 12.4485   |
+--------+----------------+------------+-----------+
| 116    | 0.9152         | 0.0926     | 12.5659   |
+--------+----------------+------------+-----------+
| 117    | 0.9229         | 0.0835     | 12.6828   |
+--------+----------------+------------+-----------+
| 118    | 0.9306         | 0.0745     | 12.7994   |
+--------+----------------+------------+-----------+
| 119    | 0.9383         | 0.0657     | 12.9155   |
+--------+----------------+------------+-----------+
| 120    | 0.9461         | 0.0570     | 13.0311   |
+--------+----------------+------------+-----------+
| 121    | 0.9538         | 0.0485     | 13.1464   |
+--------+----------------+------------+-----------+
| 122    | 0.9615         | 0.0401     | 13.2611   |
+--------+----------------+------------+-----------+
| 123    | 0.9692         | 0.0318     | 13.3755   |
+--------+----------------+------------+-----------+
| 124    | 0.9769         | 0.0237     | 13.4894   |
+--------+----------------+------------+-----------+
| 125    | 0.9846         | 0.0157     | 13.6028   |
+--------+----------------+------------+-----------+
| 126    | 0.9923         | 0.0078     | 13.7158   |
+--------+----------------+------------+-----------+
| 127    | 1.0000         | 0.0000     | 13.8283   |
+--------+----------------+------------+-----------+

.. raw:: html

   </center>


Zoom-in "Caterpillar" Halos
========================

.. NOTE::
   The majority of the information about the zoom-in runs can be found in `Griffen et al. (2016) <http://adsabs.harvard.edu/cgi-bin/bib_query?arXiv:1509.01255>`__. Here we simply outline some details which were left out of the publication for the sake of brevity.

Overview
--------

.. raw:: html

   <center>

+--------+--------+--------+--------+--------+--------+
| ~\ *Aq | MUSIC  | Effect | \\(m\_ | \\(m\_ | \\(:ra |
| uarius | *level | ive    | {dm}\\ | {dm}\\ | w-late |
| *      | max*   | Resolu | )      | )      | x:`\ep |
| Level  |        | tion   | 10^4   | 10^4   | silon` |
|        |        |        | *h*\ ^ | \\(M\_ | \_{dm} |
|        |        |        | -1     | :raw-l | \\)    |
|        |        |        | \\(M\_ | atex:` | pc/h   |
|        |        |        | :raw-l | \odot` |        |
|        |        |        | atex:` | \\)    |        |
|        |        |        | \odot` |        |        |
|        |        |        | \\)    |        |        |
+========+========+========+========+========+========+
| 1      | 15     | 32768^ | 0.25   | 0.37   | 36     |
|        |        | 3      |        |        |        |
+--------+--------+--------+--------+--------+--------+
| **2**  | **14** | **1638 | **2**  | **3**  | **76** |
|        |        | 4^3**  |        |        |        |
+--------+--------+--------+--------+--------+--------+
| 3      | 13     | 8096^3 | 16     | 24     | 152    |
+--------+--------+--------+--------+--------+--------+
| 4      | 12     | 4096^3 | 128    | 190    | 228    |
+--------+--------+--------+--------+--------+--------+
| 5      | 11     | 2048^3 | 1025   | 1527   | 452    |
+--------+--------+--------+--------+--------+--------+

.. raw:: html

   </center>

Each panel represents one single realization of the Cat-1 halo at
different resolutions. The far left is an LX11 run and the far right is
an LX14 run.

.. NOTE:: 
   The LX15 run has currently only been run for one of the halos and has been temporarily paused at z = 1. This will be finished with a few others once the main suite has been completed.

We have complete (modified) rockstar halo catalogues (together with
consistent-trees merger trees) and z = 0 subfind catalogues.

Force Softening
---------------

Softening was 1/80th the interparticle separation. We adopt the formula:
``boxwidth/lx^2/80`` but stagger the force softenings for each higher
level as 4 x base, 8 x base, 32 x base, 64 x base where base is the base
force softening. For each of the zooms, this equates to:

.. raw:: html

   <center>

+----------------------+---------------+---------------+---------------+----------------+
| In Gadget            | LX11          | LX12          | LX13          | LX14           |
+======================+===============+===============+===============+================+
| ``SofteningHalo``    | 0.000610352   | 0.000305176   | 0.000152588   | 0.0000762939   |
+----------------------+---------------+---------------+---------------+----------------+
| ``SofteningDisk``    | 0.002441406   | 0.001220703   | 0.000610352   | 0.000305176    |
+----------------------+---------------+---------------+---------------+----------------+
| ``SofteningBulge``   | 0.004882813   | 0.002441406   | 0.001220703   | 0.000610352    |
+----------------------+---------------+---------------+---------------+----------------+
| ``SofteningStars``   | 0.01953125    | 0.009765625   | 0.004882813   | 0.002441406    |
+----------------------+---------------+---------------+---------------+----------------+
| ``SofteningBndry``   | 0.0390625     | 0.01953125    | 0.009765625   | 0.004882813    |
+----------------------+---------------+---------------+---------------+----------------+

units of Mpc/h

.. raw:: html

   </center>

Temporal Resolution
-------------------

.. IMPORTANT::
   Timesteps are spaced logarithmically in expansion factor to z = 6, then linearly spaced in expansion factor down to z = 0. Always be aware of this as it could be strength and a weakness of your study.

This image shows the difference between the time step resolutions used
in Caterpillar and those used in the Aquarius simulation. We wanted
higher resolution at all redshifts for many purposes. At z > 6 we wanted
to model Lyman-Werner radiation which requires timesteps of order the
lifespan of Population III star formation. At low redshift we wanted
timesteps of roughly 50-60 Myrs which is the disruption time scale of
many small dwarf galaxies of the Milky Way. This also allows detailed
modelling of the pericentric passages of infalling satellite systems,
which is a crucial parameter for determining post-infall mass loss, for
example.

.. raw:: html

   <center>

.. raw:: html

   </center>

Contamination Study
-------------------

A number of contamination studies have been carried out. This involves
changing the Lagrangian geometry in some way to keep the contamination
(distance to the nearest particle type 2 as far as possible) low whilst
conserving CPU hours. Our selected test geometries were as follows

.. raw:: html

   <center>

+--------+------+
| Geomet | Deta |
| ry     | il   |
+========+======+
| BA     | Orig |
|        | inal |
|        | MUSI |
|        | C    |
|        | boun |
|        | ding |
|        | box  |
|        | (e.g |
|        | .    |
|        | the  |
|        | exac |
|        | t    |
|        | boun |
|        | ding |
|        | box  |
|        | of   |
|        | lagr |
|        | volu |
|        | me). |
+--------+------+
| BB     | 1.2  |
|        | boun |
|        | ding |
|        | box  |
|        | exte |
|        | nt   |
+--------+------+
| BC     | 1.4  |
|        | boun |
|        | ding |
|        | box  |
|        | exte |
|        | nt   |
+--------+------+
| BD     | 1.6  |
|        | boun |
|        | ding |
|        | box  |
|        | exte |
|        | nt   |
+--------+------+
| CA     | Conv |
|        | ex   |
|        | Hull |
|        | Volu |
|        | me   |
+--------+------+
| EA     | Orig |
|        | inal |
|        | MUSI |
|        | C    |
|        | elli |
|        | psoi |
|        | d    |
|        | (e.g |
|        | .    |
|        | the  |
|        | exac |
|        | t    |
|        | boun |
|        | ding |
|        | box  |
|        | of   |
|        | lagr |
|        | volu |
|        | me). |
+--------+------+
| EB     | 1.1  |
|        | padd |
|        | ing  |
+--------+------+
| EC     | 1.2  |
|        | padd |
|        | ing  |
+--------+------+
| EX     | 1.05 |
|        | padd |
|        | ing  |
+--------+------+

.. raw:: html

   </center>

We did this for both 4 and 5 times the virial radius at z = 0 (marked by
the letter 4 or 5 at the end of the abbreviated geometry). Making a
total of ~18 test halos per *Caterpillar* halo. Our requirement was that
there was no contamation (particle type 2) within 1 Mpc of the host at
the LX11 level.

We also looked at how the geometry of the lagrangian volume affected the
contamination radius. As outlined in Griffen et al. (2015), we did not
find any correlation with geometry and overall level contamination.
Every simulation requires its own tailored geometry to achieve our
contamination requirements.

.. raw:: html

   <center>

.. raw:: html

   </center>

The size of the lagrangian volumes were also another challenge to
overcome. If a halo had LX11 ICs which were larger than 300mb, we found
that we could not run these at LX14 on national facilities. The size and
distance became our two biggest obstacles when running the *Caterpillar*
suite.

.. raw:: html

   <center>

.. raw:: html

   </center>

Our rockstar catalogues only use the high-resolution particles. This
means that there will be halos in the outskirts of the simulation which
are contaminated. These are shown clearly below. Be sure not to just
take all halos within the rockstar catalogues as some of them will be
contaminated (underestimated masses, wrong profiles etc.). As a safety,
one should only take halos which are within the contamination distance.
This changes as a function of redshift so make sure you update your cut
for each snapshot. The plots below are for z = 0.

.. raw:: html

   <center>

.. raw:: html

   </center>
