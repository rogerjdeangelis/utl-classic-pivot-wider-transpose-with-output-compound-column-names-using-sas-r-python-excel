# utl-classic-pivot-wider-transpose-with-output-compound-column-names-using-sas-r-python-excel
Classic pivot wider transpose with output compound column names using sas r python excel
    %let pgm=utl-classic-pivot-wider-transpose-with-output-compound-column-names-using-sas-r-python-excel;

    %stop_submission;

    Classic pivot wider transpose with output compound column names using sas r python excel


    Pivot wider in r with compound column names using arts transpose

             SEVEN SOLUTIONS

                1 sas transpose
                2 r tidyverse language
                3 sas sql
                4 r sql
                5 python sql
                6 excel sql
                7 proc corresp


    github
    https://tinyurl.com/3kww82ch
    https://github.com/rogerjdeangelis/utl-classic-pivot-wider-transpose-with-output-compound-column-names-using-sas-r-python-excel

    stackoverflow
    https://tinyurl.com/22fvcu6e
    https://stackoverflow.com/questions/79343986/pivot-wider-in-r-with-2-variables-to-names-from

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                             |                                                  |                                       */
    /*         INPUT               |      PROCESS                                     |            OUTPUT                     */
    /*         =====               |      ========                                    |            ======                     */
    /*Note CATxFAVORxYEAR is unique| SQL code is actually more flexible(fast w index) |                                       */
    /*                             |                                                  |                                       */
    /* options validvarname=upcase;| Pivot by cat combinations                        |     M     G  G  M  M  G       G       */
    /* libname sd1 "d:/sd1";       | of favor and year for                            |     E  B  O  O  E  E  O  B  B O       */
    /* data sd1.have;              | variable pct                                     |     D  A  O  O  D  D  O  A  A O       */
    /*  informat cat favor $4.;    |                                                  |     I  D  D  D  I  I  D  D  D D       */
    /*  input CAT YEAR PCT FAVOR;  | 1 SAS TRANSPOSE                                  |     _  _  _  _  _  _  _  _  _ _       */
    /* cards;                      |   =============                                  |     2  2  2  2  1  2  1  1  2 1       */
    /* A 2002 36 Medi              |                                                  | C   0  0  0  0  9  0  9  9  0 9       */
    /* B 2002 36 Bad               | proc transpose data=sd1.have                     | A   0  0  0  0  9  0  9  9  0 9       */
    /* B 2001 71 Good              |      out=want(drop=_name_)                       | T   2  2  1  2  9  1  9  8  1 8       */
    /* B 2002 60 Good              |      delimiter=_;                                | --------------------------------      */
    /* B 1999 33 Medi              |   by cat;                                        | A  36  .  .  .  .  .  .  .  . .       */
    /* B 2001 37 Medi              |   id favor year;                                 | B   . 36 71 60 33 37  .  .  . .       */
    /* C 1999 80 Good              |   var pct;                                       | C  37  .  . 70  . 38 80  .  . .       */
    /* C 2002 70 Good              | run;quit;                                        | D  48  . 68 58  .  .  .  .  . .       */
    /* C 2001 38 Medi              |                                                  | E   .  .  . 67  .  .  . 29 30 .       */
    /* C 2002 37 Medi              | 2 R TIDYVERSE                                    | F   .  .  .  .  .  . 44  .  . .       */
    /* D 2001 68 Good              | =============                                    | H   .  . 88  .  .  .  .  .  . .       */
    /* D 2002 58 Good              |                                                  | I   . 46  . 65  .  .  .  .  . .       */
    /* D 2002 48 Medi              | want<-have %>%                                   | J   .  .  .  .  .  . 86  .  . .       */
    /* E 1998 29 Bad               |  arrange(                                        | K  35 33  .  .  .  . 80  .  . .       */
    /* E 2001 30 Bad               |    CAT,                                          | M   .  .  .  .  .  .  . 29  .69       */
    /* E 2002 67 Good              |    factor(FAVOR, levels =                        | N   .  . 80  .  .  .  .  . 2075       */
    /* F 1999 44 Good              |      c("Bad", "Medi", "Good")),                  | O   .  .  .  .  .  .  . 13  . .       */
    /* H 2001 88 Good              |    YEAR                                          | P  34  .  .  .  . 31 67 38  . .       */
    /* I 2002 46 Bad               |  ) %>%                                           |                                       */
    /* I 2002 65 Good              |  pivot_wider(                                    |                                       */
    /* J 1999 86 Good              |    names_from = c(FAVOR, YEAR),                  |                                       */
    /* K 2002 33 Bad               |    values_from = PCT,                            |                                       */
    /* K 1999 80 Good              |    names_sep = "_"                               |                                       */
    /* K 2002 35 Medi              |  )                                               |                                       */
    /* M 1998 29 Bad               |                                                  |                                       */
    /* M 1998 69 Good              |------------------------------------------------------------------------------------------*/
    /* N 2001 20 Bad               |                                                                                          */
    /* N 1998 75 Good              | 3-6 SAS SQL (CODE IS GENERATED)                                                          */
    /* N 2001 80 Good              |   EXACT SAME CODE IN SAS, R, PYTHON and EXCEL                                            */
    /* O 1998 13 Bad               |   ===========================================                                            */
    /* P 1998 38 Bad               |                                                                                          */
    /* P 1999 67 Good              |  select                                                                                  */
    /* P 2001 31 Medi              |     cat                                                                                  */
    /* P 2002 34 Medi              |    ,max(case when fvyr='Bad_1998'  then pct  else . end) as Bad_1998                     */
    /* ;;;;                        |    ,max(case when fvyr='Bad_2001'  then pct  else . end) as Bad_2001                     */
    /* run;quit;                   |    ,max(case when fvyr='Bad_2002'  then pct  else . end) as Bad_2002                     */
    /*                             |    ,max(case when fvyr='Good_1998' then pct  else . end) as Good_1998                    */
    /*                             |    ,max(case when fvyr='Good_1999' then pct  else . end) as Good_1999                    */
    /*                             |    ,max(case when fvyr='Good_2001' then pct  else . end) as Good_2001                    */
    /*                             |    ,max(case when fvyr='Good_2002' then pct  else . end) as Good_2002                    */
    /*                             |    ,max(case when fvyr='Medi_1999' then pct  else . end) as Medi_1999                    */
    /*                             |    ,max(case when fvyr='Medi_2001' then pct  else . end) as Medi_2001                    */
    /*                             |    ,max(case when fvyr='Medi_2002' then pct  else . end) as Medi_2002                    */
    /*                             |  from                                                                                    */
    /*                             |     compound                                                                             */
    /*                             |  group                                                                                   */
    /*                             |     by cat                                                                               */
    /*                             |                                                                                          */
    /*                             |  7 SAS PROC CORRESP                                                                      */
    /*                             |  ===================                                                                     */
    /*                             |                                                                                          */
    /*                             |   ods output observed=want;                                                              */
    /*                             |   proc corresp data=sd1.have                                                             */
    /*                             |      oserved dim=1 cross=col;                                                            */
    /*                             |       table cat,favor year;                                                              */
    /*                             |       weight pct;                                                                        */
    /*                             |   run;quit;                                                                              */
    /*                             |                                                                                          */
    /*********************************|****************************************************************************************/


    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     informat cat favor $4.;
     input CAT YEAR PCT FAVOR;
    cards;
    A 2002 36 Medi
    B 2002 36 Bad
    B 2001 71 Good
    B 2002 60 Good
    B 1999 33 Medi
    B 2001 37 Medi
    C 1999 80 Good
    C 2002 70 Good
    C 2001 38 Medi
    C 2002 37 Medi
    D 2001 68 Good
    D 2002 58 Good
    D 2002 48 Medi
    E 1998 29 Bad
    E 2001 30 Bad
    E 2002 67 Good
    F 1999 44 Good
    H 2001 88 Good
    I 2002 46 Bad
    I 2002 65 Good
    J 1999 86 Good
    K 2002 33 Bad
    K 1999 80 Good
    K 2002 35 Medi
    M 1998 29 Bad
    M 1998 69 Good
    N 2001 20 Bad
    N 1998 75 Good
    N 2001 80 Good
    O 1998 13 Bad
    P 1998 38 Bad
    P 1999 67 Good
    P 2001 31 Medi
    P 2002 34 Medi
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  CAT    FAVOR    YEAR    PCT                                                                                           */
    /*                                                                                                                        */
    /*   A     Medi     2002     36                                                                                           */
    /*   B     Bad      2002     36                                                                                           */
    /*   B     Good     2001     71                                                                                           */
    /*   B     Good     2002     60                                                                                           */
    /*   B     Medi     1999     33                                                                                           */
    /*   ....                                                                                                                 */
    /*   O     Bad      1998     13                                                                                           */
    /*   P     Bad      1998     38                                                                                           */
    /*   P     Good     1999     67                                                                                           */
    /*   P     Medi     2001     31                                                                                           */
    /*   P     Medi     2002     34                                                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                                         _
    / |  ___  __ _ ___   _ __  _ __ ___   ___ | |_ _ __ __ _ _ __  ___ _ __   ___  ___  ___
    | | / __|/ _` / __| | `_ \| `__/ _ \ / __|| __| `__/ _` | `_ \/ __| `_ \ / _ \/ __|/ _ \
    | | \__ \ (_| \__ \ | |_) | | | (_) | (__ | |_| | | (_| | | | \__ \ |_) | (_) \__ \  __/
    |_| |___/\__,_|___/ | .__/|_|  \___/ \___| \__|_|  \__,_|_| |_|___/ .__/ \___/|___/\___|
                        |_|                                           |_|
    */
    proc transpose data=sd1.have
         out=want(drop=_name_)
         delimiter=_;
      by cat;
      id favor year;
      var pct;
    run;quit;

    proc print data=want split='_' /* heading=vertical */;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*        MEDI     BAD    GOOD    GOOD    MEDI    MEDI    GOOD     BAD     BAD    GOOD                                    */
    /* CAT    2002    2002    2001    2002    1999    2001    1999    1998    2001    1998                                    */
    /*                                                                                                                        */
    /*  A      36       .       .       .       .       .       .       .       .       .                                     */
    /*  B       .      36      71      60      33      37       .       .       .       .                                     */
    /*  C      37       .       .      70       .      38      80       .       .       .                                     */
    /*  D      48       .      68      58       .       .       .       .       .       .                                     */
    /*  E       .       .       .      67       .       .       .      29      30       .                                     */
    /*  F       .       .       .       .       .       .      44       .       .       .                                     */
    /*  H       .       .      88       .       .       .       .       .       .       .                                     */
    /*  I       .      46       .      65       .       .       .       .       .       .                                     */
    /*  J       .       .       .       .       .       .      86       .       .       .                                     */
    /*  K      35      33       .       .       .       .      80       .       .       .                                     */
    /*  M       .       .       .       .       .       .       .      29       .      69                                     */
    /*  N       .       .      80       .       .       .       .       .      20      75                                     */
    /*  O       .       .       .       .       .       .       .      13       .       .                                     */
    /*  P      34       .       .       .       .      31      67      38       .       .                                     */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___           _   _     _
    |___ \   _ __  | |_(_) __| |_   ___   _____ _ __ ___  ___
      __) | | `__| | __| |/ _` | | | \ \ / / _ \ `__/ __|/ _ \
     / __/  | |    | |_| | (_| | |_| |\ V /  __/ |  \__ \  __/
    |_____| |_|     \__|_|\__,_|\__, | \_/ \___|_|  |___/\___|
                                |___/
    */

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(tidyverse)
    library(haven)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    print(have)
    want<-have %>%
      arrange(
        CAT,
        factor(FAVOR, levels =
          c("Bad", "Medi", "Good")),
        YEAR
      ) %>%
      pivot_wider(
        names_from = c(FAVOR, YEAR),
        values_from = PCT,
        names_sep = "_"
      )
    print(want)
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want split='_' width=min;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* R                                                                                                                      */
    /*                                                                                                                        */
    /*  CAT   Medi_2002 Bad_2002 Medi_1999 Medi_2001 Good_2001 Good_2002 Good_1999                                            */
    /*  <chr>     <dbl>    <dbl>     <dbl>     <dbl>     <dbl>     <dbl>     <dbl>                                            */
    /*  A            36       NA        NA        NA        NA        NA        NA                                            */
    /*  B            NA       36        33        37        71        60        NA                                            */
    /*  C            37       NA        NA        38        NA        70        80                                            */
    /*  D            48       NA        NA        NA        68        58        NA                                            */
    /*  E            NA       NA        NA        NA        NA        67        NA                                            */
    /*  F            NA       NA        NA        NA        NA        NA        44                                            */
    /*  H            NA       NA        NA        NA        88        NA        NA                                            */
    /*  I            NA       46        NA        NA        NA        65        NA                                            */
    /*  J            NA       NA        NA        NA        NA        NA        86                                            */
    /*  K            35       33        NA        NA        NA        NA        80                                            */
    /*  M            NA       NA        NA        NA        NA        NA        NA                                            */
    /*  N            NA       NA        NA        NA        80        NA        NA                                            */
    /*  O            NA       NA        NA        NA        NA        NA        NA                                            */
    /*  P            34       NA        NA        31        NA        NA        67                                            */
    /*                                                                                                                        */
    /* SAS                                                                                                                    */
    /*                                                                                                                        */
    /*        MEDI     BAD    MEDI    MEDI    GOOD    GOOD    GOOD     BAD     BAD    GOOD                                    */
    /* CAT    2002    2002    1999    2001    2001    2002    1999    1998    2001    1998                                    */
    /*                                                                                                                        */
    /*  A      36       .       .       .       .       .       .       .       .       .                                     */
    /*  B       .      36      33      37      71      60       .       .       .       .                                     */
    /*  C      37       .       .      38       .      70      80       .       .       .                                     */
    /*  D      48       .       .       .      68      58       .       .       .       .                                     */
    /*  E       .       .       .       .       .      67       .      29      30       .                                     */
    /*  F       .       .       .       .       .       .      44       .       .       .                                     */
    /*  H       .       .       .       .      88       .       .       .       .       .                                     */
    /*  I       .      46       .       .       .      65       .       .       .       .                                     */
    /*  J       .       .       .       .       .       .      86       .       .       .                                     */
    /*  K      35      33       .       .       .       .      80       .       .       .                                     */
    /*  M       .       .       .       .       .       .       .      29       .      69                                     */
    /*  N       .       .       .       .      80       .       .       .      20      75                                     */
    /*  O       .       .       .       .       .       .       .      13       .       .                                     */
    /*  P      34       .       .      31       .       .      67      38       .       .                                     */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____                             _
    |___ /   ___  __ _ ___   ___  __ _| |
      |_ \  / __|/ _` / __| / __|/ _` | |
     ___) | \__ \ (_| \__ \ \__ \ (_| | |
    |____/  |___/\__,_|___/ |___/\__, |_|
                                    |_|
    */

    /*--- GENERATE SQL CODE SEGMENTS ---*/

    proc sql;
      create
        view compound as
      select
        cat
       ,catx('_',favor,year) as fvyr
       ,pct
      from
        sd1.have
    ;quit;

    proc sql;
      select
         distinct fvyr
      into
         :fvyr1-
      from
         compound
    ;quit;

    %let fvyrn=&sqlobs;

    %put &=fvyr1;
    %put &=fvyr3;
    %put &=fvyrn;

    FVYR1=Bad_1998
    FVYR3=Bad_2002
    FVYRN=10

    data _null_;
      %do_over(fvyr,phrase=%str(
         put ",max(case when fvyr='?' then pct else . end) as ?" ;
         ));
     run;quit;

    /*----
    ,max(case when fvyr='Bad_1998'  then pct  else . end) as Bad_1998
    ,max(case when fvyr='Bad_2001'  then pct  else . end) as Bad_2001
    ,max(case when fvyr='Bad_2002'  then pct  else . end) as Bad_2002
    ,max(case when fvyr='Good_1998' then pct  else . end) as Good_1998
    ,max(case when fvyr='Good_1999' then pct  else . end) as Good_1999
    ,max(case when fvyr='Good_2001' then pct  else . end) as Good_2001
    ,max(case when fvyr='Good_2002' then pct  else . end) as Good_2002
    ,max(case when fvyr='Medi_1999' then pct  else . end) as Medi_1999
    ,max(case when fvyr='Medi_2001' then pct  else . end) as Medi_2001
    ,max(case when fvyr='Medi_2002' then pct  else . end) as Medi_2002
    ----*/

    /*---- FINAL WORKING CODE ----*/

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    proc sql;
      create
         table want as
      select
         cat
        ,max(case when fvyr='Bad_1998'  then pct  else . end) as Bad_1998
        ,max(case when fvyr='Bad_2001'  then pct  else . end) as Bad_2001
        ,max(case when fvyr='Bad_2002'  then pct  else . end) as Bad_2002
        ,max(case when fvyr='Good_1998' then pct  else . end) as Good_1998
        ,max(case when fvyr='Good_1999' then pct  else . end) as Good_1999
        ,max(case when fvyr='Good_2001' then pct  else . end) as Good_2001
        ,max(case when fvyr='Good_2002' then pct  else . end) as Good_2002
        ,max(case when fvyr='Medi_1999' then pct  else . end) as Medi_1999
        ,max(case when fvyr='Medi_2001' then pct  else . end) as Medi_2001
        ,max(case when fvyr='Medi_2002' then pct  else . end) as Medi_2002
      from
         compound
      group
         by cat
    ;quit;

    proc print data=want split='_' width=min;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*         BAD     BAD     BAD    GOOD    GOOD    GOOD    GOOD    MEDI    MEDI    MEDI                                    */
    /* CAT    1998    2001    2002    1998    1999    2001    2002    1999    2001    2002                                    */
    /*                                                                                                                        */
    /*  A       .       .       .       .       .       .       .       .       .      36                                     */
    /*  B       .       .      36       .       .      71      60      33      37       .                                     */
    /*  C       .       .       .       .      80       .      70       .      38      37                                     */
    /*  D       .       .       .       .       .      68      58       .       .      48                                     */
    /*  E      29      30       .       .       .       .      67       .       .       .                                     */
    /*  F       .       .       .       .      44       .       .       .       .       .                                     */
    /*  H       .       .       .       .       .      88       .       .       .       .                                     */
    /*  I       .       .      46       .       .       .      65       .       .       .                                     */
    /*  J       .       .       .       .      86       .       .       .       .       .                                     */
    /*  K       .       .      33       .      80       .       .       .       .      35                                     */
    /*  M      29       .       .      69       .       .       .       .       .       .                                     */
    /*  N       .      20       .      75       .      80       .       .       .       .                                     */
    /*  O      13       .       .       .       .       .       .       .       .       .                                     */
    /*  P      38       .       .       .      67       .       .       .      31      34                                     */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _                      _
    | || |    _ __   ___  __ _| |
    | || |_  | `__| / __|/ _` | |
    |__   _| | |    \__ \ (_| | |
       |_|   |_|    |___/\__, |_|
                            |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source("c:/oto/fn_tosas9x.R")
    have<-read_sas("d:/sd1/have.sas7bdat")
    want<-sqldf('
       with
          compound as (
       select
          cat
         ,favor||"_"||cast(year as integer) as fvyr
         ,pct
       from
          have )
       select
         cat
        ,max(case when fvyr="Bad_1998"  then pct  else NULL end) as Bad_1998
        ,max(case when fvyr="Bad_2001"  then pct  else NULL end) as Bad_2001
        ,max(case when fvyr="Bad_2002"  then pct  else NULL end) as Bad_2002
        ,max(case when fvyr="Good_1998" then pct  else NULL end) as Good_1998
        ,max(case when fvyr="Good_1999" then pct  else NULL end) as Good_1999
        ,max(case when fvyr="Good_2001" then pct  else NULL end) as Good_2001
        ,max(case when fvyr="Good_2002" then pct  else NULL end) as Good_2002
        ,max(case when fvyr="Medi_1999" then pct  else NULL end) as Medi_1999
        ,max(case when fvyr="Medi_2001" then pct  else NULL end) as Medi_2001
        ,max(case when fvyr="Medi_2002" then pct  else NULL end) as Medi_2002
       from
         compound
       group
         by cat
       ')
    print(want)
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want split='_';
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  R                                                                                                                     */
    /*                                                                                                                        */
    /*   cat Bad_1998 Bad_2001 Bad_2002 Good_1998 Good_1999 Good_2001 Good_2002 Medi_1999 Medi_2001 Medi_2002                 */
    /*     A       NA       NA       NA        NA        NA        NA        NA        NA        NA        36                 */
    /*     B       NA       NA       36        NA        NA        71        60        33        37        NA                 */
    /*     C       NA       NA       NA        NA        80        NA        70        NA        38        37                 */
    /*     D       NA       NA       NA        NA        NA        68        58        NA        NA        48                 */
    /*     E       29       30       NA        NA        NA        NA        67        NA        NA        NA                 */
    /*     F       NA       NA       NA        NA        44        NA        NA        NA        NA        NA                 */
    /*     H       NA       NA       NA        NA        NA        88        NA        NA        NA        NA                 */
    /*     I       NA       NA       46        NA        NA        NA        65        NA        NA        NA                 */
    /*     J       NA       NA       NA        NA        86        NA        NA        NA        NA        NA                 */
    /*     K       NA       NA       33        NA        80        NA        NA        NA        NA        35                 */
    /*     M       29       NA       NA        69        NA        NA        NA        NA        NA        NA                 */
    /*     N       NA       20       NA        75        NA        80        NA        NA        NA        NA                 */
    /*     O       13       NA       NA        NA        NA        NA        NA        NA        NA        NA                 */
    /*     P       38       NA       NA        NA        67        NA        NA        NA        31        34                 */
    /*                                                                                                                        */
    /*  SAS                                                                                                                   */
    /*                                                                                                                        */
    /*                     BAD     BAD     BAD    GOOD    GOOD    GOOD    GOOD    MEDI    MEDI    MEDI                        */
    /* ROWNAMES    CAT    1998    2001    2002    1998    1999    2001    2002    1999    2001    2002                        */
    /*                                                                                                                        */
    /*     1        A       .       .       .       .       .       .       .       .       .      36                         */
    /*     2        B       .       .      36       .       .      71      60      33      37       .                         */
    /*     3        C       .       .       .       .      80       .      70       .      38      37                         */
    /*     4        D       .       .       .       .       .      68      58       .       .      48                         */
    /*     5        E      29      30       .       .       .       .      67       .       .       .                         */
    /*     6        F       .       .       .       .      44       .       .       .       .       .                         */
    /*     7        H       .       .       .       .       .      88       .       .       .       .                         */
    /*     8        I       .       .      46       .       .       .      65       .       .       .                         */
    /*     9        J       .       .       .       .      86       .       .       .       .       .                         */
    /*    10        K       .       .      33       .      80       .       .       .       .      35                         */
    /*    11        M      29       .       .      69       .       .       .       .       .       .                         */
    /*    12        N       .      20       .      75       .      80       .       .       .       .                         */
    /*    13        O      13       .       .       .       .       .       .       .       .       .                         */
    /*    14        P      38       .       .       .      67       .       .       .      31      34                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

     /*___                _   _                             _
    | ___|   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
    |___ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql('''
       with
          compound as (
       select
          cat
         ,favor||"_"||cast(year as integer) as fvyr
         ,pct
       from
          have )
       select
         cat
        ,max(case when fvyr="Bad_1998"  then pct  else NULL end) as Bad_1998
        ,max(case when fvyr="Bad_2001"  then pct  else NULL end) as Bad_2001
        ,max(case when fvyr="Bad_2002"  then pct  else NULL end) as Bad_2002
        ,max(case when fvyr="Good_1998" then pct  else NULL end) as Good_1998
        ,max(case when fvyr="Good_1999" then pct  else NULL end) as Good_1999
        ,max(case when fvyr="Good_2001" then pct  else NULL end) as Good_2001
        ,max(case when fvyr="Good_2002" then pct  else NULL end) as Good_2002
        ,max(case when fvyr="Medi_1999" then pct  else NULL end) as Medi_1999
        ,max(case when fvyr="Medi_2001" then pct  else NULL end) as Medi_2001
        ,max(case when fvyr="Medi_2002" then pct  else NULL end) as Medi_2002
       from
         compound
       group
         by cat
       ''');
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant split='_';
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* PYTHON                                                                                                                 */
    /*                                                                                                                        */
    /*     cat  Bad_1998  Bad_2001  ...  Medi_1999  Medi_2001  Medi_2002                                                      */
    /*  0    A       NaN       NaN  ...        NaN        NaN       36.0                                                      */
    /*  1    B       NaN       NaN  ...       33.0       37.0        NaN                                                      */
    /*  2    C       NaN       NaN  ...        NaN       38.0       37.0                                                      */
    /*  3    D       NaN       NaN  ...        NaN        NaN       48.0                                                      */
    /*  4    E      29.0      30.0  ...        NaN        NaN        NaN                                                      */
    /*  5    F       NaN       NaN  ...        NaN        NaN        NaN                                                      */
    /*  6    H       NaN       NaN  ...        NaN        NaN        NaN                                                      */
    /*  7    I       NaN       NaN  ...        NaN        NaN        NaN                                                      */
    /*  8    J       NaN       NaN  ...        NaN        NaN        NaN                                                      */
    /*  9    K       NaN       NaN  ...        NaN        NaN       35.0                                                      */
    /*  10   M      29.0       NaN  ...        NaN        NaN        NaN                                                      */
    /*  11   N       NaN      20.0  ...        NaN        NaN        NaN                                                      */
    /*  12   O      13.0       NaN  ...        NaN        NaN        NaN                                                      */
    /*  13   P      38.0       NaN  ...        NaN       31.0       34.0                                                      */
    /*                                                                                                                        */
    /*  SAS                                                                                                                   */
    /*                                                                                                                        */
    /*          BAD     BAD     BAD    GOOD    GOOD    GOOD    GOOD    MEDI    MEDI    MEDI                                   */
    /*  CAT    1998    2001    2002    1998    1999    2001    2002    1999    2001    2002                                   */
    /*                                                                                                                        */
    /*   A       .       .       .       .       .       .       .       .       .      36                                    */
    /*   B       .       .      36       .       .      71      60      33      37       .                                    */
    /*   C       .       .       .       .      80       .      70       .      38      37                                    */
    /*   D       .       .       .       .       .      68      58       .       .      48                                    */
    /*   E      29      30       .       .       .       .      67       .       .       .                                    */
    /*   F       .       .       .       .      44       .       .       .       .       .                                    */
    /*   H       .       .       .       .       .      88       .       .       .       .                                    */
    /*   I       .       .      46       .       .       .      65       .       .       .                                    */
    /*   J       .       .       .       .      86       .       .       .       .       .                                    */
    /*   K       .       .      33       .      80       .       .       .       .      35                                    */
    /*   M      29       .       .      69       .       .       .       .       .       .                                    */
    /*   N       .      20       .      75       .      80       .       .       .       .                                    */
    /*   O      13       .       .       .       .       .       .       .       .       .                                    */
    /*   P      38       .       .       .      67       .       .       .      31      34                                    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*__                       _             _
     / /_     _____  _____ ___| |  ___  __ _| |
    | `_ \   / _ \ \/ / __/ _ \ | / __|/ _` | |
    | (_) | |  __/>  < (_|  __/ | \__ \ (_| | |
     \___/   \___/_/\_\___\___|_| |___/\__, |_|
                         _                 |_|       _   _                   _
      ___ _ __ ___  __ _| |_ ___    _____  _____ ___| | (_)_ __  _ __  _   _| |_
     / __| `__/ _ \/ _` | __/ _ \  / _ \ \/ / __/ _ \ | | | `_ \| `_ \| | | | __|
    | (__| | |  __/ (_| | ||  __/ |  __/>  < (_|  __/ | | | | | | |_) | |_| | |_
     \___|_|  \___|\__,_|\__\___|  \___/_/\_\___\___|_| |_|_| |_| .__/ \__,_|\__|
                                                                |_|
    */

    %utlfkil(d:/xls/wantxl.xlsx);

    %utl_rbeginx;
    parmcards4;
    library(openxlsx)
    library(sqldf)
    library(haven)
    have<-read_sas("d:/sd1/have.sas7bdat")
    wb <- createWorkbook()
    addWorksheet(wb, "have")
    writeData(wb, sheet = "have", x = have)
    saveWorkbook(
        wb
       ,"d:/xls/wantxl.xlsx"
       ,overwrite=TRUE)
    ;;;;
    %utl_rendx;

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(openxlsx)
    library(sqldf)
     wb<-loadWorkbook("d:/xls/wantxl.xlsx")
     have<-read.xlsx(wb,"have")
     addWorksheet(wb, "want")
     want<-sqldf('
       with
          compound as (
       select
          cat
         ,favor||"_"||cast(year as integer) as fvyr
         ,pct
       from
          have )
       select
         cat
        ,max(case when fvyr="Bad_1998"  then pct  else NULL end) as Bad_1998
        ,max(case when fvyr="Bad_2001"  then pct  else NULL end) as Bad_2001
        ,max(case when fvyr="Bad_2002"  then pct  else NULL end) as Bad_2002
        ,max(case when fvyr="Good_1998" then pct  else NULL end) as Good_1998
        ,max(case when fvyr="Good_1999" then pct  else NULL end) as Good_1999
        ,max(case when fvyr="Good_2001" then pct  else NULL end) as Good_2001
        ,max(case when fvyr="Good_2002" then pct  else NULL end) as Good_2002
        ,max(case when fvyr="Medi_1999" then pct  else NULL end) as Medi_1999
        ,max(case when fvyr="Medi_2001" then pct  else NULL end) as Medi_2001
        ,max(case when fvyr="Medi_2002" then pct  else NULL end) as Medi_2002
       from
         compound
       group
         by cat
      ')
     writeData(wb,sheet="want",x=want)
     saveWorkbook(
         wb
        ,"d:/xls/wantxl.xlsx"
        ,overwrite=TRUE)
    ;;;;
    %utl_rendx;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  d:/xls/wantxl.xlsx  aheet=WANT                                                                                        */
    /*                                                                                                                        */
    /*  --------------------------                                                                                            */
    /*  | A1   | f  fx  |   CAT  |                                                                                            */
    /*  -----------------------------------------------------------------------------------------------------------           */
    /*  [ ]| A |    B   |    C   |    E   |    F    |    G    |    H    |    I    |    J    |    K    |    L    |             */
    /*  ---------------------------------------------------------------------------------------------------------             */
    /*   1 |CAT|Bad_1998|Bad_2001|Bad_2002|Good_1998|Good_1999|Good_2001|Good_2002|Medi_1999|Medi_2001|Medi_2002|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   2 |A  |       .|       .|       .|        .|        .|        .|        .|        .|        .|      36 |             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   3 |B  |       .|       .|     36 |        .|        .|      71 |      60 |      33 |      37 |        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   4 |C  |       .|       .|       .|        .|      80 |        .|      70 |        .|      38 |      37 |             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   5 |D  |       .|       .|       .|        .|        .|      68 |      58 |        .|        .|      48 |             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   6 |E  |     29 |     30 |       .|        .|        .|        .|      67 |        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   7 |F  |       .|       .|       .|        .|      44 |        .|        .|        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   8 |H  |       .|       .|       .|        .|        .|      88 |        .|        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*   9 |I  |       .|       .|     46 |        .|        .|        .|      65 |        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*  10 |J  |       .|       .|       .|        .|      86 |        .|        .|        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*  11 |K  |       .|       .|     33 |        .|      80 |        .|        .|        .|        .|      35 |             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*  12 |M  |     29 |       .|       .|      69 |        .|        .|        .|        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*  13 |N  |       .|     20 |       .|      75 |        .|      80 |        .|        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*  14 |O  |     13 |       .|       .|        .|        .|        .|        .|        .|        .|        .|             */
    /*  -- |---+--------+--------+--------+---------+---------+---------+---------+---------+---------+---------|             */
    /*  15 |P  |     38 |       .|       .|        .|      67 |        .|        .|        .|      31 |      34 |             */
    /*  ---------------------------------------------------------------------------------------------------------             */
    /*  [WANT]                                                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____
    |___  |  ___  __ _ ___    ___ ___  _ __ _ __ ___  ___ _ __
       / /  / __|/ _` / __|  / __/ _ \| `__| `__/ _ \/ __| `_ \
      / /   \__ \ (_| \__ \ | (_| (_) | |  | | |  __/\__ \ |_) |
     /_/    |___/\__,_|___/  \___\___/|_|  |_|  \___||___/ .__/
                                                         |_|
    */


    ods exclude all;

    ods output observed=want;
    proc corresp data=sd1.have
       oserved dim=1 cross=col;
        table cat,favor year;
        weight pct;
    run;quit;

    ods select all;

    proc print data=want split='_' width=min;
    run;quit;


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*            Bad      Bad      Bad      Good      Good      Good      Good      Medi      Medi      Medi                 */
    /*  LABEL    1998     2001     2002      1998      1999      2001      2002      1999      2001      2002     Sum         */
    /*                                                                                                                        */
    /*   A          0       0         0        0         0         0         0         0         0        36        36        */
    /*   B          0       0        36        0         0        71        60        33        37         0       237        */
    /*   C          0       0         0        0        80         0        70         0        38        37       225        */
    /*   D          0       0         0        0         0        68        58         0         0        48       174        */
    /*   E         29      30         0        0         0         0        67         0         0         0       126        */
    /*   F          0       0         0        0        44         0         0         0         0         0        44        */
    /*   H          0       0         0        0         0        88         0         0         0         0        88        */
    /*   I          0       0        46        0         0         0        65         0         0         0       111        */
    /*   J          0       0         0        0        86         0         0         0         0         0        86        */
    /*   K          0       0        33        0        80         0         0         0         0        35       148        */
    /*   M         29       0         0       69         0         0         0         0         0         0        98        */
    /*   N          0      20         0       75         0        80         0         0         0         0       175        */
    /*   O         13       0         0        0         0         0         0         0         0         0        13        */
    /*   P         38       0         0        0        67         0         0         0        31        34       170        */
    /*                                                                                                                        */
    /*   Sum      109      50       115      144       357       307       320        33       106       190      1731        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
