# Oseberg DevOps Screener

Please complete the following and submit source code and output to the person
that sent you this screener. Please also track and state with how much time you
spent on each assignment.

You're welcome to use Internet resources in solving these problems, as long as
they don't give you a complete solution, and you obviously can't ask people
(online or in person) for help. Please cite every resource that you used.

In order to test your solution you'll need to have PostgreSQL and Linux
installed. If you're not running these on your computer already, using Docker is
a great way to quickly spin these up.

The thought that goes into this is more important than achieving perfection, so
don't worry about making sure it's 100% bug free (though it certainly should be
tested adequately). We prefer simple solutions. The goal is not for you to spend
a lot of time on these problems. If it turns out to be very time-consuming
please talk to me.

Please reach out to me if you have any questions about this or would like to
seek clarification.

The interview team will use this assignment to determine if you may be a
suitable candidate for the position.


## Problem #1: PostgreSQL info retriever

You have two servers, one running a Postgres database. You do not have SSH
access to the server that hosts the Postgres database. From the machine *not*
running the Postgres instance write a bash script that connects to the database
and displays the following output derived from that database:

```
Number of non-idle database connections: ___
Date & time on database server: _____________________________
List of databases: <db1>, <db2>, <db3>, ...
```

Example output:
```
Number of non-idle database connections: 2
Date & time on database server: 2018-05-25 14:25:00.647533-05
List of databases: postgres, template0, template1, test1, test2
```

If the Postgres database is down it should wait to execute the SQL queries
needed to generate the output above until it's verified that the database is up
and accepting connections. For the list of databases do not use a SQL
aggregation function to come up with a comma-separated list. Instead, handle
consolidation of multiple values into a single comma-separated line within bash
(and any standard \*nix tools you'd like to use, of course).


## Problem #2: Processes with top disk reads

Write a Python script that quietly collects disk read statistics until you hit
the `<return>` key. Once you hit `<return>` it should print out the top 10
processes that are reading the most data from disk over the course of the script
duration. It should display the PID and number of bytes read from the storage
layer (while the script was running) for each top 10 process. This script should
not report cumulative numbers (i.e. don't report disk usage since the beginning
of a process); it should only report bytes read since the invocation of the
script.

You can assume it'll run on a 64-bit Linux server running a 2.6.20+ kernel.
You're welcome to call out to external commands from within the Python script,
although it's certainly possible to do without. You can assume this script is
invoked as the root user, but if it's not run as root and you get permissions
errors while retrieving I/O stats for processes you don't own you can just
ignore those processes, and calculate I/O only for processes for which you can
access I/O stats.

Example output:
```
Please press <return> to stop collecting data.

PID     Bytes read
15489   38084608
14585   22536192
564     630784
24672   327680
32072   114688
14908   65536
20115   32768
19551   16384
1       0
2       0
```
