FINAL UPDATE
============

The last version of the code is here (still a bit buggy): https://null.53bits.co.uk/uploads/programming/php/smoketrace/smoketrace-2013-11.tar.gz

A read-only version of the last version is here: http://smoketrace.53bits.co.uk/smoketrace/testing/

This project was abandoned due to time commitments. I strongly recommend you write something new using InfluxDB, MySQL is no good for this type of data storage.




SmokeTrace
==========


Description:

    Traceroute sourced monitoring with graphing and reporting.
    
    SmokeTrace records a path and assosicated statistics (IPs,
    number of hops, delay at each hop etc) to a destination.
    Criteria is then assigned to this path and alerts are generated
    for path changes such as hop or delay increases as defined by
    the alerting criteria.
    
    This is not related to the SmokePing plugin Smoketrace (which
    was removed in SmokePing 2.5.0 as per these release notes
    http://oss.oetiker.ch/smokeping/pub/CHANGES).


![Alt text](https://null.53bits.co.uk/uploads/programming/php/smoketrace/Smoketrace1.png "SmokeTrace Screenshot")

Why was it Made:  

    A similar concept to the infamous and brilliant SmokePing 
    (http://smokeping.org/), but with traceroute!
    
    Every time I receive a SmokePing alert the first thing I do is run
    traceroute/mtr/etc to see where in the path the loss is occurring.
    If regular traceroutes where being run I could alert on this instead.
              

What is it used for:

    SmokePing alerts are latency triggered events, SmokeTrace alerts are path
    triggered events.
    
    Future versions could incorporate latency monitoring and MTU monitoring to
    bring this into one tool although I think it's best to keep them separate.
    SmokePing could be extended to include other OWAMPs so the two tools'
    become more specialised in their respective fields and should aim to
    complement each other, not conflict.


Technical details:

    * Written in PHP for Linux (it maybe altered at a later date to support
    other operating systems, unsure as yet)
    * Uses MySQL as back end not RRD files (testing will commence on MariaDB
    soon, unsure of other DB support as yet)
    * Still in alpha, so no public beta code release as yet, Q1-2014!
    * The alpha release looks similar to this, which will hopefully be improved
    upon in time for the beta release: http://goo.gl/K8NjCo
    
    
Development Plan:

    Initial release (Q1/Q2 2014) will be the completed web interface and MySQL 
    DB running "traceroutes" to a given destination using one of a
    possibility of methods (calling the native Linux traceroute binary in either
    UDP or ICMP mode, calling the MTR binary using ICMP, or the tcptraceroute
    binary). The output is formatted for storing the MySQL DB and path changes
    can be alerted on (a basic proof of concept release but at this stage the
    alerting won't be reliable using traceroute alone).
    
    After the initial release the next stage will integrate BGP. SmokeTrace
    will take a BGP feed and then cross-examine route changes from BGP with
    traceroute path changes. We can also factor in latency changes from the
    traceroute output. Together they pose the question:
    Was the path update received "worse" than the previous path?
    We can create alerting criteria then to make the alerting accurate
    (higher latency, longer path, more packet loss etc).
    
    The final step after routing integration is automatic traceroute destination
    generation (take BGP top hosts or NetFlow top hosts for example and
    automatically use them to populate SmokeTrace with new traceroute targets).
    At this point SmokeTrace will be considered out of beta and in version 
    "1.0 stable".


Who made it:

    James Bensley <jwbensley@gmail.com>
