# Vitro Logging (in developement)

In general, these steps are helpful when debugging a specific module during local development.

1. Start Tomcat,
2. Go to http://localhost:8080/vitro/admin/log4j.jsp
3. Find the module you are using (i.e. `com.hp.hpl.jena.sparql.engine.http.HttpQuery`)
  1. Note: Logger instances do not appear in the Log4J control page until the class they represent has been instantiated, so if the module is `edu.cornell.mannlib.vitro.webapp.searchindex.tasks.UpdateUrisTask` for instance, after starting Tomcat, login to the site admin panel and start a reindex 
4. Set the log level to DEBUG
5. Scroll to the bottom of the page and click `Submit`
6. Watch the `vitro.all.log` file grow **quickly**.
