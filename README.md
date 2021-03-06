# utl_nice_example_of_the_misunderstood_retain_issue_with_datastep_merg
Nice example of the misunderstood retain issue with datastep merge.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.

    Nice example of the misunderstood retain issue with datastep merge

    Same result in WPS and SAS

    github
    https://tinyurl.com/yb3xatbj
    https://github.com/rogerjdeangelis/utl_nice_example_of_the_misunderstood_retain_issue_with_datastep_merg

    see
    https://tinyurl.com/y9eteet6
    https://communities.sas.com/t5/Base-SAS-Programming/create-xyz-table/m-p/478567

    K Sharp profile
    https://communities.sas.com/t5/user/viewprofilepage/user-id/18408

    INPUT
    =====

       When I merge Data A with data B Iget

          DATA A     DATA B   |   PROBLEM     |     WANT
                              |               |
          X    Y      X    Z  |  X   Y    Z   |  X    Y    Z
                              |               |
          1    2      1    4  |  1   2    4   |  1    2    4
          1    3      1    5  |  1   3    5   |  1    3    5
          2    4      1    6  |  1   3**  6   |  1    .    6
          2    5      2    3  |  2   4    3   |  2    4    3
          2    9      2    7  |  2   5    7   |  2    5    7
                              |  2   9    7** |  2    9    .

                                * should be missing Y is retained
                                * should be missing Z is retained

    PROCESS
    =======

      data want;
         merge one two;
         by x;
         output;
         call missing(of _all_);
      run;quit;


    OUTPUT
    ======

     WORK.WANT total obs=6

        X    Y    Z

        1    2    4
        1    3    5
        1    .    6
        2    4    3
        2    5    7
        2    9    .

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;


    data one;
    input x y;
    cards;
    1 2
    1 3
    2 4
    2 5
    2 9
    ;;;;
    run;

    data two;
    input x z;
    cards4;
    1 4
    1 5
    1 6
    2 3
    2 7
    ;;;;
    run;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    SAS  see process

    %utl_submit_wps64('
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    data want;
       merge wrk.one wrk.two;
       by x;
       output;
       call missing(of _all_);
    run;quit;
    proc print;
    run;quit;
    ');

