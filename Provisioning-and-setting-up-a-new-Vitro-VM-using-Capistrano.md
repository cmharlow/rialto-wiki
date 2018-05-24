1. Create operations-tasks issue ([see example](https://github.com/sul-dlss/operations-tasks/issues/1633))
1. Create puppet PR ([see example](https://github.com/sul-dlss/puppet/pull/3045))
1. Add server environment to Capistrano configuration ([see example](https://github.com/sul-dlss-labs/Vitro/pull/7))
1. Run `cap ENVIRONMENT deploy`
1. Configure the home/config directories, namely `~/home/runtime.properties` (to setup baseURL, set root user email, and enable TLS SMTP) and `~/home/config/applicationSetup.n3` (to enable TDB as content store)
1. Make Vitro home directory writeable by `tomcat` user -- `chmod -R o+w home` -- and then restart Tomcat
1. Confirm Apache is proxying Tomcat (w/ Shib) at https://HOSTNAME.stanford.edu/vitro 
1. Confirm Vitro starts up w/o worrisome error messages
1. Create an initial root user in Vitro
