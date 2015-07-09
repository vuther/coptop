# coptop
<h3>Summary</h3>
coptop is a terminal-based PHP tool for monitoring and administrating a MySQL/MariaDB/Percona 5.0+ server. With this tool, DBAs can take full control of queries running on their database servers. Lay down the law!

I've been using mytop for a few years now and recently wanted to build my own monitoring tool because it didn't have all of the features I wanted. coptop was built with mytop in mind so thanks to Jeremy Zawodny for his work!

<h3>Requirements</h3>
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
  
<h3>Features</h3>
* Color coded threads that are based on time:
  - Green: Less than 1s
  - Yellow: 1-2s
  - Red: 3s+
* Master/slave information in header
* Threads taking less than 1 second are in milliseconds
* Other nice stats to see at a glance

<h3>Command line parameters</h3>
```
Login
  	-u        $user  (will check my.cnf client section for username field)
  	-p        $pass  (will check my.cnf client section for password field)
  	-h        $host
  	-P        $port  (port of server      - default: 3306)

Options
  	--ansi    0/1    (ansi refresh        - default: off) -- this is to eliminate flickering when the screen refreshes; currently bugged. If you know how to fix, please let me know :-)
  	--delay   $delay (delay in seconds    - default: 1)
  	--header  0/1    (show header         - default: on)
  	--idle    0/1    (show idle threads   - default: off)
  	--resolve 0/1    (resolve ips to host - default: on) -- also resolves host to ip
  	--sort    0/1    (reverse sort        - default: on)
  	--prompt         (prompts for password; text is invisible)
```
<h3>Commands</h3>
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
<h3>Want to contribute?</h3>
If you'd like to contribute, feel free to submit a merge request or get in contact with me. I'm open to all suggestions!

I'm currently tackling one problem where whenever ansi refresh is enabled, blank space in the header section can have "ghost" characters saved whenever you resize the terminal and what not. I have no clue why it does that. mytop does not do that so I think it's something PHP specific. If you know how to fix that, please let me know! :-)

