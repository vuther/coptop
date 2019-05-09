# coptop
coptop is a linux terminal-based PHP tool for monitoring and administrating a MySQL/MariaDB/Percona 5.0+ server. With this tool, DBAs can take full control of queries running on their database servers. Lay down the law!

I've been using mytop for a few years now and recently wanted to build my own monitoring tool because it didn't have all of the features I wanted. coptop was built with mytop in mind so thanks to Jeremy Zawodny for his work!

![ScreenShot](http://i.imgur.com/BT8t43S.png)

## Requirements
* This was built using PHP 5.5. I'm unaware of any incompabilities with other versions
* MySQLi
* Readline must be compiled with your PHP version
* MySQL privileges to fully utilize coptop:
  - KILL
  - PROCESS
  - REPLICATION CLIENT
* coptop runs these commands every $delay seconds:
  - SELECT Id, User, Host, db, Command, Host, Time_MS As Time, Info, State FROM information_schema.PROCESSLIST; OR SHOW FULL PROCESSLIST; depending on the version
  - SHOW GLOBAL STATUS;
  - SHOW MASTER STATUS;
  - SHOW SLAVE STATUS;
  
## Features
* Color coded threads that are based on time:
  - Green: Less than 1s
  - Yellow: 1-2s
  - Red: 3s+
* Master/slave information in header
* Threads taking less than 1 second are in milliseconds
* Other nice stats to see at a glance

## Command line parameters
```
Login
    -u        $user  (Will check my.cnf client section for username field)
    -p        $pass  (Will check my.cnf client section for password field)
    -h        $host
    -P        $port  (default: 3306) - port of server

Options
    --delay   $time  (default: 1)    - Refresh delay in seconds
    --notify  $email (default: off)  - Send email when slow query hits --limit value
    --limit   $time  (default: 30)   - Notify limit in seconds
    --ansi    0/1    (default: off)  - Ansi escape character method for smoother refresh that reduces flickering
    --header  0/1    (default: on)   - Show header
    --idle    0/1    (default: off)  - Show idle threads
    --resolve 0/1    (default: on)   - Resolve IPs to hostnames
    --sort    0/1    (default: on)   - Reverse sort
    --prompt         (prompts for password; text is invisible)
```
## Commands
```
Command Description
   ?    Help section
   c    Clear all filters
   d    Filter by database
   D    Display available databases
   e    Explain query/show information of a thread ID
   h    Filter by host/IP
   H    Hide/show stats header
   i    Hide/show idle threads
   k    Kill thread by ID
   K    Kill threads by username, host, or time range
   l    Set notify limit for slow queries
   o    Reverse sort order
   p    Pause screen
   q    Quit
   r    Resolve IPs to hostnames and vice versa
   R    Reset MySQL status counters via FLUSH STATUS
   s    Set delay in seconds
   t    Filter by minimum time
   u    Filter by user
   v    Display some important variables
```
## Want to contribute?
If you'd like to contribute, feel free to submit a merge request or get in contact with me. I'm open to all suggestions!

Current issues I'm tackling:
* Want to get rid of the readline dependency. It has to be installed w/ PHP from what I read so that's an issue for non-power users.

If you know how to fix any of these issues, please let me know! :-)
