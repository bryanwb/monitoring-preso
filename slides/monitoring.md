!SLIDE
# A New Hope


<br />
<br />
<br />
<center style="font-size:6em;">
Monitoring <br />data.fao.org<br /><br />

<img src="images/anewhope.png"></img>
</center>

.notes http://www.ironicsans.com/images/anewhope.png

!SLIDE
# Overview

* What we have now
* Why it sucks
* What might be better
* What you can do


!SLIDE
# We have a complicated application stack

<center style="font-size:4em;">systematic monitoring is critical to
untangling it</center><br />


<center><img src="images/spaghetti-bolognese.jpg" height="400px" width="600px" /></center>

.notes http://dummyatcooking.files.wordpress.com/2007/10/spaghetti-bolognese.jpg
                                         
!SLIDE
# We currently use Nagios and RHQ

<center><img src="images/monitoring.svg" /></center>

!SLIDE
# Downsides

<br />
<br />

* Graphing capabilities in Nagios+Cacti very limited
* Nagios is a pain to configure, even with Chef
* RHQ is powerful but very inflexible

!SLIDE
# More RHQ Issues
<br />
<br />

* The RHQ agent consumes non-trivial amount of RAM and CPU
* Extending it requires you to write Java class and a Maven pom.xml
* Small user community despite being a relatively mature project
* No easy way to access data in RHQ to create dashboards <br /> or do computations on data

!SLIDE
# That Makes me Want to...

<center><img src="images/the-scream.jpg" height="600px"
width="400px"></img></center>

.notes http://3.bp.blogspot.com/-RAPTS9vZKKw/TZB8Zf7HSpI/AAAAAAAAEmA/5uSAjc4xfsc/s1600/the-scream.jpg

!SLIDE
# A New Hope

* A more flexible monitoring system
* We will continue to use Nagios for alerting
* The future use of RHQ is uncertain
<br />
<br />
<center style="font-size:3em;">The DevOps Community has (mostly) converged on a toolchain for monitoring</center>

!SLIDE
# What is a metric?

* a name
* a value
* a timestamp, typically the UNIX epoch time
<br />

<center  style="font-size:2em;">
stats.haproxy.data_fao_org.request_duration   330 74857843</center>

<br />

!SLIDE 
# Collectd for system metrics
<center>
<img src="images/collectd-monitoring.svg"></img>
</center>

!SLIDE
# Collectd is good

* lightweight C daemon
* monitors continuously, not once every 5 minutes
* Best for OS-level metrics such as CPU, Disk, Memory, etc. 

!SLIDE
# What's Graphite?

* Time Series Database (Whisper)
* Rendering Engine 
* Dashboard (Graphite-Web)
* data relay and aggregation (Carbon)
<br />


!SLIDE
# Here is a taste
<br />
<center><img src="images/graphite-demo.png"></img></center>

<center  style="font-size:4em;">We'll come back to this later!</center>

!SLIDE
# Let's take a look at that JVM

<img src="images/jmxtrans.svg"></img>

!SLIDE
# JMXTrans

* Is just a connector for transporting JMX data
* No agent involved

!SLIDE
# What about those logs?

<img style="float:right;" src="image/images/logstash.png"></img>

<center  style="font-size:3em;">We don't only care about metrics, we also care about important
events.<br /><br /> Would be nice to scrape metrics from logs though.</center>

!SLIDE
# Show me the graphic already!

![logstash](images/logstash.svg)

!SLIDE
# Logstash can more than just ship logs

* Win
  * index by field
  * shape data
  * add new fields and tags to entries
  * Elasticsearch backend is awwwes0me

* Con - The agent isn't so light on resource usage

!SLIDE
# Logs don't have to be Ugly

![logstash](images/basic-kibana.png)

!SLIDE
# We can filter the data

![logstash](images/kibana-select-fields.png)

!SLIDE
# UNIX Tail in your browser

![logstash](images/kibana-tail.png)

!SLIDE
# Elasticsearch Rocks

* We can use [Lucene Parser
  Syntax](https://lucene.apache.org/core/old_versioned_docs/versions/3_5_0/queryparsersyntax.html)
  to construct queries
* Watch out though, don't use quotes, the 1st example here works, the
  second doesn't
<br />
<div style="font-size:2em;">status_code:40* AND request_header_host:*fao_org</div>
<br />
<br />
<div  style="font-size:2em;">status_code:"40*" AND request_header_host:"*fao_org"</div>

!SLIDE
# Listen

Be sure to listen to the FoodFightShow!

![Food Fight Show](images/foodfight_banner.png)


