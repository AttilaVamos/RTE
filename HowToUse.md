# Steps to run Regression Suite

## Local mode

The Local Mode means: All components are located and/or running in same environment. The user cloned or has access to the source tree, started the HPCC Platform and executes the Regression Test Engine - RTE - ./ecl-test command)

### In Bare Metal (BM) or Virtual Machine (VM) environment

#### Preliminary

1. Cloned HPCC-Platform source tree from GitHub
2. Installed and started HPCC-Platform from local build or from donwloaded install package. Important: the selected branch in HPCC-Platfrom shpld match to the installed and started Platfrom version.

#### Steps

1. Change directory to HPCC-Platform/testing/regress subdirectory.

2. To list all available clusters:
They are coming from the configuration file: ./ecl-test.json in same directory and the command is:

    ./ecl-test list

The result (by default) looks like this:

        Available Clusters: 
            - hthor
            - thor
            - roxie

3. Setup
There are several test cases relied on existing and re-usable data and index file. Avoid to generate them in evry time when a test case need them, we put all generation into the Setup Suite.
To run the Regression Setup Suite, the command is::

        `./ecl-test setup`

to run setup on the default (thor) cluster

or
        `./ecl-test setup -t <target cluster> | all`

to run setup on a selected or all clusters

The result for thor:

>        [Action] Suite: thor (setup)
>        [Action] Queries: 4
>        [Action]   1. Test: setup.ecl
>        [Pass]   1. Pass W20140410-133419 (8 sec)
>        [Pass]   1. URL http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140410-133419
>        [Action]   2. Test: setup_fetch.ecl
>        [Pass]   2. Pass W20140410-133428 (3 sec)
>        [Pass]   2. URL http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140410-133428
>        [Action]   3. Test: setupsq.ecl
>        [Pass]   3. Pass W20140410-133432 (5 sec)
>        [Pass]   3. URL http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140410-133432
>        [Action]   4. Test: setupxml.ecl
>        [Pass]   4. Pass W20140410-133438 (2 sec)
>        [Pass]   4. URL http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140410-133438
>        [Action]
>            Results
>            -------------------------------------------------
>            Passing: 4
>            Failure: 0
>            -------------------------------------------------
>            Log: /home/ati/HPCCSystems-regression/log/thor.14-04-10-13-34-18.log
>            -------------------------------------------------
>            Elapsed time: 24 sec  (00:00:24)
>            -------------------------------------------------

To setup the proper environment for text search test cases there is a new component called setuptext.ecl. It uses data files from another location and the default location stored into the options.ecl. RS generates location from the run-time environment and passes it to the setup via stored variable called 'OriginalTextFilesEclPath'.

4.To run Regression Suite on a selected cluster (e.g. Thor):
Command:

        ./ecl-test run [-t <target cluster>|all] [-h] [--pq threadNumber]

Optional arguments:
  -h, --help         show help message and exit
   --target [target_cluster | all], -t [target_cluster | all]
|                        Target cluster for single query run. If target = 'all' then run query on all clusters. Default value is thor.
  --pq threadNumber  Parallel query execution with threadNumber threads.
                    ('-1' can be use to calculate usable thread count on a single node system)

The result is a list of test cases and their result.

The first and last couple of lines look like this:

|
|        [Action] Suite: thor
|        [Action] Queries: 320
|        [Action]
|        [Action]   1. Test: agglist.ecl
|        [Pass]   1. Pass W20131119-173524 (2 sec)
|        [Pass]   1. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-173524>
|        [Action]   2. Test: aggregate.ecl
|        [Pass]   2. Pass W20131119-173527 (1 sec)
|        [Pass]   2. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-173527>
|        [Action]   3. Test: aggsq1.ecl
|
|        .
|        .
|        .
|        [Action] 319. Test: xmlout2.ecl
|        [Pass] Pass W20131119-182536 (1 sec)
|        [Pass] URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-182536>
|        [Action] 320. Test: xmlparse.ecl
|        [Pass] Pass W20131119-182537 (1 sec)
|        [Pass] URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-182537>
|
|         Results
|         `-------------------------------------------------`
|         Passing: 320
|         Failure: 0
|         `-------------------------------------------------`
|         Log: /home/ati/HPCCSystems-regression/log/thor.13-11-19-17-52-27.log
|         `-------------------------------------------------`
|         Elapsed time: 2367 sec  (00:39:27)
|         `-------------------------------------------------`
|

If --pq option used (in this case with 16 threads) then then the content of the console log will be different like this:

|
|        [Action] Suite: thor
|        [Action] Queries: 320
|        [Action]
|        [Action]   1. Test: agglist.ecl
|        [Action]   2. Test: aggregate.ecl
|        [Action]   3. Test: aggsq1.ecl
|        [Action]   4. Test: aggsq1seq.ecl
|        [Action]   5. Test: aggsq2.ecl
|        [Action]   6. Test: aggsq2seq.ecl
|        [Action]   7. Test: aggsq4.ecl
|        [Action]   8. Test: aggsq4seq.ecl
|        [Action]   9. Test: alljoin.ecl
|        [Action]  10. Test: apply3.ecl
|        [Action]  11. Test: atmost2.ecl
|        [Action]  12. Test: bcd1.ecl
|        [Action]  13. Test: bcd2.ecl
|        [Action]  14. Test: bcd4.ecl
|        [Action]  15. Test: betweenjoin.ecl
|        [Action]  16. Test: bigrecs.ecl
|        [Pass]   2. Pass W20131119-150514 (4 sec)
|        [Pass]   2. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-150514>
|        [Pass]   1. Pass W20131119-150513 (4 sec)
|        [Pass]   1. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-150513>
|        [Action]  17. Test: bloom2.ecl
|        [Action]  18. Test: bug8688.ecl
|        [Pass]   3. Pass W20131119-150514-5 (5 sec)
|        [Pass]   3. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-150514-5>
|        [Action]  19. Test: builtin.ecl
|        [Pass]  12. Pass W20131119-150517 (5 sec)
|        [Pass]  12. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-150517>
|        [Action]  20. Test: casts.ecl
|        [Pass]  14. Pass W20131119-150517-2 (6 sec)
|        [Pass]  14. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-150517-2>
|        [Action]  21. Test: catchexpr.ecl
|        .
|        .
|        .
|        [Action] 257. Test: xmlparse.ecl
|        [Pass] 240. Pass W20131119-160614 (9 sec)
|        [Pass] 240. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160614>
|        [Pass] 241. Pass W20131119-160614-3 (10 sec)
|        [Pass] 241. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160614-3>
|        [Pass] 254. Pass W20131119-160622-1 (2 sec)
|        [Pass] 254. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160622-1>
|        [Pass] 191. Pass W20131119-160058-2 (327 sec)
|        [Pass] 191. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160058-2>
|        [Pass] 245. Pass W20131119-160617-3 (9 sec)
|        [Pass] 245. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160617-3>
|        [Pass] 248. Pass W20131119-160619-4 (7 sec)
|        [Pass] 248. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160619-4>
|        [Pass] 249. Pass W20131119-160619-3 (9 sec)
|        [Pass] 249. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160619-3>
|        [Pass] 250. Pass W20131119-160620 (10 sec)
|        [Pass] 250. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160620>
|        [Pass] 252. Pass W20131119-160620-3 (10 sec)
|        [Pass] 252. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160620-3>
|        [Pass] 253. Pass W20131119-160622 (8 sec)
|        [Pass] 253. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160622>
|        [Pass] 255. Pass W20131119-160623 (8 sec)
|        [Pass] 255. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160623>
|        [Pass] 256. Pass W20131119-160623-1 (9 sec)
|        [Pass] 256. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160623-1>
|        [Pass] 257. Pass W20131119-160624 (9 sec)
|        [Pass] 257. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160624>
|        [Pass] 213. Pass W20131119-160138-4 (305 sec)
|        [Pass] 213. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-160138-4>
|        [Pass] 127. Pass W20131119-155918 (462 sec)
|        [Pass] 127. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-155918>
|        [Pass] 100. Pass W20131119-155713 (600 sec)
|        [Pass] 100. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20131119-155713>
|        [Action]
|        [Action]
|         Results
|         `-------------------------------------------------`
|         Passing: 320
|         Failure: 0
|         `-------------------------------------------------`
|         Log: /home/ati/HPCCSystems-regression/log/thor.14-04-10-16-12-30.log
|         `-------------------------------------------------`
|         Elapsed time: 1498 sec  (00:24:58)
|         `-------------------------------------------------`
|

The logfile generated into the HPCCSystems-regression/log subfolder of the user personal folder and sorted by the test case number.

5.To run Regression Suite with selected test case on a selected cluster (e.g. Thor) or all:

Command:

        ./ecl-test query test_name [test_name...] [-h] [--target <cluster|all>] [--publish] [--pq <threadNumber|-1>]

Positional arguments:
        test_name               Name of a single ECL query. It can contain wildcards. (mandatory).

Optional arguments:
        -h, --help            Show help message and exit
        --target [target_cluster | all], -t [target_cluster | all]
                              Target cluster for query to run. If target = 'all' then run query on all clusters. Default value is thor.
        --publish             Publish compiled query instead of run.
        --pq threadNumber     Parallel query execution for multiple test cases specified in CLI with threadNumber threads. (If threadNumber is '-1' on a single node system then threadNumer = numberOfLocalCore * 2 )

The format of the output is the same as 'run', except there is a log, result and diff per cluster targeted:

|         [Action] Suite: hthor
|         [Action] Queries: 9
|         [Action]
|         [Action]   1. Test: aggsq1.ecl
|         [Action]   2. Test: aggsq1a.ecl
|         [Action]   3. Test: aggsq1seq.ecl
|         [Pass]   1. Pass W20140313-171024 (2 sec)
|         [Pass]   1. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171024>
|         [Action]   4. Test: aggsq2.ecl
|         [Action]   5. Test: aggsq2seq.ecl
|         [Failure]   2. Fail W20140313-171025 (2 sec)
|         [Failure]   2. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171025>
|         [Action]   6. Test: aggsq3.ecl
|         [Pass]   3. Pass W20140313-171026 (2 sec)
|         [Pass]   3. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171026>
|         [Action]   7. Test: aggsq3seq.ecl
|         [Pass]   4. Pass W20140313-171027 (2 sec)
|         [Pass]   4. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171027>
|         [Action]   8. Test: aggsq4.ecl
|         [Pass]   5. Pass W20140313-171028 (2 sec)
|         [Pass]   5. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171028>
|         [Action]   9. Test: aggsq4seq.ecl
|         [Pass]   6. Pass W20140313-171029 (2 sec)
|         [Pass]   6. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171029>
|         [Pass]   7. Pass W20140313-171029-1 (3 sec)
|         [Pass]   7. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171029-1>
|         [Pass]   8. Pass W20140313-171030 (2 sec)
|         [Pass]   8. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171030>
|         [Pass]   9. Pass W20140313-171031 (2 sec)
|         [Pass]   9. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171031>
|         [Action]
|         [Action]
|             Results
|             `-------------------------------------------------`
|             Passing: 8
|             Failure: 1
|             `-------------------------------------------------`
|             KEY FILE NOT FOUND. /home/ati/MyPython/RegressionSuite/ecl/key/aggsq1a.xml
|             `-------------------------------------------------`
|             Log: /home/ati/HPCCSystems-regression/log/hthor.14-03-13-17-10-24.log
|             `-------------------------------------------------`
|             Elapsed time: 10 sec  (00:00:10)
|             `-------------------------------------------------`
|
|         [Action] Suite: thor
|         [Action] Queries: 2
|         [Action]
|         [Action]   1. Test: aggsq2.ecl
|         [Action]   2. Test: aggsq2seq.ecl
|         [Pass]   1. Pass W20140313-171035 (3 sec)
|         [Pass]   1. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171035>
|         [Pass]   2. Pass W20140313-171036 (4 sec)
|         [Pass]   2. URL <http://127.0.0.1:8010/WsWorkunits/WUInfo?Wuid=W20140313-171036>
|         [Action]
|         [Action]
|             Results
|             `-------------------------------------------------`
|             Passing: 2
|             Failure: 0
|             `-------------------------------------------------`
|             Log: /home/ati/HPCCSystems-regression/log/thor.14-03-13-17-10-35.log
|             `-------------------------------------------------`
|             Elapsed time: 7 sec  (00:00:07)
|             `-------------------------------------------------`
|
|         [Action] Suite: roxie
|         [Action] Queries: 0
|         [Action]
|         [Action]
|         [Action]
|             Results
|             `-------------------------------------------------`
|             Passing: 0
|             Failure: 0
|             `-------------------------------------------------`
|             Log: /home/ati/HPCCSystems-regression/log/roxie.14-03-13-17-10-42.log
|             `-------------------------------------------------`
|             Elapsed time: 2 sec  (00:00:02)
|             `-------------------------------------------------`
|
|         End.

## Remote mode

The Remote Mode means: The source tree cloned into the local environment, HPCC-Platform or Client tools are installed too, but the HPCC Platform is running in other place like:

- Another BM/VM

- In cloud, like AKS

- In same machine, but
        - In Docker Desktop
        - In Minikube
  
### In Bare Metal (BM) or Virtual Machine (VM) environment

### In Containerized Environment

#### AKS

#### DockerDesktop

#### Minikube
