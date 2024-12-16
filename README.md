# utl-simple-ascii-plot-to-visually-display-the-the-overlap-of-two-time-series-proc-plot-graph
Simple ascii plot to visually display the the overlap of two time series proc plot graph
    %let pgm=utl-simple-ascii-plot-to-visually-display-the-the-overlap-of-two-time-series-proc-plot-graph;

    %stop_submission;

    Simple ascii plot to visually display the the overlap of two time series proc plot graph

    Not as simple with r ggplot or sas sgplot?

    github
    https://tinyurl.com/48xtfa3t
    https://github.com/rogerjdeangelis/utl-simple-ascii-plot-to-visually-display-the-the-overlap-of-two-time-series-proc-plot-graph


    /**************************************************************************************************************************/
    /*                                          |                                                                             */
    /*             INPUT                        |                             PROCESS                                         */
    /*             =====                        |                             =======                                         */
    /*                                          |                                                                             */
    /*                                          | Display the the overlap of two time series                                  */
    /* data have;                               |                                                                             */
    /*                                          |                                                                             */
    /*  call streaminit(1234567);               |                                                                             */
    /*                                          | options ls=72 ps=15;                                                        */
    /*  do day=1 to 64;                         | proc plot data=have;                                                        */
    /*    if rand('uniform')>.5 then seq1=1;    |  plot                                                                       */
    /*    else seq1=.;                          |    seq1*day='|'                                                             */
    /*    if rand('uniform')>.5 then seq2=2;    |    seq2*day='|'                                                             */
    /*    else seq2=.;                          |    overlap*day='|' /                                                        */
    /*    if seq1=1 and seq2=2  then overlap=0; |      overlay box haxis=1 to 64 by 1;                                        */
    /*    else overlap=.;                       | run;quit;                                                                   */
    /*    put day  seq1 seq2 overlap  @;        |                                                                             */
    /*    output;                               |                                                                             */
    /*  end;                                    |                                                                             */
    /*                                          |                                                                             */
    /* run;quit;                                |                               OUTPUT                                        */
    /*                                          |                               ======                                        */
    /*                                          |                                                                             */
    /*                                          |                                  DAY                                        */
    /*                                          |     1234567891111111111222222222233333333334444444444555555555566666        */
    /* run;quit;                                | SEQ          0123456789012345678901234567890123456789012345678901234        *
    /*                                          |    -++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--      */
    /* day    seq1    seq2    overlap           |    |                                                                 |      */
    /*                                          |  2 + |||||||| |  |    || |  |||  ||||  |||| |||| || |||||      ||| | + 2    */
    /*   1      .       .       .  gap all 3    |  1 + |  || | || |     |  || |  ||  | | || ||     | ||| | |  |  | |   + 1    */
    /*   2      1       1       1               |    |                                                                 |      */
    /*   3      .       1       .               |    |                           OVERLAP                               |      */
    /*  ...                                     |    |                                                                 |      */
    /*  62      1       1       1               |  0 + |  || |  |       |  |  |      |   || |      |  || |       | |   + 0    */
    /*  63      .       .       .               |    -++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--      */
    /*  64      .       1       .               |     1234567891111111111222222222233333333334444444444555555555566666        */
    /*                                          |              0123456789012345678901234567890123456789012345678901234        */
    /*                                          |                                   DAY                                       */
    /*                                          |                                                                             */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options ls=255 ps=72;
    data have;

     call streaminit(1234567);

     do day=1 to 64;
       if rand('uniform')>.5 then seq1=1;
       else seq1=.;
       if rand('uniform')>.5 then seq2=2;
       else seq2=.;
       if seq1=1 and seq2=2  then overlap=0;
       else overlap=.;
       output;
     end;

    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  DAY    SEQ1    SEQ2    OVERLAP   DAY    SEQ1    SEQ2    OVERLAP                                                       */
    /*                                                                                                                        */
    /*    1      .       .        .                                                                                           */
    /*    2      1       2        0       33      .       2        .                                                          */
    /*    3      .       2        .       34      1       .        .                                                          */
    /*    4      .       2        .       35      .       .        .                                                          */
    /*    5      1       2        0       36      1       2        0                                                          */
    /*    6      1       2        0       37      1       2        0                                                          */
    /*    7      .       2        .       38      .       2        .                                                          */
    /*    8      1       2        0       39      1       2        0                                                          */
    /*    9      .       2        .       40      1       .        .                                                          */
    /*   10      1       .        .       41      .       2        .                                                          */
    /*   11      1       2        0       42      .       2        .                                                          */
    /*   12      .       .        .       43      .       2        .                                                          */
    /*   13      1       .        .       44      .       2        .                                                          */
    /*   14      .       2        .       45      .       .        .                                                          */
    /*   15      .       .        .       46      1       2        0                                                          */
    /*   16      .       .        .       47      .       2        .                                                          */
    /*   17      .       .        .       48      1       .        .                                                          */
    /*   18      .       .        .       49      1       2        0                                                          */
    /*   19      1       2        0       50      1       2        0                                                          */
    /*   20      .       2        .       51      .       2        .                                                          */
    /*   21      .       .        .       52      1       2        0                                                          */
    /*   22      1       2        0       53      .       2        .                                                          */
    /*   23      1       .        .       54      1       .        .                                                          */
    /*   24      .       .        .       55      .       .        .                                                          */
    /*   25      1       2        0       56      .       .        .                                                          */
    /*   26      .       2        .       57      1       .        .                                                          */
    /*   27      .       2        .       58      .       .        .                                                          */
    /*   28      1       .        .       59      .       .        .                                                          */
    /*   29      1       .        .       60      1       2        0                                                          */
    /*   30      .       2        .       61      .       2        .                                                          */
    /*   31      .       2        .       62      1       2        0                                                          */
    /*   32      1       2        0       63      .       .        .                                                          */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    options ls=72 ps=15;
    proc plot data=have;
     plot
       seq1*day='|'
       seq2*day='|'
       overlap*day='|' /
         overlay box haxis=1 to 64 by 1;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                 Plot of seq1*day.     Symbol used is '|'.                                                              */
    /*                 Plot of seq2*day.     Symbol used is '|'.                                                              */
    /*                 Plot of overlap*day.  Symbol used is '|'.                                                              */
    /*                                                                                                                        */
    /*  seq1 -(NOTE: 107 obs had missing values.)+++++++++++++++++++++++++++++--                                              */
    /*     2 + |||||||| |  |    || |  |||  ||||  |||| |||| || |||||      ||| | +                                              */
    /*       |                                                                 |                                              */
    /*     1 + |  || | || |     |  || |  ||  | | || ||     | ||| | |  |  | |   +                                              */
    /*       |                                                                 |                                              */
    /*     0 + |  || |  |       |  |  |      |   || |      |  || |       | |   +                                              */
    /*       -++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--                                              */
    /*        1234567891111111111222222222233333333334444444444555555555566666                                                */
    /*                 0123456789012345678901234567890123456789012345678901234                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

























































































































 day    seq1    seq2    seq3

   1      .       .       .
   2      1       1       1
   3      .       1       .
  ...
  62      1       1       1
  63      .       .       .
  64      .       1       .


01 . . . 02 1 2 . 03 . 2 . 04 . 2 .
05 1 2 . 06 1 2 . 07 . 2 . 08 1 2 .
09 . 2 .            10 1 . .0 11 1 2 . 12 . . .
13 1 . . 14 . 2 . 15 . . . 16 . . .
17 . . . 18 . . . 19 1 2 . 20 . 2 .
21 . . . 22 1 2 . 23 1 . . 24 . . .
25 1 2 . 26 . 2 . 27 . 2 . 28 1 . .
29 1 . . 30 . 2 . 31 . 2 . 32 1 2 .
33 . 2 . 34 1 . . 35 . . . 36 1 2 .
37 1 2 . 38 . 2 . 39 1 2 . 40 1 . .
41 . 2 . 42 . 2 . 43 . 2 . 44 . 2 .
45 . . . 46 1 2 . 47 . 2 . 48 1 . .
49 1 2 . 50 1 2 . 51 . 2 . 52 1 2 .
53 . 2 . 54 1 . . 55 . . . 56 . . .
57 1 . . 58 . . . 59 . . . 60 1 2 .
61 . 2 . 62 1 2 . 63 . . . 64 . 2 .





data have;

 call streaminit(1234567);

 do day=1 to 64;
   if rand('uniform')>.5 then seq1=1;
   else seq1=.;
   if rand('uniform')>.5 then seq2=2;
   else seq2=.;
   if seq1=1 and seq2=2  then overlap=0;
   else overlap=.;
   put day  seq1 seq2 overlap  @;
   output;
 end;

run;quit;


options ls=72 ps=16;
proc plot data=have;
 plot
  seq1*day='|'
  seq2*day='|'
  overlap*day='|'/
    overlay box haxis=1 to 64 by 1;
run;quit;



















01 . . . 02 1 2 0 03 . 2 . 04 . 2 .
05 1 2 0 06 1 2 0 07 . 2 . 08 1 2 0
09 . 2 . 10 1 . . 11 1 2 0 12 . . .
13 1 . . 14 . 2 . 15 . . . 16 . . .
17 . . . 18 . . . 19 1 2 0 20 . 2 .
21 . . . 22 1 2 0 23 1 . . 24 . . .
25 1 2 0 26 . 2 . 27 . 2 . 28 1 . .
29 1 . . 30 . 2 . 31 . 2 . 32 1 2 0
33 . 2 . 34 1 . . 35 . . . 36 1 2 0
37 1 2 0 38 . 2 . 39 1 2 0 40 1 . .
41 . 2 . 42 . 2 . 43 . 2 . 44 . 2 .
45 . . . 46 1 2 0 47 . 2 . 48 1 . .
49 1 2 0 50 1 2 0 51 . 2 . 52 1 2 0
53 . 2 . 54 1 . . 55 . . . 56 . . .
57 1 . . 58 . . . 59 . . . 60 1 2 0
61 . 2 . 62 1 2 0 63 . . . 64 . 2 .
;;;;
run;quit;




















1 . . . 2 1 2 0 3 . 2 . 4 . 2 . 5 1 2 0 6 1 2 0 7 . 2 . 8 1 2 0 9 . 2 .
10 1 . . 11 1 2 0 12 . . . 13 1 . . 14 . 2 . 15 . . . 16 . . . 17 . . .
18 . . . 19 1 2 0 20 . 2 . 21 . . . 22 1 2 0 23 1 . . 24 . . . 25 1 2 0
26 . 2 . 27 . 2 . 28 1 . . 29 1 . . 30 . 2 . 31 . 2 . 32 1 2 0 33 . 2 .
34 1 . . 35 . . . 36 1 2 0 37 1 2 0 38 . 2 . 39 1 2 0 40 1 . . 41 . 2 .
42 . 2 . 43 . 2 . 44 . 2 . 45 . . . 46 1 2 0 47 . 2 . 48 1 . . 49 1 2 0
50 1 2 0 51 . 2 . 52 1 2 0 53 . 2 . 54 1 . . 55 . . . 56 . . . 57 1 . .
58 . . . 59 . . . 60 1 2 0 61 . 2 . 62 1 2 0 63 . . . 64 . 2 .
























options ls=72 ps=16;
proc plot data=have;
  plot seq1*day='|' seq2*day='|'  seq3*day='|'/ overlay box haxis=1 to 64 by 1;
run;quit;



     -+-------+-------+-------+-------+-------+-------+-------+-------+-
seq1 |                                                                 |
   2 +  |||||||| |  |    || |  |||  ||||  |||| |||| || |||||      ||| |+
     |                                                                 |
   1 +  |  || | || |     |  || |  ||  | | || ||     | ||| | |  |  | |  +
     |                                                                 |
   0 +  |  || |  |       |  |  |      |   || |      |  || |       | |  +
     -+-------+-------+-------+-------+-------+-------+-------+-------+-
       1234567891111111111222222222233333333334444444444555555555566666
                0123456789012345678901234567890123456789012345678901234
                            day

proc sgplot data=your_data nocycleattrs;
  series x=time y=value1 / group=category1;
  series x=time y=value2 / group=category2;
run;
