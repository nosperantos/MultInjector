# MultInjector
MultInjector is an automated, mass SQL Injection tool with preprogrammed tasks for complete server takeover

MultiInjector Feature List:
--------------------------

1.    Receives a list of URLs as input
2.    Recognizes the parameterized URLs from the list
3.    Fuzzes all URL parameters to concatenate the desired payload once an injection is successful
4.    Automatic defacement - you decide on the defacement content, be it a hidden script, or just pure old "cyber graffiti" fun
5.    OS command execution - remote enabling of XP_CMDSHELL on SQL server, subsequently running any arbitrary operating system command lines entered by the user
6.    Configurable parallel connections exponentially speed up the attack process - one payload, multiple targets, simultaneous attacks
7.    Optional use of an HTTP proxy to mask the origin of the attacks

Requirements:
--------------

    * Python >= 2.4
    * Pycurl (compatible with the above version of Python)
    * Psyco (compatible with the above version of Python)

Windows Support
-----------------

The binary has been compiled using the wonderful Pyinstaller.
You may custom compile it yourself by downloading Pyinstaller and following the
straightforward instructions attached, describing how to compile on Windows.

Linux Support
---------------

Simply remove or comment out the "import psyco" line
You may also use Pyinstaller as described in the Windows section above to compile native
UNIX binaries.

Usage:
------

Following is an example of using MultiInjector against a list of URLs from a text file named targets.txt

The next choice is the attacks menu. It allows one choice from:

1) Automatic defacement - Try to concatenate a string to all user-defined text fields in DB
2) Run OS shell command on DB server - Run any OS command as if you're running a command console on the DB machine
3) Run SQL query on DB server - Execute SQL commands of your choice
4) Enable OS shell procedure on DB - Revive the good old XP_CMDSHELL where it was turned off (default mode in MSSQL-2005)
5) Add administrative user to DB server with password: T0pSeKret - Automagically join the Administrators family on DB machine
6) Enable remote desktop on DB server - Turn remote terminal services back on...

In case you choose the OS command option, you will need to type in a Windows shell command such as:
echo test > c:\hacked.txt
However, in this example an arbitrary Javascript is chosen to be the defacement content in an automatic DB defacement scenraio.
The number of parallel connections defines the concurrent number of HTTP sessions being initiated against URLs from the list.
An optional HTTP proxy may be used to mask the origin of the attacks. For the sake of this example, the Vidalia bundle is being used. So the Privoxy port is 8118, listening on the localhost interface = 127.0.0.1
This is configurable after choosing 'y' or 'yes' at the 'Use HTTP proxy?' prompt
Here's what it looks like at run time:

> python MultiInjector.py targets.txt

Please choose the attack of your flavor:

1) Automatic defacement
2) Run OS shell command on DB server
3) Run SQL query on DB server
4) Enable OS shell procedure on DB
5) Add administrative user to DB server with password: T0pSeKret
6) Enable remote desktop on DB server

> 1

Enter defacement content:

> <script>alert('You have been hacked!')</script>

Number of parallel connections: (default=5)

> 10

Use HTTP proxy? [y/n]: (default=n)

> y

Proxy address:

> 127.0.0.1

Proxy port:

> 8118

[!] Bombs Away !!
