====================
Available Datasets
====================

Please refer to the Current Status and Policies page before proceeding.

Particle Data (Gadget)
-------------

See Data Access Examples to see how to load each of these blocks. One such way is:

.. code:: python

    import haloutils as htils
    hpath = htils.get_paper_paths_lx(14)[0]
    zoomid = htils.load_zoomid(hpath)
    blockname = "POS " # NOTE THE EXTRA SPACE!
    pos = htils.load_partblock(hpath,zoomid,blockname,partids=[listofids]) # units Mpc/h

{{site.data.alerts.tip}} Make sure you include the right number of
spaces (4) otherwise you will get an error when trying to read the
blocks.{{site.data.alerts.end}}

Other blocks you have access to are listed below:

.. raw:: html

   <center>

+---------+-------+--------+---------+
| Block   | Descr | Units  | Notes   |
| Name    | iptio |        |         |
|         | n     |        |         |
+=========+=======+========+=========+
| ``ID``  | ID    | -      | --      |
|         | numbe |        |         |
|         | r     |        |         |
|         | (N)   |        |         |
+---------+-------+--------+---------+
| ``POS`` | posit | comovi | They    |
|         | ion   | ng     | are all |
|         | (Nx3) | Mpc/h  | around  |
|         |       |        | ~50     |
|         |       |        | Mpc/h   |
|         |       |        | as they |
|         |       |        | are in  |
|         |       |        | the     |
|         |       |        | center  |
|         |       |        | of the  |
|         |       |        | 100     |
|         |       |        | Mpc/h   |
|         |       |        | box for |
|         |       |        | the     |
|         |       |        | resimul |
|         |       |        | ations. |
+---------+-------+--------+---------+
| ``VEL`` | veloc | spatia | Spatial |
|         | ity   | l      | velocit |
|         | (Nx3) | km\\(: | y.      |
|         |       | raw-la | The     |
|         |       | tex:`\ | peculia |
|         |       | sqrt`( | r       |
|         |       | a)\\)/ | velocit |
|         |       | s      | y       |
|         |       |        | is      |
|         |       |        | obtaine |
|         |       |        | d       |
|         |       |        | by      |
|         |       |        | multipl |
|         |       |        | ying    |
|         |       |        | this    |
|         |       |        | value   |
|         |       |        | by      |
|         |       |        | \\(:raw |
|         |       |        | -latex: |
|         |       |        | `\sqrt` |
|         |       |        | (a)\\). |
+---------+-------+--------+---------+
| ``MASS` | parti | Msol/h | Use     |
| `       | cle   |        | ``heade |
|         | mass  |        | r.massa |
|         | (N)   |        | rr[1]*1 |
|         |       |        | e10``   |
|         |       |        | as it   |
|         |       |        | is      |
|         |       |        | faster  |
|         |       |        | than    |
|         |       |        | reading |
|         |       |        | in the  |
|         |       |        | entire  |
|         |       |        | block.  |
+---------+-------+--------+---------+
| ``POT`` | poten | ---    | ----    |
|         | tial  |        |         |
|         | energ |        |         |
|         | y     |        |         |
+---------+-------+--------+---------+

.. raw:: html

   </center>

{{site.data.alerts.warning}} Remember to use the scale factor for the
snapshot you are working on to convert the comoving quantities to
physical. For z = 0, it doesn't matter.{{site.data.alerts.end}}

Halo Catalogues (Rockstar)
-----------

Rockstar outputs a large number of halo properties.

.. raw:: html

   <center>

+--------+------+------+------+
| variab | unit | defi | note |
| le     | s    | niti | s    |
|        |      | on   |      |
+========+======+======+======+
| ``id`` |      | the  |      |
|        |      | ID   |      |
|        |      | numb |      |
|        |      | er   |      |
|        |      | of   |      |
|        |      | the  |      |
|        |      | halo |      |
+--------+------+------+------+
| ``posX | Mpc/ | como |      |
| ``     | h    | ving |      |
|        |      | x-po |      |
|        |      | siti |      |
|        |      | on   |      |
+--------+------+------+------+
| ``posY | Mpc/ | como |      |
| ``     | h    | ving |      |
|        |      | y-po |      |
|        |      | siti |      |
|        |      | on   |      |
+--------+------+------+------+
| ``posZ | Mpc/ | como |      |
| ``     | h    | ving |      |
|        |      | z-po |      |
|        |      | siti |      |
|        |      | on   |      |
+--------+------+------+------+
| ``pecV | km/s | Pecu |      |
| X``    |      | liar |      |
|        |      | x-di |      |
|        |      | r    |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``pecV | km/s | Pecu |      |
| Y``    |      | liar |      |
|        |      | y-di |      |
|        |      | r    |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``pecV | km/s | Pecu |      |
| Z``    |      | liar |      |
|        |      | z-di |      |
|        |      | r    |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``core | km/s | x-di |      |
| velX`` |      | r    |      |
|        |      | core |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``core | km/s | y-di |      |
| velY`` |      | r    |      |
|        |      | core |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``core | km/s | z-di |      |
| velZ`` |      | r    |      |
|        |      | core |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``bulk | como | x-di |      |
| velX`` | ving | r    |      |
|        | km/s | bulk |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``bulk | como | y-di |      |
| velY`` | ving | r    |      |
|        | km/s | bulk |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``bulk | como | z-di |      |
| velZ`` | ving | r    |      |
|        | km/s | bulk |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``mvir | Msol | viri | this |
| ``     | /h   | al   | shou |
|        |      | mass | ld   |
|        |      | set  | only |
|        |      | by   | be   |
|        |      | `Bry | used |
|        |      | an   | for  |
|        |      | &    | the  |
|        |      | Norm | mass |
|        |      | an   | ive  |
|        |      | (199 | host |
|        |      | 8) < | halo |
|        |      | http | s    |
|        |      | ://c | - it |
|        |      | dsad | is   |
|        |      | s.u- | best |
|        |      | stra | to   |
|        |      | sbg. | just |
|        |      | fr/a | use  |
|        |      | bs/1 | ``mg |
|        |      | 998A | rav` |
|        |      | pJ.. | `    |
|        |      | .495 |      |
|        |      | ...8 |      |
|        |      | 0B>` |      |
|        |      | __   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
+--------+------+------+------+
| ``mgra | Msol | viri | when |
| v``    | /h   | al   | usin |
|        |      | mass | g    |
|        |      | set  | the  |
|        |      | by   | cata |
|        |      | `Bry | logu |
|        |      | an   | es,  |
|        |      | &    | only |
|        |      | Norm | use  |
|        |      | an   | this |
|        |      | (199 | quan |
|        |      | 8) < | tity |
|        |      | http | as   |
|        |      | ://c | it   |
|        |      | dsad | is   |
|        |      | s.u- | the  |
|        |      | stra | grav |
|        |      | sbg. | itat |
|        |      | fr/a | iona |
|        |      | bs/1 | lly  |
|        |      | 998A | boun |
|        |      | pJ.. | d    |
|        |      | .495 | mass |
|        |      | ...8 | of   |
|        |      | 0B>` | the  |
|        |      | __   | halo |
|        |      | pres | -    |
|        |      | crip | espe |
|        |      | tion | cial |
|        |      |      | ly   |
|        |      |      | for  |
|        |      |      | subh |
|        |      |      | alos |
+--------+------+------+------+
| ``rvir | kpc/ | viri |      |
| ``     | h    | al   |      |
|        |      | radi |      |
|        |      | us   |      |
|        |      | set  |      |
|        |      | by   |      |
|        |      | `Bry |      |
|        |      | an   |      |
|        |      | &    |      |
|        |      | Norm |      |
|        |      | an   |      |
|        |      | (199 |      |
|        |      | 8) < |      |
|        |      | http |      |
|        |      | ://c |      |
|        |      | dsad |      |
|        |      | s.u- |      |
|        |      | stra |      |
|        |      | sbg. |      |
|        |      | fr/a |      |
|        |      | bs/1 |      |
|        |      | 998A |      |
|        |      | pJ.. |      |
|        |      | .495 |      |
|        |      | ...8 |      |
|        |      | 0B>` |      |
|        |      | __   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
+--------+------+------+------+
| ``chil |      |      |      |
| d_r``  |      |      |      |
+--------+------+------+------+
| ``vmax | km/s |      |      |
| _r``   |      |      |      |
+--------+------+------+------+
| ``mgra | Msol | grav |      |
| v``    | /h   | itat |      |
|        |      | iona |      |
|        |      | l    |      |
|        |      | mass |      |
+--------+------+------+------+
| ``vmax | km/s | Maxi |      |
| ``     |      | mum  |      |
|        |      | circ |      |
|        |      | ular |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``rvma | kpc/ | radi |      |
| x``    | h    | us   |      |
|        |      | at   |      |
|        |      | maxi |      |
|        |      | mum  |      |
|        |      | circ |      |
|        |      | ular |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``rs`` | kpc/ | NFW  |      |
|        | h    | scal |      |
|        |      | e    |      |
|        |      | radi |      |
|        |      | us   |      |
+--------+------+------+------+
| ``rs_k | kpc/ | Klyp | bett |
| lypin` | h    | in   | er   |
| `      |      | defi | for  |
|        |      | ned  | smal |
|        |      | scal | ler  |
|        |      | e    | halo |
|        |      | radi | s    |
|        |      | us   |      |
+--------+------+------+------+
| ``vrms | km/s | rms  |      |
| ``     |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``Jx`` |      | x-co |      |
|        |      | mpon |      |
|        |      | ent  |      |
|        |      | angu |      |
|        |      | lar  |      |
|        |      | mome |      |
|        |      | ntum |      |
+--------+------+------+------+
| ``Jy`` |      | y-co |      |
|        |      | mpon |      |
|        |      | ent  |      |
|        |      | angu |      |
|        |      | lar  |      |
|        |      | mome |      |
|        |      | ntum |      |
+--------+------+------+------+
| ``Jz`` |      | z-co |      |
|        |      | mpon |      |
|        |      | ent  |      |
|        |      | angu |      |
|        |      | lar  |      |
|        |      | mome |      |
|        |      | ntum |      |
+--------+------+------+------+
| ``Epot |      | Pote |      |
| ``     |      | ntia |      |
|        |      | l    |      |
|        |      | ener |      |
|        |      | gy   |      |
|        |      | of   |      |
|        |      | the  |      |
|        |      | halo |      |
+--------+------+------+------+
| ``spin |      | Peeb | This |
| ``     |      | les  | shou |
|        |      | defi | ld   |
|        |      | ned  | only |
|        |      | spin | be   |
|        |      | para | used |
|        |      | mete | for  |
|        |      | r    | halo |
|        |      |      | s    |
|        |      |      | with |
|        |      |      | a    |
|        |      |      | larg |
|        |      |      | e    |
|        |      |      | numb |
|        |      |      | er   |
|        |      |      | of   |
|        |      |      | part |
|        |      |      | icle |
|        |      |      | s    |
|        |      |      | (~50 |
|        |      |      | 0+)  |
+--------+------+------+------+
| ``spin |      | Bull | See  |
| _bullo |      | ock' | abov |
| ck``   |      | s    | e.   |
|        |      | modi |      |
|        |      | fied |      |
|        |      | spin |      |
|        |      | para |      |
|        |      | mete |      |
|        |      | r    |      |
+--------+------+------+------+
| ``xoff |      | Posi |      |
| ``     |      | tion |      |
|        |      | offs |      |
|        |      | et   |      |
|        |      | para |      |
|        |      | mete |      |
|        |      | r    |      |
|        |      | abs( |      |
|        |      | cent |      |
|        |      | er   |      |
|        |      | of   |      |
|        |      | mass |      |
|        |      | posi |      |
|        |      | tion |      |
|        |      | -    |      |
|        |      | halo |      |
|        |      | posi |      |
|        |      | tion |      |
|        |      | )    |      |
+--------+------+------+------+
| ``voff |      | Velo |      |
| ``     |      | city |      |
|        |      | offs |      |
|        |      | et   |      |
|        |      | para |      |
|        |      | mete |      |
|        |      | r    |      |
|        |      | abs( |      |
|        |      | cent |      |
|        |      | er   |      |
|        |      | of   |      |
|        |      | mass |      |
|        |      | velo |      |
|        |      | city |      |
|        |      | -    |      |
|        |      | halo |      |
|        |      | velo |      |
|        |      | city |      |
|        |      | )    |      |
+--------+------+------+------+
| ``b_to |      | Halo |      |
| _a``   |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | b/a  |      |
+--------+------+------+------+
| ``c_to |      | Halo |      |
| _a``   |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | c/a  |      |
+--------+------+------+------+
| ``b_to |      | Halo |      |
| _a2``  |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | b/a  |      |
|        |      | (dif |      |
|        |      | fere |      |
|        |      | nt   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
|        |      | )    |      |
+--------+------+------+------+
| ``c_to |      | Halo |      |
| _a2``  |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | c/a  |      |
|        |      | (dif |      |
|        |      | fere |      |
|        |      | nt   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
|        |      | )    |      |
+--------+------+------+------+
| ``A[x] |      | x-ax |      |
| ``     |      | is   |      |
|        |      | for  |      |
|        |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | a    |      |
+--------+------+------+------+
| ``A[y] |      | y-xi |      |
| ``     |      | s    |      |
|        |      | for  |      |
|        |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | a    |      |
+--------+------+------+------+
| ``A[z] |      | z-xi |      |
| ``     |      | s    |      |
|        |      | for  |      |
|        |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | a    |      |
+--------+------+------+------+
| ``A2[x |      | x-ax |      |
| ]``    |      | is   |      |
|        |      | for  |      |
|        |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | a    |      |
|        |      | (dif |      |
|        |      | fere |      |
|        |      | nt   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
|        |      | )    |      |
+--------+------+------+------+
| ``A2[y |      | y-xi |      |
| ]``    |      | s    |      |
|        |      | for  |      |
|        |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | a    |      |
|        |      | (dif |      |
|        |      | fere |      |
|        |      | nt   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
|        |      | )    |      |
+--------+------+------+------+
| ``A2[z |      | z-xi |      |
| ]``    |      | s    |      |
|        |      | for  |      |
|        |      | elli |      |
|        |      | ptic |      |
|        |      | ity  |      |
|        |      | a    |      |
|        |      | (dif |      |
|        |      | fere |      |
|        |      | nt   |      |
|        |      | pres |      |
|        |      | crip |      |
|        |      | tion |      |
|        |      | )    |      |
+--------+------+------+------+
| ``T/ab |      | Viri |      |
| s(U)`` |      | al   |      |
|        |      | rati |      |
|        |      | o    |      |
|        |      | (kin |      |
|        |      | etic |      |
|        |      | /abs |      |
|        |      | (pot |      |
|        |      | enti |      |
|        |      | al)) |      |
+--------+------+------+------+
| ``min_ |      | Mini |      |
| pos_er |      | mum  |      |
| r``    |      | erro |      |
|        |      | r    |      |
|        |      | in   |      |
|        |      | posi |      |
|        |      | tion |      |
+--------+------+------+------+
| ``min_ |      | Mini |      |
| vel_er |      | mum  |      |
| r``    |      | erro |      |
|        |      | r    |      |
|        |      | in   |      |
|        |      | bulk |      |
|        |      | velo |      |
|        |      | city |      |
+--------+------+------+------+
| ``min_ |      | Mini |      |
| bulkve |      | mum  |      |
| l_err` |      | bulk |      |
| `      |      | velo |      |
|        |      | city |      |
|        |      | erro |      |
|        |      | r.   |      |
+--------+------+------+------+
| ``tota |      | The  |      |
| l_npar |      | tota |      |
| t``    |      | l    |      |
|        |      | numb |      |
|        |      | er   |      |
|        |      | of   |      |
|        |      | part |      |
|        |      | icle |      |
|        |      | s    |      |
|        |      | asso |      |
|        |      | ciat |      |
|        |      | ed   |      |
|        |      | with |      |
|        |      | this |      |
|        |      | halo |      |
|        |      | (sub |      |
|        |      | s    |      |
|        |      | incl |      |
|        |      | uded |      |
|        |      | )    |      |
+--------+------+------+------+
| ``npar |      | The  |      |
| t``    |      | numb |      |
|        |      | er   |      |
|        |      | of   |      |
|        |      | part |      |
|        |      | icle |      |
|        |      | s    |      |
|        |      | asso |      |
|        |      | ciat |      |
|        |      | ed   |      |
|        |      | with |      |
|        |      | a    |      |
|        |      | halo |      |
|        |      | (doe |      |
|        |      | s    |      |
|        |      | not  |      |
|        |      | incl |      |
|        |      | ude  |      |
|        |      | subh |      |
|        |      | alos |      |
|        |      | )    |      |
+--------+------+------+------+

.. raw:: html

   </center>

Merger Trees (consistent-trees)
-----------

The consistent-trees output it similar to that of the rockstar catalogue
except now there are additional paramters which connect the halos in
time.

.. raw:: html

   <center>

+----------+--------+------------+
| variable | units  | definition |
| le       |        | niti.      |
|          |        | on         |
+========+========+======+
| ``id`` | -      | id   |
|        |        | of   |
|        |        | the  |
|        |        | halo |
|        |        | in   |
|        |        | the  |
|        |        | merg |
|        |        | er   |
|        |        | tree |
+--------+--------+------+
| ``pid` | -      | the  |
| `      |        | next |
|        |        | leve |
|        |        | l    |
|        |        | up   |
|        |        | halo |
|        |        | if   |
|        |        | the  |
|        |        | halo |
|        |        | is a |
|        |        | subh |
|        |        | alo  |
|        |        | (oth |
|        |        | erwi |
|        |        | se   |
|        |        | -1)  |
+--------+--------+------+
| ``upid | -      | the  |
| ``     |        | ID   |
|        |        | of   |
|        |        | the  |
|        |        | uppe |
|        |        | rmos |
|        |        | t    |
|        |        | leve |
|        |        | l    |
|        |        | of   |
|        |        | the  |
|        |        | halo |
|        |        | if   |
|        |        | the  |
|        |        | halo |
|        |        | is a |
|        |        | subh |
|        |        | alo  |
|        |        | (oth |
|        |        | erwi |
|        |        | se   |
|        |        | -1)  |
+--------+--------+------+
| ``bfid | -      | brea |
| ``     |        | dth  |
|        |        | firs |
|        |        | t    |
|        |        | orde |
|        |        | r    |
|        |        | id   |
+--------+--------+------+
| ``dfid | -      | dept |
| ``     |        | h    |
|        |        | firs |
|        |        | t    |
|        |        | orde |
|        |        | r    |
|        |        | id   |
+--------+--------+------+
| ``orig | -      | orig |
| id``   |        | inal |
|        |        | id   |
|        |        | as   |
|        |        | iden |
|        |        | tifi |
|        |        | ed   |
|        |        | in   |
|        |        | Rock |
|        |        | star |
|        |        | cata |
|        |        | logu |
|        |        | e    |
+--------+--------+------+
| ``last | -      | last |
| prog_d |        | prog |
| fid``  |        | enit |
|        |        | or   |
|        |        | dept |
|        |        | h    |
|        |        | firs |
|        |        | t    |
|        |        | id   |
+--------+--------+------+
| ``snap | -      | snap |
| ``     |        | shot |
+--------+--------+------+
| ``scal | -      | scal |
| e``    |        | e    |
|        |        | fact |
|        |        | or   |
+--------+--------+------+
| ``desc | -      | desc |
| _id``  |        | enda |
|        |        | nt   |
|        |        | id   |
+--------+--------+------+
| ``num_ | -      | numb |
| prog`` |        | er   |
|        |        | of   |
|        |        | prog |
|        |        | enit |
|        |        | ors  |
+--------+--------+------+
| ``phan | -      | Nonz |
| tom``  |        | ero  |
|        |        | if   |
|        |        | the  |
|        |        | halo |
|        |        | is a |
|        |        | "pha |
|        |        | ntom |
|        |        | "    |
|        |        | halo |
|        |        | ,    |
|        |        | i.e. |
|        |        | a    |
|        |        | halo |
|        |        | not  |
|        |        | foun |
|        |        | d    |
|        |        | by   |
|        |        | Rock |
|        |        | star |
|        |        | but  |
|        |        | inse |
|        |        | rted |
|        |        | by   |
|        |        | cons |
|        |        | iste |
|        |        | nt-t |
|        |        | rees |
|        |        | to   |
|        |        | link |
|        |        | time |
|        |        | step |
|        |        | s    |
+--------+--------+------+
| ``sam_ | Msol/h | smoo |
| mvir`` |        | thed |
|        |        | viri |
|        |        | al   |
|        |        | mass |
+--------+--------+------+
| ``mvir | Msol/h | viri |
| ``     |        | al   |
|        |        | mass |
|        |        | (Bri |
|        |        | an   |
|        |        | &    |
|        |        | Norm |
|        |        | an   |
|        |        | pres |
|        |        | crip |
|        |        | tion |
|        |        | )    |
|        |        | (it  |
|        |        | is   |
|        |        | actu |
|        |        | ally |
|        |        | mgra |
|        |        | v    |
|        |        | from |
|        |        | Rock |
|        |        | star |
|        |        | )    |
+--------+--------+------+
| ``rvir | kpc    | viri |
| ``     |        | al   |
|        |        | radi |
|        |        | us   |
|        |        | (Bri |
|        |        | an   |
|        |        | &    |
|        |        | Norm |
|        |        | an   |
|        |        | pres |
|        |        | crip |
|        |        | tion |
|        |        | )    |
+--------+--------+------+
| ``rs`` | kpc    | scal |
|        |        | e    |
|        |        | radi |
|        |        | us   |
+--------+--------+------+
| ``vrms | km/s   | rms  |
| ``     |        | velo |
|        |        | city |
+--------+--------+------+
| ``mmp` | -      | most |
| `      |        | mass |
|        |        | ive  |
|        |        | prog |
|        |        | enit |
|        |        | or   |
+--------+--------+------+
| ``scal | -      | scal |
| e_of_l |        | e    |
| ast_MM |        | fact |
| ``     |        | or   |
|        |        | of   |
|        |        | last |
|        |        | majo |
|        |        | r    |
|        |        | merg |
|        |        | er   |
+--------+--------+------+
| ``vmax | km/s   | maxi |
| ``     |        | mum  |
|        |        | circ |
|        |        | ular |
|        |        | velo |
|        |        | city |
+--------+--------+------+
| ``posX | kpc    | x-po |
| ``     |        | siti |
|        |        | on   |
+--------+--------+------+
| ``posY | kpc    | y-po |
| ``     |        | siti |
|        |        | on   |
+--------+--------+------+
| ``posZ | kpc    | z-po |
| ``     |        | siti |
|        |        | on   |
+--------+--------+------+
| ``pecV | km/s   | x-di |
| X``    |        | r    |
|        |        | pecu |
|        |        | liar |
|        |        | velo |
|        |        | city |
+--------+--------+------+
| ``pecV | km/s   | y-di |
| Y``    |        | r    |
|        |        | pecu |
|        |        | liar |
|        |        | velo |
|        |        | city |
+--------+--------+------+
| ``pecV | km/s   | z-di |
| Z``    |        | r    |
|        |        | pecu |
|        |        | liar |
|        |        | velo |
|        |        | city |
+--------+--------+------+
| ``Jx`` |        | x-co |
|        |        | mpon |
|        |        | ent  |
|        |        | angu |
|        |        | lar  |
|        |        | mome |
|        |        | ntum |
+--------+--------+------+
| ``Jy`` |        | y-co |
|        |        | mpon |
|        |        | ent  |
|        |        | angu |
|        |        | lar  |
|        |        | mome |
|        |        | ntum |
+--------+--------+------+
| ``Jz`` |        | z-co |
|        |        | mpon |
|        |        | ent  |
|        |        | angu |
|        |        | lar  |
|        |        | mome |
|        |        | ntum |
+--------+--------+------+
| ``spin |        | spin |
| ``     |        | para |
|        |        | mete |
|        |        | r    |
|        |        | (Pee |
|        |        | bles |
|        |        | vers |
|        |        | ion) |
+--------+--------+------+
| ``spin |        | spin |
| _bullo |        | para |
| ck``   |        | mete |
|        |        | r    |
|        |        | (Bul |
|        |        | lock |
|        |        | modi |
|        |        | fied |
|        |        | vers |
|        |        | ion) |
+--------+--------+------+
| ``m200 | Msol/h | viri |
| c_all` |        | al   |
| `      |        | mass |
|        |        | of   |
|        |        | all  |
|        |        | part |
|        |        | icle |
|        |        | s    |
|        |        | base |
|        |        | d    |
|        |        | on   |
|        |        | 200x |
|        |        | crit |
|        |        | ical |
|        |        | dens |
|        |        | ity  |
+--------+--------+------+
| ``m200 | Msol/h | viri |
| b``    |        | al   |
|        |        | mass |
|        |        | of   |
|        |        | all  |
|        |        | part |
|        |        | icle |
|        |        | s    |
|        |        | base |
|        |        | d    |
|        |        | on   |
|        |        | 200x |
|        |        | back |
|        |        | grou |
|        |        | nd   |
|        |        | dens |
|        |        | ity  |
+--------+--------+------+
| ``xoff | kpc    | Posi |
| ``     |        | tion |
|        |        | offs |
|        |        | et   |
|        |        | para |
|        |        | mete |
|        |        | r    |
|        |        | abs( |
|        |        | cent |
|        |        | er   |
|        |        | of   |
|        |        | mass |
|        |        | posi |
|        |        | tion |
|        |        | -    |
|        |        | halo |
|        |        | posi |
|        |        | tion |
|        |        | )    |
+--------+--------+------+
| ``voff | kpc    | Velo |
| ``     |        | city |
|        |        | offs |
|        |        | et   |
|        |        | para |
|        |        | mete |
|        |        | r    |
|        |        | abs( |
|        |        | cent |
|        |        | er   |
|        |        | of   |
|        |        | mass |
|        |        | velo |
|        |        | city |
|        |        | -    |
|        |        | halo |
|        |        | velo |
|        |        | city |
|        |        | )    |
+--------+--------+------+
| ``b_to | -      | Halo |
| _a(500 |        | elli |
| c)``   |        | ptic |
|        |        | ity  |
|        |        | b/a  |
+--------+--------+------+
| ``c_to | -      | Halo |
| _a(500 |        | elli |
| c)``   |        | ptic |
|        |        | ity  |
|        |        | c/a  |
+--------+--------+------+
| ``A[x] |        | x-ax |
| (500c) |        | is   |
| ``     |        | for  |
|        |        | elli |
|        |        | ptic |
|        |        | ity  |
+--------+--------+------+
| ``A[y] |        | y-xi |
| (500c) |        | s    |
| ``     |        | for  |
|        |        | elli |
|        |        | ptic |
|        |        | ity  |
+--------+--------+------+
| ``A[z] |        | z-xi |
| (500c) |        | s    |
| ``     |        | for  |
|        |        | elli |
|        |        | ptic |
|        |        | ity  |
+--------+--------+------+
| ``T/ab | -      | Viri |
| s(U)`` |        | al   |
|        |        | rati |
|        |        | o    |
|        |        | (kin |
|        |        | etic |
|        |        | /abs |
|        |        | (pot |
|        |        | enti |
|        |        | al)) |
+--------+--------+------+

.. raw:: html

   </center>

As listed in the previous table, ``consistent-trees`` outputs two
indexes for the connecting the halos, (1) depth-first ordered or (2)
breadth-first ordered. The graphic below indicates what the fundamental
differences are between these two methods.

.. raw:: html

   <center>

.. raw:: html

   </center>

