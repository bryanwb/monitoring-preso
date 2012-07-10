
monitoring preso

* what we have now
  - nagios
  - rhq
* Aren't these two enough?
  - nagios best at OS-level level checks, sucks for getting arbitrary
 metrics and visualization. excellent at alerting
  - rhq is very powerful, but only really good for jmx metrics, also
 not very flexible and not very well-supported
  - neither can gather metrics from logs nor aggregate logs
* Aggregating Logs - why?
  - graphic of one log, catalina.out from 1 instance
  - graphic of 4 logs, catalina.out from 4 instances
  - enter logstash
* logstash 
  - components shipper, indexer
  - takes inputs, filter/mutate, output
  - nc logs.data.fao.org 5200 < '{ "some": "json" }'
* haproxy example
  - shipper on haproxy servers ships log entries
  - indexer on server matches fields to a pattern
  - sends it on to Elastic search
* web UI
  - really looking at the log entries stored by elastic search
  - can search logs
    - by date
    - date by any indexed field
    - w/ wildcards but it is tricky
  - can view a stream
  - can limit fields displayed
* demo of haproxy logs
* demo of catalina.out logs
* technical components
  - logstash entirely written in Ruby and runs on JRuby
  - Elastic search is storage backend
  - web interface is Twitter bootstrap w/ a small PHP backend
* limitations
  - currently no way to save your search for later use

* getting metrics from logs
  - sending them to graphite
* show graphite
  - arbitrary time periods
  - adding multiple 
* Graphite - visualization for any metric
  - can send anything to graphite
    nc logs.data.fao.org 5200 < 'stats.fao.http_requests 1'
  - can send it jmx data
  - how to use the interface
  - sending jmx data
* self-service monitoring and metrics
  - previous examples require cooperation of sysadmins
  - even you can send metrics to graphite, tho I prefer u ask me first
  - many people use Statsd, a local daemon that forwards to graphite
    or Coda Hale's metrics
  - Coda Hale's metrics library and talk

* next steps
  - Damiano and I still playing w/ graphite, don't know if it will
  replace rhq partly or entirely
  - start piping more logs to logstash
  - u guys are welcome to play w/ Metrics and start sending stuff to graphite
  