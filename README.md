RHQ Metrics Openshift Cartridge
=====================

RHQ Metrics cartridge was designed to allow the project to run on a small gear.

### Default Deployment

To deploy RHQ Metrics on OpenShift run the following command:

`rhc app create [app-name] https://raw.githubusercontent.com/rhq-project/rhq-metrics-openshift/master/metadata/manifest.yml`


### Deployment Configuration

Available environment variables to configure the deployment:

```
OPENSHIFT_RHQ_METRICS_BACKEND
  - default: mem
  - supported: mem (for memory) and cass (for cassandra)
  
OPENSHIFT_RHQ_METRICS_VERSION
  - default: 0.2.5
  - supported: 0.2.5 and above

OPENSHIFT_CASSANDRA_VERSION
  - default: 2.1.1
  - supported: 2.1.1
  
OPENSHIFT_WILDFLY_VERSION
  - default: 8.1.0.Final
  - supported: 8.1.0.Final
```


### Sample Deployment with Options

To alter default configuration, use env option:

`rhc app create tester1 https://raw.githubusercontent.com/rhq-project/rhq-metrics-openshift/master/metadata/manifest.yml --env OPENSHIFT_RHQ_METRICS_BACKEND=cass OPENSHIFT_RHQ_METRICS_VERSION=0.2.5`


### Cartridge Details

Steps for cartridge setup:

1. Download and configure Cassandra to run with low memory
2. Download and configure Wildfly
3. Download and install RHQ Metrics applications: rest endpoint, core UI, and explorer UI

On cartridge start, the control scripts starts Cassandra and then Wildfly. Stop command does the reverse, stop Cassandra first and then Wildfly. 

Cassandra data is stored at `app-root/data/cassandra-data/`. Memory data is volatile.


### Notes

1. Scaling is not supported yet.
2. RHQ Metrics version 0.2.4 is supported only with memory data store.
