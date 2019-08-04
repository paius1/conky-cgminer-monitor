# conky-cgminer-monitor
Add Script to Conky to monitor Bitcoin Mining Rigs

These Files allow you to Monitor your bitcoin mining rigs running
cgminer with Conky 

Place these scripts:
 cgminer-monitor-horizontal
 conky-monitor-bar  (or any conky config)
 gradient_function
 Miners
 Pools
in the same directory. Conky bases file paths on the location of
the config file used to start it

Edit:

1) /etc/hosts
   on Debian I added [IP address] [hostname] to the end of the file
   e.g as root echo 10.10.10.25 Miner1 >> /etc/hosts

2) cgminer startup with "--api-listen" option

3) conky-monitor-bar
    alignment may be top_left, top_right, top_middle,
     bottom_left, bottom_right, bottom_middle,
     middle_left, middle_middle, middle_right
    x and y gap
    mimimum size fit to your screen
    or just add ${execpi 10 cgminer-monitor-horizontal} to and existing conky config
    
4) Miners
   Miners is an associative array of the form
   Miners=( ["Hostname"]="a goto value for Conky" )
    e.g. 
     Miners=( ["Miner1"]="10" ["Miner2"]="150" )

5) Pools
   Pools is an associative array of the form
   Pools=( ["Pool named returned by cgminer-api"]="An Abbreviation" )
   execute cgminer-api [Hostname] to find the full pool name
    e.g. 
     Miners=( ["stratum+tcp://somepool.com"]="SMP" ["anotherpool.com"]="ANO" )

6) cgminer-monitor-horizontal
   set lower_limit and step for each worker and for 
   the Cumulative Totals  lines 79 and 152
   Set $lower_limit and $step to place "Normal" Value as Yellow
   e.g. I am running Antminer S3's which run "normally" at 480Gh/s
        There are 36 steps in the gradient function
        play with these numbers to get them right
        Set the value for AverageRate (line 81) and AvgHashRate
        (line 157) manually to see the results
  
7) adjust Miners Array to fit each worker on the bar 
    with my setup I can fit 8  rigs on a 1080x1920 screen
