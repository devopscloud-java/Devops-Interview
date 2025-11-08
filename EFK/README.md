In DevOps, EFK refers to a logging stack used to collect, process, and visualize logs from applications and infrastructure. It is widely used in cloud-native and containerized environments like Kubernetes.

EFK stands for:

Elasticsearch

A distributed search and analytics engine.

Stores logs and allows querying and indexing large volumes of data quickly.

Fluentd

A log collector and forwarder.

Collects logs from different sources (containers, applications, servers) and sends them to Elasticsearch.

Can also filter, transform, and route logs.

Kibana

A visualization and dashboard tool.

Connects to Elasticsearch to display logs in an interactive, user-friendly way.

Helps monitor system/application health and troubleshoot issues.

How it works in a Kubernetes/DevOps setup:

Fluentd runs on each node (or as a DaemonSet in Kubernetes) and collects logs from containers.

Logs are sent to Elasticsearch, which indexes and stores them.

Kibana reads from Elasticsearch and provides dashboards, search, and analytics.

Why EFK is important in DevOps:

Centralizes logs from multiple sources.

Helps monitor and debug microservices or distributed applications.

Enables alerting and proactive issue resolution.

Scales well in containerized environments.

💡 Note: Sometimes you’ll see ELK stack instead of EFK, where Logstash replaces Fluentd as the log shipper. Fluentd is lighter and preferred in Kubernetes setups.
