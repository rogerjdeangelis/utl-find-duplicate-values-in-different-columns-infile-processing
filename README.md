# utl-find-duplicate-values-in-different-columns-infile-processing
Find duplicate values in different columns infile processing
    Find duplicate values in different columns infile processing

    github
    https://tinyurl.com/ya6l7mn4
    https://github.com/rogerjdeangelis/utl-find-duplicate-values-in-different-columns-infile-processing

    SAS Forum
    https://tinyurl.com/yarzoxzs
    https://communities.sas.com/t5/SAS-Programming/how-to-find-duplicate-values-in-different-variables/m-p/642888

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    filename ft15f001 "d:/txt/dedup.txt";
    parmcards4;
    cat    human  cat
    dog    bird   human
    mouse  fish   horse
    human  lizard rabbit
    ;;;;
    run;quit;


    d:/txt/dedup.txt

    cat    human  cat
    dog    bird   human
    mouse  fish   horse
    human  lizard rabbit


    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;                                    | RULES (find dups)
                                         |
    Up to 40 obs from WANT total obs=5   |
                                         |
      ROW   COL      WORD                |
                                         |  Cat appears on week1 and week3 of row 1
       1   week1     cat                 |
       1   week3     cat                 |
                                         |
       1   week2     human               |
       2   week3     human               |
       4   week1     human               |

    *
     _ __  _ __ ___   ___ ___  ___ ___
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    ;

    data havNrm;
         retain col "     " row 1 ;
         infile "d:/txt/dedup.txt" line=lyn ;
         input word$ @@;
         row = row + (lyn=2);
         col=cats('week',mod(_n_-1,3) + 1);
    run;quit;

    proc sort data=havnrm out=want nonuniquekey;
    by word;
    run;quit;


