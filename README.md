# tomcat_bin cookbook

Install and configure Tomcat using Apache binaries.

**This cookbook and documentation are under construction.**

## Recipes
### default
Install and configure tomcat. Please note this recipe does NOT install Java.
You should install Java earlier in your run list before including this recipe.
For example...
* [java](https://supermarket.chef.io/cookbooks/java) community cookbook
* [oracle_jdk](https://github.com/bdclark/chef-oracle_jdk) - my cookbook dedicated
to installing the Oracle JDK

### Attributes
Uses the tomcat_bin resource (see below) to install and configure tomcat.
See the resource attributes listed below and attributes/default.rb for default settings.

## Resources and Providers

### tomcat_bin
Install and/or configure an instance of tomcat.

#### Actions
* `install` - Default action. Download and install tomcat into `home`
* `configure` - create user, configs, service, ulimits, etc. and start service

#### Attributes
* `home` - required install directory of tomcat; default: name of resource block
* `service_name` - optional name of service (defaults to basename of `home`)
* `user` - user running tomcat; default: `tomcat`
* `group` - primary group of tomcat user; default: `tomcat`
* `service_name` - optional name of service (defaults to basename of `home`)
* `mirror` - url to apache tomcat mirror (defaults to node attribute)
* `version` - version of tomcat to download/install (defaults to node attribute)
* `checksum` - sha256 checksum of downloaded tarball (defaults to node attribute)
* `log_dir` - directory for tomcat logs; default: 'logs'. Can be absolute or relative to `home`
* `logs_rotatable` - sets tomcat rotatable flag; default: `false`.
If false, tomcat will not rotate logs but logrotate will.
(Also applies to access log if `access_log_enabled` is true)
* `logrotate_frequency` - rotation frequency; default: `weekly`
* `logrotate_count` - logrotate file count
* `ulimit_nofile` - optional open file ulimit for tomcat user (integer)
* `ulimit_nproc` - optional num procs ulimit for tomcat user (integer)
* `kill_delay` - seconds to wait before kill -9 on service stop/restart; default: 45 (integer)
* `initial_heap_size` - optional java initial heap size (-Xms) added to CATALINA_OPTS
* `max_heap_size` - optional java max heap size (-Xmx) added to CATALINA_OPTS
* `max_perm_size` - optional java max permanent size (-XX:MaxPermSize) added to CATALINA_OPTS
* `catalina_opts` - optional string or array of CATALINA_OPTS in setenv.sh
* `java_opts` - optional string or array of JAVA_OPTS in setenv.sh
* `java_home` - optional JAVA_HOME in setenv.sh
* `jmx_port` - JMX report port (integer); default: `nil` (JMX management is disabled if `nil`)
* `jmx_authenticate` - whether JMX authentication is enabled; default: `true`
(ignored unless `jmx_port` set)
* `jmx_monitor_password` - password for JMX readonly access; default: `nil`
(ignored unless `jmx_port` set and `jmx_authenticate` true)
* `jmx_control_password` - password for JMX readwrite access; default: `nil`
(ignored unless `jmx_port` set and `jmx_authenticate` true)
* `jmx_dir` - optional directory for jmxremote.password and jmxremote.access,
defaults to `home`/conf
* `shutdown_port` - tomcat shutdown port in server.xml; required
* `http_port` - optional http port (integer)
* `ajp_port` - optional ajp port (integer)
* `ssl_port` - optional ssl port (integer)
* `pool_enabled` - enable shared executor (thread pool); default: `false`
* `access_log_enabled` - whether to enable access log valve; default: `false`
* `http_additional` - hash of additional http connector attributes
* `ajp_additional` - hash of additional ajp connector attributes
* `ssl_additional` - hash of addtional ssl connector attributes
* `pool_additional` - hash of additional executor (thread pool) attributes
* `access_log_additional` - hash of additional access log valve attributes
* `engine_valves` - nested hash of one or more engine valves
* `host_valves` - nested hash of one or more host valves

## License and Authors
- Author:: Brian Clark (brian@clark.zone)

```text
Copyright 2015, Brian Clark

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
