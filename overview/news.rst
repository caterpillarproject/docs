Documentation News & Updates
========================

**[BFG Aug, 2018]** New documentation page built on Sphinx-RTD made available.

**[APJ Jan, 2016]** The majority of halos have now been upgraded to 320 snaps. Some halos had hiccups in the upgrade process. These are H95289 and H1725372 (Cat-20 and Cat-11, respectively). They are currently being fixed and should be online soon. Standard postprocessing plugins have not yet been run. Status of all Caterpillar halos can be found at this link (updated once per day): https://www.dropbox.com/s/t35s3k7l15257uq/status.png

**[APJ Oct, 2015]** IMPORTANT! We are currently re-running rockstar on several LX14 halos to increase their time resolution up to 320 snaps (instead of 256). Due to our slow rockstar, I this will probably take about 2-3 weeks per halo on one AMD node (at best 7 run at a time). While this happens, our standard haloutils.py code (e.g. load_rscat, load_partblock ) will not correctly access data from several halo IDs. For the bad halos, Brendan has kept their old rockstar catalogs in halos_bound_coarse which you can read manually with RSDataReader and MTCatalogue. The old coarse snapshots are kept on the "grinder" storage server, and if you need them you should ask Brendan.