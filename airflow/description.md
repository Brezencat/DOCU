**Description:** As the name suggestes it is a small description about the service

**After:** It simply means that your service must be started after the services that are required for your deamon to run, like for apache-airflow we need network, postgresql and mysql to be ready before it gets started. If your apache-airflow installation requires redis or rabbitmq services than you can specify the dependency here

**EnvironmentFile:** it specifies the file where service will find its environment variables in ubuntu its /etc/environment

**User:** set your actual username here, the specified userid will be used to invoke the service

**ExecStart:** here you can specify the command to be executed or set the proper path to your script that needs to be excuted. in our case we simple need to run the command airflow webserver

**Restart:** by default, systemd does not restart your service if the program exits for whatever reason. This is usually not what you want for a service that must be always available, so we’re instructing it to always restart on-failure

**RestartSec:** by default, systemd attempts a restart after 100ms. You can specify the number of seconds to wait before attempting a restart, using RestartSec.