History & Motivation
========================

.. NOTE::
    Much more detail of the Caterpillar project can be found in Griffen et al. (2015).

A Brief History
---------------

The Caterpillar project was the brainchild of Profs. Anna Frebel and
Lars Hernquist at the CfA in ~2010. In 2012, Phillip Zukin was then a
PhD student under Edmund Bertschinger at MIT who was temporarily
employed to carry out the first parent volume simulations that would
become the Caterpillar project. His work continued until Brendan Griffen
arrived as the new postdoc to take charge of the project in its entirety
in late 2012. Graduate students Greg Dooley and Alex Ji also contributed heavily to the project throughout their PhD at MIT. At a conference at UC Irvine in early 2014
between Anna Frebel, Brian O'Shea, Brendan Griffen and Facundo Gomez, it
was agreed that we would combined datasets and future efforts (Brian and
Facundo had a similar sized project for studying stellar halos at the
time). In September of 2015, the first Caterpillar paper was put `on the
arxiv <http://arxiv.org/abs/1509.01255v1>`__.

Motivation
----------

The Caterpillar project is a large simulation suite of dark matter halos
of mass similar in size to that of the Milky Way. By virtue of the
extremely large number of halos, temporal and spatial resolution of the
simulations, it is one of the largest simulation suites of its kind in the
world. We plan to extend the initial release sample to 40 halos in
total.

The goal of the Caterpillar Project is to use these relatively
inexpensive dark matter simulations to:

-  statistically probe the merger history of Milky Way-like galaxies,
-  understand the origin and evolution of the satellite systems of Milky
   Way-like galaxies and
-  determine to what extent the Milky Way is unusual relative to its
   similar sized cousins.
-  probe the earliest progenitors of the Milky Way and determine the
   properties of their surviving populations.

Approach
------------------

The *Caterpillar* suite was run using P-Gadget3 and Gadget4, tree-based
*n*-body codes based on Gadget2 (Springel et al. 2005). For the
underlying cosmological model we adopt the \\(:raw-latex:`\Lambda`\\)CDM
parameter set characterised by a Planck cosmology given by,
\\(:raw-latex:`\Omega`\ *m=0.32\\),
\\(:raw-latex:`\Omega`*\ :raw-latex:`\Lambda`=0.68\\),
\\(:raw-latex:`\Omega`\_b=0.05\\), \\(n\_s=0.96\\),
\\(:raw-latex:`\sigma`\ *8=0.83\\) and Hubble constant, H = 100
\\(h km s\ :sup:`{-1} Mpc`\ {-1}\\) = 67.11
\\(km s\ :sup:`{-1} Mpc`\ {-1}\\) (Planck et al. 2014). All initial
conditions were constructed using music (Hahn & Abel 2011). We identify
dark matter halos via Rockstar (Behroozi et al. 2013) and construct
merger trees using consistent-trees (Behroozi et al. 2012). Rockstar
assigns virial masses to halos, \\(M*\ {vir}\\), using the evolution of
the virial relation from Bryan & Norman (1998). for our particular
cosmology. At *z* = 0, this definition corresponds to an over-density of
104x the critical density of the Universe. We have modified rockstar to
output *all* particles belonging to each halo so we can reconstruct any
halo property in post-processing if required. We have also improved the
code to include iterative unbinding. In our work, we restrict our
definition of virial mass to include only those particles which are
bound to the halo.
