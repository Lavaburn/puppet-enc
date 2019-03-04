Puppet External Node Classifer
=========================

Puppet-enc is a external node classifier for puppet. The classification file itself is a standard yaml file
	
	--- 
	groups: 
	  group1:
	    environment: testing
	    classes:
	      myclass1: {}
	    parameters:
	      param1: value1
	  group2:
	    parent: group1
	    parameters:
	      param3: value3
	  default: 
	    classes: {} 
	    parameters: {}
	nodes: 
	  host1.mydomain.com: 
	    environment: development 
	    parameters:
	      param2: value2
	    classes: 
	      myclass2: {}
	  host2.mydomain.com: 
	    parameters:
	      param1: value1b
	    group: group2
	              
All the nodes are enclosed in the nodes array. Hosts not added will get data from the "default" group! 
Group data will be merged recursively (Deep merge not supported!) from the parent down.


bin/classify.rb
===============

The classifier comes classify.rb; example usage

    :puppet.conf

    [main]
      # The Puppet log directory.
      # The default value is '$vardir/log'.
      logdir = /var/log/puppet

      # Where Puppet PID files are kept.
      # The default value is '$vardir/run'.
      rundir = /var/run/puppet

      # Where SSL certificates are kept.
      # The default value is '$confdir/ssl'.
      ssldir = $vardir/ssl

      node_terminus  = exec
      external_nodes = /etc/puppet/bin/classify.rb -q -H

Command line;

    # classify.rb -H myhost.fqdn


