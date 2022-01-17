# ClusterLogging deployment resources

Store these resources to be reused in future deployment.

Will try to put some examples of ClusterLogging instance configuration and ClusterLogForwarder configuration for specific case.

## Install ClusterLogging operator

You can install the OpenShift ClusterLogging operator using the resources definition from the resources directory.

```bash
oc apply -f resources
```


## Forward namespace pods output to rsyslogd server using ClusterLogging operator ClusterLogForwarder

Look at the examples folder.


# TODO

- build an ansible playbook to manage upgrade of versions
