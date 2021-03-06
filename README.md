# Docker image for tomcat with logback integration

Based on the official tomcat image, but with logs using logback.


Some environment variables are available to tune the logs:

* DEFAULT_LOG_LEVEL: Set the default log level.
* TOMCAT_LOG_LEVEL: Set the tomcat log level.
* TOMCAT_LOG_TYPE:
  * `classic` (default): The logs are humane readable. Access logs are going to stdout and the other logs are going to stderr.
  * `json`: The logs will be formatted in a JSON suitable for logstash. Access logs are going to stdout and the other logs are going to stderr.
  * `logstash`: The logs will be formatted in a JSON suitable for logstash (@cee) and sent by syslog/UDP. The access logs are going to stdout in json format. More variables are available for this mode:
    * TOMCAT_LOG_HOST: the target host
    * TOMCAT_LOG_PORT: the target port

If you want to change the way things are logged, change the ${CATALINA_HOME}/conf/logback-custom.xml file.

If your application uses logback/log4j, it is recommended to not ship those libraries with your webapp.
Just use the ones provided at tomcat level.

Other changes compared the official tomcat image:

* All the default webapps are removed.
* TLD and JAR scanners are disabled (faster startup).
* Resources caching is properly configured.
