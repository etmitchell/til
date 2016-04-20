#Nagios

So when you define a new service to monitor and you're using NRPE (Nagios Remote Plugin Executor) it helps to actually pass the correct number of arguments specified by the command definition. ie:

NOTE: Also you need to change `dont_blame_nrpe=0` to `dont_blame_nrpe=1` on the Nagios server in /etc/nagios/nrpe.cfg

Supplied with apt-get install nagios-nrpe

    define command {
            command_name    check_nrpe
            command_line    /usr/lib/nagios/plugins/check_nrpe -H $HOSTADDRESS$ -c $ARG1$ -a $ARG2$
    }

Here is my simple service (it checks if a specifi service is running on a hostgroup).
My solution to my problem was to include `!60` on the `check_command` line. It was returning:
`no output returned from plugin` because I was not supplying enough arguments. 


    define service {
           hostgroup_name                  EC2-instances
           service_description             Check Wowza
           check_command                   check_nrpe!check_wowza!60
           use                             generic-service
           notification_interval           0 ; set > 0 if you want to be renotified
    }
