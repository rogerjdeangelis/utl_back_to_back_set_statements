# utl_back_to_back_set_statements
How SAS/WPS interprets back to back set commands

    ```  SAS L: Properities you shoud know about multiple back to back set commands ;  ```
    ```    ```
    ```    WORKING CODE  ```
    ```    ```
    ```      1  * 2 obs out havOne determines length and havTwo overwrites havOne;  ```
    ```         * dats sets are not interleaved;  ```
    ```    ```
    ```         set havOne(obs=2)  ```
    ```         set havTwo(obs=2)  ```
    ```    ```
    ```         Middle Observation(1 ) of set_set - Total Obs 2  ```
    ```    ```
    ```          -- CHARACTER --  ```
    ```                              Truncated  ```
    ```                Type Length   Value  ```
    ```    ```
    ```         ID       C    1       Y  ```
    ```         NAME     C    1       A  ```
    ```    ```
    ```         Up to 40 obs WORK.SET_SET total obs=2  ```
    ```    ```
    ```               Both Truncated  ```
    ```         Obs    ID    NAME  ```
    ```    ```
    ```          1     Y      A  ```
    ```          2     Y      B  ```
    ```    ```
    ```         same as  ```
    ```            merge havOne(obs=2) havTwo(obs=2)  ```
    ```    ```
    ```      2  * 4 obs out. Interleaves records but still uses length from first set;  ```
    ```    ```
    ```         set havOne(obs=2);output;  ```
    ```         set havTwo(obs=2);output;  ```
    ```    ```
    ```         Up to 40 obs from set_outs total obs=4  ```
    ```    ```
    ```         Obs    ID    NAMEITruncated)  ```
    ```    ```
    ```          1     x      A    from havOne  ```
    ```          2     Y      A    from havTwo  ```
    ```          3     X      x    from havOne  ```
    ```          4     Y      B    from havTwo  ```
    ```    ```
    ```      3  * 2 obs out havOne determines length but havTwo overwrites havOne.  ```
    ```         * stops when either dataset runs out of observations;  ```
    ```    ```
    ```         set havOne(obs=3)  ```
    ```         set havTwo(obs=2)  ```
    ```    ```
    ```    ```
    ```      4  * 5 obs out. havOne determines length but havTwo overwrites havOne.  ```
    ```         * stops when either dataset runs out of observations;  ```
    ```    ```
    ```         set havOne(obs=3);output;  ```
    ```         set havTwo(obs=2);output;  ```
    ```    ```
    ```  see  ```
    ```  https://goo.gl/dmPUqo  ```
    ```  https://communities.sas.com/t5/Base-SAS-Programming/  ```
    ```  i-have-a-problem-of-combining-2-datasets-in-SAS/m-p/394414  ```
    ```    ```
    ```  PGStats profile  ```
    ```  https://communities.sas.com/t5/user/viewprofilepage/user-id/462  ```
    ```    ```
    ```  HAVE  ```
    ```  ====  ```
    ```    ```
    ```  WORK.HAVONE total obs=3  ```
    ```    ```
    ```  Obs    ID    NAME  ```
    ```    ```
    ```   1     x      A  ```
    ```   2     X      x  ```
    ```   3     X      P  ```
    ```    ```
    ```  WORK.HAVTWO total obs=2  ```
    ```    ```
    ```  Obs    ID    NAME  ```
    ```    ```
    ```   1     Y1    AAA  ```
    ```   2     Y2    BBB  ```
    ```    ```
    ```  WANT  ```
    ```    ```
    ```    see below  ```
    ```    ```
    ```    ```
    ```  *                _              _       _  ```
    ```   _ __ ___   __ _| | _____    __| | __ _| |_ __ _  ```
    ```  | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |  ```
    ```  | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |  ```
    ```  |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|  ```
    ```    ```
    ```  ;  ```
    ```    ```
    ```  data havOne;  ```
    ```    length id name $1;  ```
    ```    input id$ name$;  ```
    ```  cards4;  ```
    ```  x1 ABC  ```
    ```  X2 xyz  ```
    ```  X3 PQR  ```
    ```  ;;;;  ```
    ```  run;quit;  ```
    ```    ```
    ```  /*  ```
    ```  HavOne  ```
    ```    ```
    ```   -- CHARACTER --  ```
    ```                       Truncated  ```
    ```         Type Length   Value  ```
    ```    ```
    ```  ID       C    1       Y  ```
    ```  NAME     C    1       A  ```
    ```  */  ```
    ```    ```
    ```  data havTwo;  ```
    ```    length id name $5;  ```
    ```    input id$ name$;  ```
    ```  cards4;  ```
    ```  Y1 AAA  ```
    ```  Y2 BBB  ```
    ```  ;;;;  ```
    ```  run;quit;  ```
    ```    ```
    ```  /*  ```
    ```  havTwo  ```
    ```    ```
    ```   -- CHARACTER --  ```
    ```  ID      C    5       Y1  ```
    ```  NAME    C    5       AAA  ```
    ```  */  ```
    ```    ```
    ```  *                     _    _  ```
    ```  __  ___ __ ___  _ __ | |  / |  ```
    ```  \ \/ / '_ ` _ \| '_ \| |  | |  ```
    ```   >  <| | | | | | |_) | |  | |  ```
    ```  /_/\_\_| |_| |_| .__/|_|  |_|  ```
    ```                 |_|  ```
    ```  ;  ```
    ```    ```
    ```  data set_set;  ```
    ```    set havOne(obs=2);  ```
    ```    set havTwo(obs=2);  ```
    ```  run;quit;  ```
    ```    ```
    ```  data set_set;  ```
    ```    merge havOne(obs=2)  havTwo(obs=2);  ```
    ```  run;quit;  ```
    ```    ```
    ```  WORK.SET_SET  ```
    ```    ```
    ```   -- CHARACTER --  ```
    ```                       Truncated  ```
    ```         Type Length   Value  ```
    ```    ```
    ```  ID       C    1       Y  ```
    ```  NAME     C    1       A  ```
    ```    ```
    ```  *                     _    ____  ```
    ```  __  ___ __ ___  _ __ | |  |___ \  ```
    ```  \ \/ / '_ ` _ \| '_ \| |    __) |  ```
    ```   >  <| | | | | | |_) | |   / __/  ```
    ```  /_/\_\_| |_| |_| .__/|_|  |_____|  ```
    ```                 |_|  ```
    ```  ;  ```
    ```    ```
    ```  data set_outs;  ```
    ```    set havOne(obs=2); output;  ```
    ```    set havTwo(obs=2); output;  ```
    ```  run;quit;  ```
    ```    ```
    ```  /*  ```
    ```  Up to 40 obs from set_outs total obs=4  ```
    ```    ```
    ```  Obs    ID    NAME  ```
    ```    ```
    ```   1     x      A  ```
    ```   2     Y      A  ```
    ```   3     X      x  ```
    ```   4     Y      B  ```
    ```  */  ```
    ```    ```
    ```  *                     _    _____  ```
    ```  __  ___ __ ___  _ __ | |  |___ /  ```
    ```  \ \/ / '_ ` _ \| '_ \| |    |_ \  ```
    ```   >  <| | | | | | |_) | |   ___) |  ```
    ```  /_/\_\_| |_| |_| .__/|_|  |____/  ```
    ```                 |_|  ```
    ```  ;  ```
    ```    ```
    ```  data set_outs;  ```
    ```    set havOne(obs=3);  ```
    ```    set havTwo(obs=2);  ```
    ```  run;quit;  ```
    ```    ```
    ```  /*  ```
    ```  Up to 40 obs WORK.SET_OUTS total obs=2  ```
    ```    ```
    ```  Obs    ID    NAME  ```
    ```    ```
    ```   1     Y      A  ```
    ```   2     Y      B  ```
    ```  */  ```
    ```    ```
    ```  *                     _    _  _  ```
    ```  __  ___ __ ___  _ __ | |  | || |  ```
    ```  \ \/ / '_ ` _ \| '_ \| |  | || |_  ```
    ```   >  <| | | | | | |_) | |  |__   _|  ```
    ```  /_/\_\_| |_| |_| .__/|_|     |_|  ```
    ```                 |_|  ```
    ```  ;  ```
    ```    ```
    ```  data set_outs;  ```
    ```    set havOne(obs=3);output;  ```
    ```    set havTwo(obs=2);output;  ```
    ```  run;quit;  ```
    ```    ```
    ```    ```
    ```  /*  ```
    ```  Up to 40 obs WORK.SET_OUTS total obs=5  ```
    ```    ```
    ```  Obs    ID    NAME  ```
    ```    ```
    ```   1     x      A    from havOne  ```
    ```   2     Y      A    from havTwo  ```
    ```    ```
    ```   3     X      x    from havOne  ```
    ```   4     Y      B    from havTwo  ```
    ```    ```
    ```   5     X      P    from havOne (non-matching last ob from havOne);  ```
    ```  */  ```
    ```    ```
    ```    ```
    ```  *                     _    ____  ```
    ```  __  ___ __ ___  _ __ | |  | ___|  ```
    ```  \ \/ / '_ ` _ \| '_ \| |  |___ \  ```
    ```   >  <| | | | | | |_) | |   ___) |  ```
    ```  /_/\_\_| |_| |_| .__/|_|  |____/  ```
    ```                 |_|  ```
    ```  ;  ```
    ```    ```
    ```    ```
    ```  data set_outs;  ```
    ```    set havOne(obs=3)  ```
    ```        havTwo(obs=2);  ```
    ```  run;quit;  ```
    ```    ```
    ```  /*  ```
    ```  5 obs out not interleaved length from first dataset  ```
    ```    ```
    ```  Up to 40 obs from set_outs total obs=5  ```
    ```    ```
    ```  Obs    ID    NAME  ```
    ```    ```
    ```   1     x      A   first dataset  ```
    ```   2     X      x  ```
    ```   3     X      P  ```
    ```    ```
    ```   4     Y      A   Truncated second dataset  ```
    ```   5     Y      B  ```
    ```  */  ```
    ```    ```
    ```    ```
