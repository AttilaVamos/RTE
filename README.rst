Overview of Regression Suite usage
==================================

To use Regression Suite change directory to HPCC-Platform/testing/regress subdirectory.

Regression Suite requires Python environment version >=2.6.6 and < 3.x

Global parameters of Regression Suite:
--------------------------------------

Command:
 
    ./ecl-test <-h|--help>

Result:

|
|       usage: ecl-test [-h] [--config [CONFIG]]
|                       [--loglevel [{info,debug}]]
|                       [--suiteDir [SUITEDIR]]
|                       [--timeout [TIMEOUT]]
|                       [--keyDir [KEYDIR]]
|                       [--ignoreResult]
|                       [-X name1=value1[,name2=value2...]]
|                       [-f optionA=valueA[,optionB=valueB...]]
|                       [--pq threadNumber]
|                       [--noversion]
|                       [--runclass class[,class,...]]
|                       [--excludeclass class[,class,...]]
|                       [--handleEclccWarningFile]
|                       [--flushDiskCache]
|                       {list,setup,run,query} ...
| 
|       HPCC Platform Regression suite
| 
|       positional arguments:
|          {list,setup,run,query} sub-command help
|            list                 list help
|            setup                setup help
|            run                  run help
|            query                query help
|
|       optional arguments:
|        -h, --help               Show this help message and exit
|        --config [CONFIG]        Config file to use. Default: ecl-test.json.
|        --loglevel [{info,debug}]
|                                 Set the log level. Use debug for more detailed logfile.
|        --suiteDir [SUITEDIR], -s [SUITEDIR]
|                                 SuiteDir to use. Default value is the current directory and it can handle relative path.
|        --timeout [TIMEOUT]      Timeout for query execution in sec. Use -1 to disable timeout. Default value defined in ecl-test.json config file (see: 9.)
|        --keyDir [KEYDIR], -k [KEYDIR]
|                                 Key file directory to compare test output. Default value defined in regress.json config file.
|        --ignoreResult, -i       Completely ignore the result.
|        -X name1=value1[,name2=value2...]
|                                 Sets the stored input value (stored('name')).
|        -f optionA=valueA[,optionB=valueB...]
|                                 Set an ECL option (equivalent to #option).
|        --pq threadNumber        Parallel query execution with threadNumber threads. (If threadNumber is '-1' on a single node system then threadNumber = numberOfLocalCore * 2)
|        --noversion              Avoid version expansion of queries. Execute them as a standard test.
|        --server [networkAddress]
|                                 ESP server address. Default value (espIp) defined in ecl-test.json config file.
|        --username [username], -u [username]
|                                 Specify a username. If this appears in command line and the STDIO is a TTY like device then, the test engine displays a prompt to get user's password. 
|                                 Pipe like 'echo "<password>" \| ./elc-test run -u <username> ...' can be used to provide user's password as well.
|                                 The username and password overrides those stored in ecl-test.json config file.
|        --runclass class[,class,...], -r class[,class,...]
|                                 Run subclass(es) of the suite. Default value is 'all'
|        --excludeclass class[,class,...], -e class[,class,...]
|                                 Exclude subclass(es) of the suite. Default value is 'none'
|        --handleEclccWarningFile, -w
|                                 Create/overwrite/delete ECLCC warning file.
|        --jobnamesuffix suffix   Specify workunit job name suffix.
|        --flushDiskCache         Flush OS (Linux) Disk Cache before execute ECL code (sudo privileges needed). Ignored when --pq <n> > 1
|        --flushDiskCachePolicy flushDiskCachePolicy
|                                 Set flush disk cache policy. The default is 1 to clear before first run only. For 2 to clear before every run.
|        --runcount runcount      Execute individual test case(s) in given times. Default value is 1
|


Important!
    There is a bug in Python argparse library whichis impacts the quoted parameters. So either in -X or -f or both contains a value with space(s) inside then the whole argument should be put in double quote!

    Example: We should pass these names values pairs to set stored input values:
                param1 = 1
                param2 = A string
                param2 = Other string

    The proper ecl-test command is:
            ./ecl-test -X"param1=1,param2=A string,param3=Other String" ...

    Same format should use for -f option(s) and values. This problem doesn't impact parameters are stored in ecl-test.json config file. (See 9.)


Parameters of Regression Suite list sub-command:
------------------------------------------------

Command:

    ./ecl-test list <-h|--help>

Result:

|
|       usage: ecl-test list [-h] [--config [CONFIG]] [--loglevel [{info,debug}]]
|                            [--runclass class[,class,...]]
|                            [--excludeclass class[,class,...]]
|                            [--jobnamesuffix suffix] [--flushDiskCache] [--clusters]
|                            [--setup] [--run] [--target [target_cluster_list | all]]
|                            [--createEclRunArg]
|
|       optional arguments:
|        -h, --help               Show this help message and exit
|        --config [CONFIG]        Config file to use. Default: ecl-test.json
|        --loglevel [{info,debug}]
|                                 Set the log level. Use debug for more detailed
|                                 logfile.
|        --runclass class[,class,...], -r class[,class,...]
|                                 Run subclass(es) of the suite. Default value is 'all'
|        --excludeclass class[,class,...], -e class[,class,...]
|                                 Exclude subclass(es) of the suite. Default value is
|                                 'none'
|        --jobnamesuffix suffix
|                                 Specify workunit job name suffix.
|        --flushDiskCache         Flush OS (Linux) Disk Cache before execute ECL code
|                                 (sudo privileges needed). Ignored when --pq <n> > 1
|        --flushDiskCachePolicy flushDiskCachePolicy
|                                 Set flush disk cache policy. The default is 1 to clear before first run only. For 2 to clear before every run.
|        --runcount runcount      Execute individual test case(s) in given times. Default value is 1
|        --clusters               Print target clusters from config (ecl-test.json by
|                                 default).
|        --setup                  Print testcases executed in setup.
|        --run                    Print test cases executed in run.
|        --target [target_cluster_list | all], -t [target_cluster_list | all]
|                                 Provide target cluster(s) to list test cases. If
|                                 target = 'all' then list test cases on all clusters.
|                                 If not defined then default value(s) come from config
|                                 (ecl-test.json by default).
|        --createEclRunArg        Generate ECL tool command line.
|

Parameters of Regression Suite setup sub-command:
-------------------------------------------------

Command:

    ./ecl-test setup <-h|--help>

Result:

|
|       usage: ecl-test setup [-h] [--config [CONFIG]]
|                             [--loglevel [{info,debug}]]
|                             [--suiteDir [SUITEDIR]]
|                             [--timeout [TIMEOUT]]
|                             [--keyDir [KEYDIR]]
|                             [--ignoreResult]
|                             [-X name1=value1[,name2=value2...]]
|                             [-f optionA=valueA[,optionB=valueB...]]
|                             [--pq threadNumber]
|                             [--noversion]
|                             [--runclass class[,class,...]]
|                             [--excludeclass class[,class,...]]
|                             [--jobnamesuffix suffix] [--flushDiskCache]
|                             [--target [target_cluster_list | all]]
|                             [--handleEclccWarningFile]
|
|       optional arguments:
|        -h, --help               Show this help message and exit
|        --config [CONFIG]        Config file to use. Default: ecl-test.json.
|        --loglevel [{info,debug}]
|                                 Set the log level. Use debug for more detailed logfile.
|        --suiteDir [SUITEDIR], -s [SUITEDIR]
|                                 SuiteDir to use. Default value is the current directory and it can handle relative path.
|        --timeout [TIMEOUT]      Timeout for query execution in sec. Use -1 to disable timeout. Default value defined in ecl-test.json config file (see: 9.)
|        --keyDir [KEYDIR], -k [KEYDIR]
|                                 Key file directory to compare test output. Default value defined in regress.json config file.
|        --ignoreResult, -i       Completely ignore the result.
|        -X name1=value1[,name2=value2...]
|                                 Sets the stored input value (stored('name')).
|        -f optionA=valueA[,optionB=valueB...]
|                                 Set an ECL option (equivalent to #option).
|        --pq threadNumber        Parallel query execution with threadNumber threads. (If threadNumber is '-1' on a single node system then threadNumber = numberOfLocalCore * 2)
|        --noversion              Avoid version expansion of queries. Execute them as a standard test.
|        --server [networkAddress]
|                                 ESP server address. Default value (espIp) defined in
|                                 ecl-test.json config file.
|        --username [username], -u [username]
|                                 Specify a username. If this appears in command line and the STDIO is a TTY like device then, the test engine displays a prompt to get user's password. 
|                                 Pipe like 'echo "<password>" \| ./elc-test run -u <username> ...' can be used to provide user's password as well.
|                                 The username and password overrides those stored in ecl-test.json config file.
|        --runclass class[,class,...], -r class[,class,...]
|                                 Run subclass(es) of the suite. Default value is 'all'
|        --excludeclass class[,class,...], -e class[,class,...]
|                                 Exclude subclass(es) of the suite. Default value is 'none'
|        --jobnamesuffix suffix   Specify workunit job name suffix.
|        --flushDiskCache         Flush OS (Linux) Disk Cache before execute ECL code
|                                 (sudo privileges needed). Ignored when --pq <n> > 1
|        --flushDiskCachePolicy flushDiskCachePolicy
|                                 Set flush disk cache policy. The default is 1 to clear before first run only. For 2 to clear before every run.
|        --runcount runcount      Execute individual test case(s) in given times. Default value is 1
|        --target [target_cluster_list | all], -t [target_cluster_list | all]
|                                 Run the setup on target cluster(s). If target = 'all'
|                                 then run setup on all clusters. If not defined then
|                                 default value(s) come from config (ecl-test.json by default).
|        --handleEclccWarningFile, -w
|                                 Create/overwrite/delete ECLCC warning file
|

Parameters of Regression Suite run sub-command:
-----------------------------------------------

Command:

    ./ecl-test run <-h|--help>

Result:

|
|       usage: ecl-test run [-h][--config [CONFIG]]
|                           [--loglevel [{info,debug}]]
|                           [--suiteDir [SUITEDIR]]
|                           [--timeout [TIMEOUT]]
|                           [--keyDir [KEYDIR]]
|                           [--ignoreResult]
|                           [-X name1=value1[,name2=value2...]]
|                           [-f optionA=valueA[,optionB=valueB...]]
|                           [--pq threadNumber] [--noversion]
|                           [--server [networkAddress]] [--runclass class[,class,...]]
|                           [--excludeclass class[,class,...]]
|                           [--jobnamesuffix suffix] [--flushDiskCache]
|                           [--target [target_cluster_list | all]] [--publish]
|                           [--handleEclccWarningFile]
|
|       optional arguments:
|        -h, --help               Show this help message and exit
|        --config [CONFIG]        Config file to use. Default: ecl-test.json.
|        --loglevel [{info,debug}]
|                                 Set the log level. Use debug for more detailed logfile.
|        --suiteDir [SUITEDIR], -s [SUITEDIR]
|                                 SuiteDir to use. Default value is the current directory and it can handle relative path.
|        --timeout [TIMEOUT]      Timeout for query execution in sec. Use -1 to disable timeout. Default value defined in ecl-test.json config file (see: 9.)
|        --keyDir [KEYDIR], -k [KEYDIR]
|                                 Key file directory to compare test output. Default value defined in regress.json config file.
|        --ignoreResult, -i       Completely ignore the result.
|        -X name1=value1[,name2=value2...]
|                                 Sets the stored input value (stored('name')).
|        -f optionA=valueA[,optionB=valueB...]
|                                 Set an ECL option (equivalent to #option).
|        --pq threadNumber        Parallel query execution with threadNumber threads. (If threadNumber is '-1' on a single node system then threadNumber = numberOfLocalCore * 2)
|        --noversion              Avoid version expansion of queries. Execute them as a standard test.
|        --server [networkAddress]
|                                 ESP server address. Default value (espIp) defined in
|                                 ecl-test.json config file.
|        --username [username], -u [username]
|                                 Specify a username. If this appears in command line and the STDIO is a TTY like device then, the test engine displays a prompt to get user's password. 
|                                 Pipe like 'echo "<password>" \| ./elc-test run -u <username> ...' can be used to provide user's password as well.
|                                 The username and password overrides those stored in ecl-test.json config file.
|        --runclass class[,class,...], -r class[,class,...]
|                                 Run subclass(es) of the suite. Default value is 'all'
|        --excludeclass class[,class,...], -e class[,class,...]
|                                 Exclude subclass(es) of the suite. Default value is 'none'
|        --jobnamesuffix suffix   Specify workunit job name suffix.
|        --flushDiskCache         Flush OS (Linux) Disk Cache before execute ECL code
|                                 (sudo privileges needed). Ignored when --pq <n> > 1
|        --flushDiskCachePolicy flushDiskCachePolicy
|                                 Set flush disk cache policy. The default is 1 to clear before first run only. For 2 to clear before every run.
|        --runcount runcount      Execute individual test case(s) in given times. Default value is 1
|        --target [target_cluster_list | all], -t [target_cluster_list | all]
|                                 Run the cluster(s) suite. If target = 'all' then run
|                                 suite on all clusters. If not defined then default
|                                 value(s) come from config (ecl-test.json by default).
|        --publish, -p            Publish compiled query instead of run.
|        --handleEclccWarningFile, -w
|                                 Create/overwrite/delete ECLCC warning file.
|


Parameters of Regression Suite query sub-command:
-------------------------------------------------

Command:

    ./ecl-test query <-h|--help>

Result:

|
|       usage: ecl-test query [-h] [--config [CONFIG]]
|                             [--loglevel [{info,debug}]]
|                             [--suiteDir [SUITEDIR]]
|                             [--timeout [TIMEOUT]]
|                             [--keyDir [KEYDIR]]
|                             [--ignoreResult]
|                             [-X name1=value1[,name2=value2...]]
|                             [-f optionA=valueA[,optionB=valueB...]]
|                             [--pq threadNumber]  [--noversion]
|                             [--server [networkAddress]]
|                             [--runclass class[,class,...]]
|                             [--excludeclass class[,class,...]]
|                             [--jobnamesuffix suffix] [--flushDiskCache]
|                             [--target [target_cluster_list | all]] [--publish]
|                             [--handleEclccWarningFile]
|                             ECL_query [ECL_query ...]
|
|       positional arguments:
|        ECL_query                Name of one or more ECL file(s). It can contain wildcards. (mandatory).
|
|       optional arguments:
|        -h, --help               Show this help message and exit
|        --config [CONFIG]        Config file to use. Default: ecl-test.json.
|        --loglevel [{info,debug}]
|                                 Set the log level. Use debug for more detailed logfile.
|        --suiteDir [SUITEDIR], -s [SUITEDIR]
|                                 SuiteDir to use. Default value is the current directory and it can handle relative path.
|        --timeout [TIMEOUT]      Timeout for query execution in sec. Use -1 to disable timeout. Default value defined in ecl-test.json config file (see: 9.)
|        --keyDir [KEYDIR], -k [KEYDIR]
|                                 Key file directory to compare test output. Default value defined in regress.json config file.
|        --ignoreResult, -i       Completely ignore the result.
|        -X name1=value1[,name2=value2...]
|                                 Sets the stored input value (stored('name')).
|        -f optionA=valueA[,optionB=valueB...]
|                                 Set an ECL option (equivalent to #option).
|        --pq threadNumber        Parallel query execution with threadNumber threads. (If threadNumber is '-1' on a single node system then threadNumber = numberOfLocalCore * 2)
|        --noversion              Avoid version expansion of queries. Execute them as a standard test.
|        --server [networkAddress]
|                                 ESP server address. Default value (espIp) defined in ecl-test.json config file.
|        --username [username], -u [username]
|                                 Specify a username. If this appears in command line and the STDIO is a TTY like device then, the test engine displays a prompt to get user's password. 
|                                 Pipe like 'echo "<password>" \| ./elc-test run -u <username> ...' can be used to provide user's password as well.
|                                 The username and password overrides those stored in ecl-test.json config file.
|        --runclass class[,class,...], -r class[,class,...]
|                                 Run subclass(es) of the suite. Default value is 'all'
|        --excludeclass class[,class,...], -e class[,class,...]
|                                 Exclude subclass(es) of the suite. Default value is 'none'
|        --jobnamesuffix suffix
|                                 Specify workunit job name suffix.
|        --flushDiskCache         Flush OS (Linux) Disk Cache before execute ECL code (sudo privileges needed). Ignored when --pq <n> > 1
|        --flushDiskCachePolicy flushDiskCachePolicy
|                                 Set flush disk cache policy. The default is 1 to clear before first run only. For 2 to clear before every run.
|        --runcount runcount      Execute individual test case(s) in given times. Default value is 1
|        --target [target_cluster_list | all], -t [target_cluster_list | all]
|                                 Target cluster(s) for query to run. If target = 'all'
|                                 then run query on all clusters. If not defined then
|                                 default value(s) come from config (ecl-test.json by default).
|         --publish, -p           Publish compiled query instead of run.
|         --handleEclccWarningFile, -w
|                                 Create/overwrite/delete ECLCC warning file.
|


6. Tags used in test cases:
---------------------------

   To define a class to be executed/excluded in run mode.
//class=<class_name>

    This tag should use when a test case intentionally fails to handle it as pass.
    If a test case intentionally fails then it should fail on all allowed platforms.
//fail

    This tag should use when an ECL file will be published but contains
    library instead of executable query and the target should by different 
    (see roxie vs roxie-workunit in containerized platfrom, where the firs handles only published queries and
    the second handles Workunits only and a library published into roxie can't reach from workunit excuting roxie-workunit.).    
//library

    To exclude testcase from cluster or clusters, the tag is:
//no<cluster_name>

    To switch off the test case output matching with key file
    (If this tag exists in the test case source then its output stored into the result log file.)
//nokey

    If //nokey is present then the following tag prevents the output being stored in the result log file.
//nooutput

    To build and publish testcase (e.g.:for libraries)
//publish

    To skip (similar to exclusion, but can have reason)
//skip type==<cluster> <reason>
    or
//skip type=<cluster> <reason>

    To set individual timeout for test case
//timeout <timeout_value_in_sec>
 
    To allow multiple tests to be generated from a single source file
    The regression suite engine executes the file once for each //version line in the file. It is compiled with command line option -Dn1=v1 -Dn2=v2 etc.
    The string value should quoted with \'.
    Optionally 'no<target>' exclusion info can add at the end of tag.
    Special variable 'flushDiskCache' with 'true' can be used to force OS (Linux) disk cache flush beforeore execute ECl code.
//version <n1>=<v1>,<n2>=<v2>,...[,no<target>[,no<target>]]

   

7. Key file handling:
---------------------

After an ECL test case execution finished and all output collected the result checking follows these steps:

If the ECL source contains //nokey tag
    then the key file and output comparison skipped and the output can control by //nooutput tag
    else RS checks cluster specific key directory and key file existence
        If both exist
            then output compared with cluster specific keyfile
            else output compared with the keyfile located KEY directory

Examples:

We have a simple structure only one ECL file and two related keyfile. One in hthor and one in key directory.

 ecl
   |---hthor
   |     alljoin.xml
   |---key
   |     alljoin.xml
   |---setup
   alljoin.ecl

If we execute this query:

     ./regress query alljoin.ecl all

Then the RS executes alljoin.ecl on all target clusters and
    on hthor the output compared with hthor/alljoin.xml
    on thor and roxie the output compared with key/alljoin.xml

For Setup keyfile handling same as Run/Query except the target specific keyfile stored platform directory under setup:

ecl
   |---hthor
   |     alljoin.xml
   |---key
   |     alljoin.xml
   |     setup.xml
   |     setup_fetch.xml
   |     setup_sq.xml
   |     setup_xml.xml
   |---setup
   |      |
   |      ---hthor
   |      |       setup.xml
   |      setup.ecl
   |      setup_fetch.ecl
   |      setup_sq.ecl
   |      setup_xml.ecl
   alljoin.ecl|

If we execute setup on target hthor:

     ./regress  setup -t hthor

Then the RS executes all ecl files from setup directory and 
    - the result of setup.ecl compared with ecl/setup/hthor/setup.xml
    - all other test cases results compared with corresponding file in ecl/key directory.

If we execute setup on any other target:

     ./regress  setup -t thor|roxie

Then the RS executes all ecl files from setup directory and 
    - the test cases results compared with corresponding file in ecl/key directory.

8. Key file generation:
-----------------------

The regression suite stores every test case output into ~/HPCCSystems-regression/result directory. This is the latest version of result. (The previous version can be found in ~/HPCCSystems-regression/archives directory.) When a test case execution finished Regression Suite compares this output file with the relevant key file to verify the result.

So if you have a new test case and it works well on all clusters (or some of them and excluded from all others by //no<cluster> tag inside it See: 6. ) then you can get key file in 2 steps:

1. Run test case with ./ecl-test [suitedir] query <testcase.ecl> <cluster> .

2. Copy the output (testcase.xml) file from ~/HPCCSystems-regression/result to the relevant key file directory.

(To check everything is fine, repeat the step 1 and the query should now pass. )

9. Configuration setting in ecl-test.json file:
-------------------------------------------------------------

        "roxieTestSocket": ":9876",                     - Roxie test socket address (not used)
        "espIp": "127.0.0.1",                           - ESP server IP
        "espSocket": "8010",                            - ESP service address
        "useSsl" : "False",                             - Control SSL encryption in communication with ESP server
                                                          If it is set to 'True' then espSocket, username and password 
                                                          should be updated accordingly
        "username": "regress",                          - Regression Suite dedicated username and pasword
        "password": "regress",
        "suiteDir": "",                                 - Default suite directory location - ""-> current directory
        "eclDir": "ecl",                                - ECL test cases directory source
        "setupDir": "ecl/setup",                        - ECL setup source directory
        "keyDir": "ecl/key",                            - XML key files directory to check testcases result
        "archiveDir": "archives",                       - Archive directory path for testcases generated XML results
        "resultDir": "results",                         - Current testcases generated XML results
        "regressionDir": "~/HPCCSystems-regression",    - Regression suite work and log file directory (in user private space)
        "logDir": "~/HPCCSystems-regression/log",       - Regression suite run log directory
        "Clusters": [                                   - List of known clusters name
            "hthor",
            "thor",
            "roxie"
        ],
        "timeout":"720",                                - Default test case timeout in sec. Can be override by command line parameter or //timeout tag in ECL file
        "maxAttemptCount":"3"                           - Max retry count to reset timeout if a testcase in any early stage (compiled, blocked) of execution pipeline.

Optionally the config file can contain some sections of default values:

If the -t | --target command line parameter is omitted then the regression test engine uses the default target(s) from one of these default definitions. If undefined, then the engine uses the first cluster from the Cluster array.

        "defaultSetupClusters": [
            "hthor",
            "thor3"
        ]

        "defaultTargetClusters": [
            "thor",
            "thor3"
        ]

For stored parameters:

    "Params":[
                "querya.ecl:param1=value1,param2=value2",
                "queryb.ecl:param1=value3",
                "some*.ecl:paramforsome=value4",
                "*.ecl:globalparam=blah"
            ]

The Regression Suite processes the Params definition(s) sequentially. The -Xname=value command line parameter overrides any values defined in this section.
Examples:

We have an ECL source called PassTest.ecl with these lines:

|    //nokey        # To avoid result comparison error
|    string bla := 'EN' : STORED('bla');
|    output(bla);

1. For the purposes of this example, we assume there is no Params section in the testing/regress/ecl_test.json file or it is empty and there are no PassTest.ecl related global entries.

If we execute it with query mode:

|     ./ecl_test query PassTest.ecl -t hthor

The result is:

|     [Action] Target: hthor
|     [Action] Queries: 1
|     [Action]   1. Test: PassTest.ecl
|     [Pass]   1. Pass W20140508-180241 (1 sec)
|     [Pass]   1. URL http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140508-180241
|     [Action]
|         Results
|         -------------------------------------------------
|         Passing: 1
|         Failure: 0
|         -------------------------------------------------
|         u"Output of PassTest.ecl test is:\n\t<Dataset name='Result 1'>\n <Row><Result_1>EN</Result_1></Row>\n</Dataset>\n"
|         -------------------------------------------------
|         Log: /home/ati/HPCCSystems-regression/log/hthor.14-05-08-18-02-41.log
|         -------------------------------------------------
|         Elapsed time: 4 sec  (00:00:04)
|         -------------------------------------------------

2. Same as 1. but execute it in query mode with -X parameter:

|     ./ecl_test -Xbla=blabla query PassTest.ecl -t hthor

then the output of PassTest.ecl changes in the result:
|         -------------------------------------------------
|         u"Output of PassTest.ecl test is:\n\t<Dataset name='Result 1'>\n <Row><Result_1>blabla</Result_1></Row>\n</Dataset>\n"
|         -------------------------------------------------

3. If we want to apply same stored value every execution then we can put it into the ecl_test.json configuration file:

|    "Params":[
|                "PassTest.ecl:bla='A value'"
|          ]

We can execute it with a simple query mode:

|     ./ecl_test query PassTest.ecl -t hthor

then the output of PassTest.ecl changes in the result accordingly with the value from the Params option:
|         -------------------------------------------------
|         u"Output of PassTest.ecl test is:\n\t<Dataset name='Result 1'>\n <Row><Result_1>A value</Result_1></Row>\n</Dataset>\n"
|         -------------------------------------------------

4. Finally we have value(s) in the config file, but we want to run PassTest.ecl with another input value.

In this case we can use same command as in 2. with a new value:

|     ./ecl_test -Xbla='Another value' query PassTest.ecl -t hthor

then the output of PassTest.ecl changes in the result:
|         -------------------------------------------------
|         u"Output of PassTest.ecl test is:\n\t<Dataset name='Result 1'>\n <Row><Result_1>Another value</Result_1></Row>\n</Dataset>\n"
|         -------------------------------------------------

We can use as many values as we need in this form:
|       -Xname1=value1,name2=value2...

Important!
    There should not be any spaces before or after the commas.
    If there is more than one -X in the command line, the last will be the active and all other discarded.


For default engine paramters:
|    "engineParams":[
|            "failOnLeaks"
|        ]

The Regression Suite processes the engineParams definition(s) sequentially and adds them with '-f' prefix to the 'ecl run ...' command.

We can store file names (with wildcards) to exclude them from suite like the --excludeFile filespec[,filespec,...] cli parameter. It can be useful when we need to exclude a large amount of files without changing them (like adding a kind of //calss<whatever> line into them)

|   "FileExclusion" : [
|
|       ]

Example: The

|   "FileExclusion" : [
|           "*expire*
|       ]

has the same effect as 

|     ./ecl-test query -t thor --ef "*expire*" spray*
command


10. Authentication:
-------------------

If your HPCC System is configured to use LDAP authentication you should change value of "username" and "password" fields in ecl-test.json file to yours.

Alternatively, ensure that your test system has a user "regress" with password "regress" and appropriate rights to be able to run the suite.


11. Handling ECLCC warnings:
----------------------------
There is a new feature of the Regression Test Engine: Eclcc warning check.

With this feature, the engine checks the Eclcc compiler output (stderr stream) for every ECL test cases and looking for warnings.

The possible events are:
Test pass:
    1. The test compiled without any warning. In this case the execution continuous as previously.
    2. The test compiled with warnings, but the engine found ‘.eclccwarn’ file with all warnings. In this case the state is well known  and the test execution continuous as previously

Test failing:
    3. Suddenly the test compiled with one or more warnings. If this situation is new no eclccwarn file associated to that test case then the engine reports those new warnings as error and the test aborted.
    4. The test compiled with warnings, the engine found .eclccwarn file, but there is some difference (warning(s) appear or disappear). In this case engine reports the difference between current compiler output and the state stored in .eclccwarn file. Further execution of test is  aborted
    5. The test compiled without warnings, but the engine found .eclccwarn file. This means the warning(s) suddenly/unintentionally disappeared and the engine reports that changes and abort the test.

For this checking the in events 2-5 the engine need an .eclccwarn file. To generate that file there is two ways:
    1. Manually: 
        a. In this case the ECL code should  compile with eclcc command like this:
              eclcc  <ecl_file>.ecl  2> <ecl_file>.eclccwarn
           with the stderr stream redirected into a file

        b. Because the warning report contains the path to the ECL file and this path can be different from system to system and execution by execution (OBT, Smoketest, developer environment, etc.) all path should remove from the generated <ecl_file>.eclccwarn file. 

        c. The edited <ecl_file>.eclccwarn must copy to the same place where the associated key file (<ecl_file>.xml) located.

        d. Example:
            i. Here is a simple ECL file with one line of code:
                    '1'[1..2]
               stored in ‘ecl/eclccwarning.ecl’ file.

            ii. Execute it with:
                    eclcc ecl/eclccwarning.ecl 2>eclccwarning.eclccwarn

            iii. The content of the ‘eclccwarning.eclccwarn’ file is:
                    ecl/eclccwarning.ecl(1,5): warning C2121: Invalid substring range: index 2 out of bound: 1..1
                    0 error, 1 warning

                So, the ‘.eclccwarn’ file contains the path ‘ecl/’ and in must remove:
                    eclccwarning.ecl(1,5): warning C2121: Invalid substring range: index 2 out of bound: 1..1
                    0 error, 1 warning
                
            iv. Copy the edited file into ecl/key/ directory and the next run of Regression Test Engine it will be used to check compiler warnings.
           
    2. Automated: (Warning!!! This is an easier but dangerous way!)
        a. In this case the ECL code can run with Regression Test Engine like this:
                ./ecl-test query –t <target_cluster> –w <ecl_file>.ecl  
           The newly implemented –w or --handleEclccWarningFile parameter force the engine to create, rewrite or delete the <ecl_file>.eclccwarn file. Depend on the result of warning check.

        b. This means
            i. In event 3 a new warning file created.
            
            ii. In event 4 the existing warnings file overwritten by a new result
                Warning! If appearing/disappearing of warning is not intentional, the previous warning state lost.
                
            iii. In event 5, all warnings disappeared the warning file is deleted.
                Warning! It is same problem as II.
                
        c. Important! 
           The –w or  --handleEclccWarningFile parameter working with query with wildcards and run mode and can cause to overwrite or remove all associated warning files.

Last comment: the warning file is part of the (Regression) suite, so it must be handled same way as the ECL test code and the test related key file. 

