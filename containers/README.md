# rsyslogd ubi container to output syslog protocol to stdout

This container can be used as a destination output for embedded fluentd use in OpenShift ClusterLogging operator.

With appropriate configuration, it is possible to output all container outputs in a project to a single syslog server.

## Build the container

```bash
export REGISTRY=<your registry>
export RSYSLOG_VERSION=8.2102
podman build --no-cache --rm -t ${REGISTRY}/ubi-rsyslogd:${RSYSLOG_VERSION} -f Containerfile .
podman push ${REGISTRY}/ubi-rsyslogd:${RSYSLOG_VERSION}
```


## Test it

Run the containerized version of rsyslogd daemon.

```bash
podman run -ti -p 10514:10514 ${REGISTRY}/ubi-rsyslogd:${RSYSLOG_VERSION}
```

Then in another terminal use logger to validate that rsyslod server can receive logs and output them to stdout

```
logger --tcp --port 10514 -n localhost --socket-errors=off hello
```

```bash
$ podman run -ti -p 10514:10514 ${REGISTRY}/ubi-rsyslogd:${RSYSLOG_VERSION}
rsyslogd 8.2102.0-5.el8: running as pid 1, enabling container-specific defaults, press ctl-c to terminate rsyslog
rsyslogd: cannot create '/var/run/rsyslog/dev/log': No such file or directory [v8.2102.0-5.el8 try https://www.rsyslog.com/e/2176 ]
rsyslogd: cannot create '/var/run/rsyslog/dev/log': No such file or directory [v8.2102.0-5.el8 try https://www.rsyslog.com/e/2176 ]
rsyslogd: imuxsock does not run because we could not aquire any socket  [v8.2102.0-5.el8]
rsyslogd: activation of module imuxsock failed [v8.2102.0-5.el8]
2022-01-17T17:06:13.887501+01:00 hz-02.clustership.com phuet hello
```
