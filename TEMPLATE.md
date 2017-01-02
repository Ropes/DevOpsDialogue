This document exists to provide a template for documenting operational information about 
a service. The goal is to cover all of the bases so a reader can get a general understanding 
of the service and how to operate it.

The topics listed are a minimal starting point for documenting a service. Some won't be 
relevant, if so state why. Almost certainly some issues have been missed should be added 
to the template as they're discovered(<3 PRs).

#DevOps Dialogue Service Template 

# General Information 

Operational Context; What is the service accomplishing?

`Service Documentation Link`
 * Link to implmentation documentation
 
# Hosting Requirements
Per service basis
* CPU [Cores || Millicores]
* Memory Usage [MB || GB]
* Disk Storage [GB]
* Host
 * Type [VMs, Kubernetes, Stateful Hosts]
 * Naming criteria [Hostname[s,ranges], Kubernetes Pods, one-off "no touching" box name]

### Networking
* Network Utilization [1MBs <> 10MBs <> 100MBs > ]
* Firewall configurations [list]
* Outbound Connections [services, endpoints, etc]
  * Ports [list]
  * Load Balancers [list]
* Inbound Connections [services, endpoints exposed, etc]
  * Ports [list]
  * Load Balancers [list]

# Dependencies
Requirements for normal operation
* System Libraries [list]
* Local objects [files, data, keys, etc]

### Upstream 
Services which are required for this service to operate. [list]

### Downstream
Services impacted by a degraded status of this service. [list]

# Data Interaction
* Schemas which must be created in order to function[eg. BigTable Schemas, Elasticsearch mappings, Mongo Indexes, MySQL Create]
* Data Interaction [eg: BigTable, etcd, PubSub, Elasticsearch, Mongo, MySQL]
 * Read Data Sources [list]
 * Written Data Destinations [list]
* Data which is mutated by the service [list: Tables, Schemas, keys, etc]
* Ephemeral data created of concern?

# Logging
* Destination [local, greylog, syslog, etc]
* Searchability [linkto: Kibana, Logging Service X, ssh 'grep...']

# Metrics
* Destination [local, network[Graphite, Prometheus, Stackdriver, service X]]
* Searchability [linkto: Graphite, Stackdriver, etc]

# Configuration
Configuration requirements for the service
 * Config Files [list]
 * Network Configuration [list]
 * Encrypted Configuration(Access) [list]

# Build Operations
 * Build Process [CI, TravisCI, {Shame}dev machine bash] 
 * Packaging 
   * Artifact storage [GCS, S3, GCR, DockerHub, WebServiceX] 
   * Format [Tarball, Docker[rkt] Image, Raw Binary]

# Deployment Operations
 * Provisioning Mechanism [Kubernetes, Salt, Ansible, bash]
 * Service Manager [Systemd, Kubernetes, monit]
 * Alert Mechanism [Monit, Pod-sidecar, healthchecks]
 * Start/Upgrade Procedure [Pre/Post Requirements]
   * [Pre,Post]-Stop requirements
   * [Pre,Post]-Start requirements
 * Lifecycle
   * Time Period [24/7, hours, one-off job, CLI]

# Disaster Recovery
* Restart procedures:
 * Different from normal deployment?
 * Safe to let monitoring service automatically restart?
* If the service fails, what are the downstream effects? What(data) might be damaged? (Services which depend on it)
* Common errors which can arise; and how to resolve them (Update with bug links when they arise) [list]
* Network Partitions(they happen) [Suvival, Recovery steps]

* Rollback procedures.
* Service is unresponsive?
* Service/host exhausts all local storage?
 

* #### Distributed Processing  
 * Is it safe to stop one service but not all? If not why?
 * What to do when one service dies suddenly?
 * What to do if half the services die?
 * If a Host disappears for hours, what is the best course of action to handle its loss?

# Escalation. Who you gonna call? 
When it goes really pear shaped and questions aren't covered already?
Ultimate source of truth? Master of the silo?

This document was originally started in a [gist](https://gist.github.com/Ropes/53363f61a626a181a331)
