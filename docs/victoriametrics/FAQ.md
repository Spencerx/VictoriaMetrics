---
weight: 24
title: FAQ
menu:
  docs:
    parent: 'victoriametrics'
    weight: 24
tags:
  - metrics
aliases:
- /FAQ.html
- /faq.html
- /faq/index.html
- /faq/
---
## What is the main purpose of VictoriaMetrics?

To be the best tool for monitoring and observability.

## Who uses VictoriaMetrics?

See [case studies](https://docs.victoriametrics.com/victoriametrics/casestudies/) and [articles](https://docs.victoriametrics.com/victoriametrics/articles).

## Which features does VictoriaMetrics have?

See the full list of [Prominent Features](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#prominent-features).

## Are there performance comparisons with other solutions?

Yes. See [these benchmarks](https://docs.victoriametrics.com/victoriametrics/articles/#benchmarks).

## How to start using VictoriaMetrics?

Follow the [Quick Start guide](https://docs.victoriametrics.com/victoriametrics/quick-start/).

## How to contribute to VictoriaMetrics?

See the [Contributing](https://docs.victoriametrics.com/victoriametrics/contributing/) guide.

## Does VictoriaMetrics support high availability?

Yes. Learn more in the High Availability docs for both [single-node](https://docs.victoriametrics.com/victoriametrics/#high-availability)
and [cluster](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#high-availability) setups.

## Does VictoriaMetrics support replication?

Yes. See [Replication and data safety](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#replication-and-data-safety) for details.

## What are scalability limits of VictoriaMetrics?

The single-node version scales vertically. It can handle up to 100 million [active time series](https://docs.victoriametrics.com/victoriametrics/faq/#what-is-an-active-time-series)
and 2 million samples per second (based on real usage).

The cluster version scales both vertically and horizontally. It can handle billions of [active time series](https://docs.victoriametrics.com/victoriametrics/faq/#what-is-an-active-time-series)
and hundreds of millions of samples per second (based on real usage).

See [performance comparison with other solutions](https://docs.victoriametrics.com/victoriametrics/faq/#are-there-performance-comparisons-with-other-solutions).

## Can I use VictoriaMetrics instead of Prometheus?

Yes, in most cases. VictoriaMetrics can substitute Prometheus in the following aspects:

* Prometheus-compatible service discovery and scraping via [vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/) and single-node VictoriaMetrics. 
  See [How to scrape Prometheus exporters such as node-exporter](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-scrape-prometheus-exporters-such-as-node-exporter).
* Prometheus-compatible alerting and recording rules via [vmalert](https://docs.victoriametrics.com/victoriametrics/vmalert/).
* Prometheus-compatible querying in Grafana. See [integrations/Grafana](https://docs.victoriametrics.com/victoriametrics/integrations/grafana/).

## What is the difference between vmagent and Prometheus?

While both [vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/) and Prometheus may scrape Prometheus targets (aka `/metrics` pages),
read Prometheus-compatible [scrape configs](https://docs.victoriametrics.com/victoriametrics/sd_configs/#scrape_configs)
and send data to multiple remote storage systems, vmagent has the following additional features:

* vmagent usually requires less CPU, RAM and disk IO compared to Prometheus when scraping an enormous number of targets (more than 1000)
  or targets with a great number of exposed metrics.
* vmagent provides independent [disk-backed buffers](https://docs.victoriametrics.com/victoriametrics/vmagent/#calculating-disk-space-for-persistence-queue) for each configured remote storage (see `-remoteWrite.url`).
  This means that slow or temporarily unavailable storage doesn't prevent it from sending data to healthy storage in parallel. 
  Prometheus uses a single shared buffer for all the configured remote storage systems (see `remote_write->url`) with a hardcoded retention of 2 hours.
* vmagent can accept, relabel, filter and aggregate data obtained via multiple data ingestion protocols in addition to data scraped from Prometheus targets.
  That means it supports both [pull](https://docs.victoriametrics.com/victoriametrics/keyconcepts/#pull-model) and [push](https://docs.victoriametrics.com/victoriametrics/keyconcepts/#push-model) protocols for data ingestion.
  See [these docs](https://docs.victoriametrics.com/victoriametrics/vmagent/#features) for details.
* vmagent can be used in different [use cases](https://docs.victoriametrics.com/victoriametrics/vmagent/#use-cases):
  * [IoT and edge monitoring](https://docs.victoriametrics.com/victoriametrics/vmagent/#iot-and-edge-monitoring)
  * [Drop-in replacement for Prometheus](https://docs.victoriametrics.com/victoriametrics/vmagent/#drop-in-replacement-for-prometheus)
  * [Statsd alternative](https://docs.victoriametrics.com/victoriametrics/vmagent/#statsd-alternative)
  * [Flexible metrics relay](https://docs.victoriametrics.com/victoriametrics/vmagent/#flexible-metrics-relay)
  * [Replication and high availability](https://docs.victoriametrics.com/victoriametrics/vmagent/#replication-and-high-availability)
  * [Sharding among remote storages](https://docs.victoriametrics.com/victoriametrics/vmagent/#sharding-among-remote-storages)
  * [Relabeling and filtering](https://docs.victoriametrics.com/victoriametrics/vmagent/#relabeling-and-filtering)
  * [Splitting data streams among multiple systems](https://docs.victoriametrics.com/victoriametrics/vmagent/#splitting-data-streams-among-multiple-systems)
  * [Prometheus remote_write proxy](https://docs.victoriametrics.com/victoriametrics/vmagent/#prometheus-remote_write-proxy)
  * [Remote_write for clustered version](https://docs.victoriametrics.com/victoriametrics/vmagent/#remote_write-for-clustered-version)

## What is the difference between vmagent and Prometheus agent?

Both [vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/) and [Prometheus agent](https://prometheus.io/blog/2021/11/16/agent/) 
serve the same purpose – to efficiently scrape Prometheus-compatible targets at the edge. They have the following differences:

* vmagent usually requires less CPU, RAM and disk IO compared to the Prometheus agent. See [comparsion of metrics collection agents](https://victoriametrics.com/blog/opentelemetry-prometheus-and-more/).
* vmagent supports both [pull](https://docs.victoriametrics.com/victoriametrics/keyconcepts/#pull-model) and [push](https://docs.victoriametrics.com/victoriametrics/keyconcepts/#push-model) 
  data collection – it can accept data via many popular data ingestion protocols such as InfluxDB line protocol, Graphite protocol, OpenTSDB protocol, DataDog protocol, Prometheus protocol, OpenTelemetry metrics protocol, CSV and JSON – see [these docs](https://docs.victoriametrics.com/victoriametrics/vmagent/#features).
* vmagent doesn't have limitations on backfilling of historical data.
* vmagent can easily scale horizontally to multiple instances for scraping a big number of targets – see [Scraping big number of targets](https://docs.victoriametrics.com/victoriametrics/vmagent/#scraping-big-number-of-targets) docs.
* vmagent supports [improved relabeling](https://docs.victoriametrics.com/victoriametrics/relabeling/).
* vmagent can limit the number of scraped metrics per target – see [these docs](https://docs.victoriametrics.com/victoriametrics/vmagent/#cardinality-limiter).
* vmagent supports loading scrape configs from multiple files – see [these docs](https://docs.victoriametrics.com/victoriametrics/vmagent/#loading-scrape-configs-from-multiple-files).
* vmagent supports data reading and data writing from/to Kafka – see [these docs](https://docs.victoriametrics.com/victoriametrics/vmagent/#kafka-integration).
* vmagent has better remote write compression to reduce transferred traffic - [these docs](https://docs.victoriametrics.com/victoriametrics/vmagent/#victoriametrics-remote-write-protocol).
* vmagent can read and update scrape configs from http and https URLs, while the Prometheus agent can only read them from the local file system.
* vmagent supports [stream aggregation](https://docs.victoriametrics.com/victoriametrics/stream-aggregation/) for performing aggregates on collected or received samples before sending them to remote storage.

## Is it safe to enable [remote write](https://prometheus.io/docs/operating/integrations/#remote-endpoints-and-storage) in Prometheus?

Yes. Prometheus continues writing data to local storage after enabling remote write, so all the existing local storage data
and new data is available for querying via Prometheus as usual.

It is recommended using [vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/) for scraping Prometheus targets
and writing data to VictoriaMetrics.

## How does VictoriaMetrics compare to other remote storage solutions for Prometheus such as [M3DB](https://github.com/m3db/m3), [Thanos](https://github.com/thanos-io/thanos), [Cortex](https://github.com/cortexproject/cortex), [Mimir](https://github.com/grafana/mimir), etc.?

* VictoriaMetrics is easier to configure and operate than competing solutions.
* VictoriaMetrics is more cost-efficient, since it requires less RAM, disk space, disk IO and network IO than competing solutions.
* VictoriaMetrics performs typical queries faster than competing solutions.
* VictoriaMetrics has a simpler architecture, which translates into fewer bugs and more useful features compared to competing time series databases.

The following articles and talks provide additional details:

* [Comparing Thanos to VictoriaMetrics cluster](https://medium.com/@valyala/comparing-thanos-to-victoriametrics-cluster-b193bea1683)
* [Remote Write Storage Wars](https://promcon.io/2019-munich/talks/remote-write-storage-wars/) talk
  from [PromCon 2019](https://promcon.io/2019-munich/talks/remote-write-storage-wars/)
* [Grafana Mimir and VictoriaMetrics: performance tests](https://victoriametrics.com/blog/mimir-benchmark/)
* [VictoriaMetrics: scaling to 100 million metrics per second](https://www.slideshare.net/NETWAYS/osmc-2022-victoriametrics-scaling-to-100-million-metrics-per-second-by-aliaksandr-valialkin)

VictoriaMetrics also [uses less RAM than Thanos components](https://github.com/thanos-io/thanos/issues/448).

## What is the difference between VictoriaMetrics and [QuestDB](https://questdb.io/)?

* QuestDB needs 20x more storage space than VictoriaMetrics. This translates to higher storage costs and slower queries over historical data, which must be read from the disk.
* QuestDB is significantly more difficult to set up and operate than VictoriaMetrics. Compare [setup instructions for QuestDB](https://questdb.io/docs/get-started/binaries) to [setup instructions for VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-start-victoriametrics).
* VictoriaMetrics provides the [MetricsQL](https://docs.victoriametrics.com/victoriametrics/metricsql/) query language, which is better suited for typical queries over time series data than the SQL-like query language provided by QuestDB. See [this article](https://valyala.medium.com/promql-tutorial-for-beginners-9ab455142085) for details.
* VictoriaMetrics can be queried via the [Prometheus querying API](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#prometheus-querying-api-usage) and via [Graphite's API](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#graphite-api-usage).
* Thanks to PromQL support, VictoriaMetrics [can be used as a drop-in replacement for Prometheus in Grafana](https://docs.victoriametrics.com/victoriametrics/integrations/grafana/), while QuestDB needs a full rewrite of existing dashboards in Grafana.
* Thanks to Prometheus' remote_write API support, VictoriaMetrics can be used as long-term storage for Prometheus or [vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/), while QuestDB does not integrate with Prometheus.
* QuestDB [supports a smaller range of popular data ingestion protocols](https://questdb.io/docs/develop/insert-data) compared to VictoriaMetrics (compare to [the list of supported data ingestion protocols for VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-import-time-series-data)).
* [VictoriaMetrics supports backfilling (e.g. storing historical data) out of the box](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#backfilling), while QuestDB provides [very limited support for backfilling](https://questdb.io/blog/2021/05/10/questdb-release-6-0-tsbs-benchmark#the-problem-with-out-of-order-data).

## What is the difference between VictoriaMetrics and [Grafana Mimir](https://github.com/grafana/mimir)?

Grafana Mimir is a [Cortex](https://github.com/cortexproject/cortex) fork, so it has the same differences
as Cortex. See [what is the difference between VictoriaMetrics and Cortex](#what-is-the-difference-between-victoriametrics-and-cortex).

See also [Grafana Mimir vs VictoriaMetrics benchmark](https://victoriametrics.com/blog/mimir-benchmark/).

## What is the difference between VictoriaMetrics and [Cortex](https://github.com/cortexproject/cortex)?

VictoriaMetrics is similar to Cortex in the following aspects:

* Both systems accept data from [vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/) or Prometheus
  via the standard [remote_write API](https://prometheus.io/docs/practices/remote_write/), so there is no need to run sidecars,
  unlike in [Thanos](https://github.com/thanos-io/thanos)' case.
* Both systems support multi-tenancy out of the box. See [the corresponding docs for VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#multitenancy).
* Both systems support data replication. See [replication in Cortex](https://github.com/cortexproject/cortex/blob/fe56f1420099aa1bf1ce09316c186e05bddee879/docs/architecture.md#hashing) and [replication in VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#replication-and-data-safety).
* Both systems scale horizontally to multiple nodes. See [these docs](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#cluster-resizing-and-scalability) for details.
* Both systems support alerting and recording rules via corresponding tools such as [vmalert](https://docs.victoriametrics.com/victoriametrics/vmalert/).
* Both systems can be queried via the [Prometheus querying API](https://prometheus.io/docs/prometheus/latest/querying/api/) and integrate perfectly with Grafana.

The main differences between Cortex and VictoriaMetrics:

* Cortex reuses Prometheus source code, while VictoriaMetrics is written from scratch.
* Cortex heavily relies on third-party services such as Consul, Memcache, DynamoDB, BigTable, Cassandra, etc.
  This may increase operational complexity and reduce system reliability compared to VictoriaMetrics' case,
  which doesn't use any external services. Compare [Cortex' Architecture](https://github.com/cortexproject/cortex/blob/master/docs/architecture.md)
  to [VictoriaMetrics' architecture](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#architecture-overview).
* VictoriaMetrics provides [production-ready single-node solution](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/),
  which is much easier to set up and operate than a Cortex cluster.
* Cortex can lose up to 12 hours of recent data on Ingestor failure – see [the corresponding docs](https://github.com/cortexproject/cortex/blob/fe56f1420099aa1bf1ce09316c186e05bddee879/docs/architecture.md#ingesters-failure-and-data-loss).
  VictoriaMetrics may lose only a few seconds of recent data, which hasn't been synced to persistent storage yet.
  See [this article for details](https://medium.com/@valyala/wal-usage-looks-broken-in-modern-time-series-databases-b62a627ab704).
* Cortex is usually slower and requires more CPU and RAM than VictoriaMetrics. See [this talk from adidas at PromCon 2019](https://promcon.io/2019-munich/talks/remote-write-storage-wars/) and [other case studies](https://docs.victoriametrics.com/victoriametrics/casestudies/).
* VictoriaMetrics accepts data in multiple popular data ingestion protocols in addition to Prometheus remote_write protocol – InfluxDB, OpenTSDB, Graphite, CSV, JSON, native binary.
  See [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-import-time-series-data) for details.
* VictoriaMetrics provides the [MetricsQL](https://docs.victoriametrics.com/victoriametrics/metricsql/) query language, while Cortex provides the [PromQL](https://prometheus.io/docs/prometheus/latest/querying/basics/) query language.
* VictoriaMetrics can be queried via [Graphite's API](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#graphite-api-usage).

## What is the difference between VictoriaMetrics and [Thanos](https://github.com/thanos-io/thanos)?

* Thanos reuses Prometheus source code, while VictoriaMetrics is written from scratch.
* VictoriaMetrics accepts data via the [standard remote_write API for Prometheus](https://prometheus.io/docs/practices/remote_write/),
  while Thanos uses a non-standard [sidecar](https://github.com/thanos-io/thanos/blob/master/docs/components/sidecar.md) which must run alongside each Prometheus instance.
* The Thanos sidecar requires disabling data compaction in Prometheus, which may hurt Prometheus performance and increase RAM usage. See [these docs](https://thanos.io/tip/components/sidecar.md/) for more details.
* Thanos stores data in object storage (Amazon S3 or Google GCS), while VictoriaMetrics stores data in block storage
  ([GCP persistent disks](https://cloud.google.com/compute/docs/disks#pdspecs), Amazon EBS or bare metal HDD).
  While object storage is usually less expensive, block storage provides much lower latencies and higher throughput.
  VictoriaMetrics works perfectly with HDD-based block storage – which eliminates the need for using more expensive SSD or NVMe disks in most cases.
* Thanos can lose up to 2 hours of recent data, which hasn't been uploaded yet to object storage yet. VictoriaMetrics may lose only a few seconds of recent data,
  which hasn't been synced to persistent storage yet. See [this article for details](https://medium.com/@valyala/wal-usage-looks-broken-in-modern-time-series-databases-b62a627ab704).
* VictoriaMetrics provides a [production-ready single-node solution](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/),
  which is much easier to set up and operate than Thanos components.
* Compared to VictoriaMetrics, Thanos has more moving parts and relies more heavily on stable network connections, which can make it trickier to set up and operate.
  See [this article for details](https://medium.com/faun/comparing-thanos-to-victoriametrics-cluster-b193bea1683).
* Thanos is usually slower and requires more CPU and RAM than VictoriaMetrics. See [this talk from adidas at PromCon 2019](https://promcon.io/2019-munich/talks/remote-write-storage-wars/).
* VictoriaMetrics accepts data via multiple popular data ingestion protocols in addition to the Prometheus remote_write protocol – InfluxDB, OpenTSDB, Graphite, CSV, JSON, native binary.
  See [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-import-time-series-data) for details.
* VictoriaMetrics provides the [MetricsQL](https://docs.victoriametrics.com/victoriametrics/metricsql/) query language, while Thanos provides the [PromQL](https://prometheus.io/docs/prometheus/latest/querying/basics/) query language.
* VictoriaMetrics can be queried via [Graphite's API](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#graphite-api-usage).

## How does VictoriaMetrics compare to [InfluxDB](https://www.influxdata.com/time-series-platform/influxdb/)?

* VictoriaMetrics requires [10x less RAM](https://medium.com/@valyala/insert-benchmarks-with-inch-influxdb-vs-victoriametrics-e31a41ae2893) and it [works faster](https://medium.com/@valyala/measuring-vertical-scalability-for-time-series-databases-in-google-cloud-92550d78d8ae).
* VictoriaMetrics uses less storage space than InfluxDB for production data.
* VictoriaMetrics doesn't support InfluxQL or Flux, but provides a better query language – [MetricsQL](https://docs.victoriametrics.com/victoriametrics/metricsql/). See [this tutorial](https://medium.com/@valyala/promql-tutorial-for-beginners-9ab455142085) for details.
* VictoriaMetrics accepts data in multiple popular data ingestion protocols in addition to InfluxDB – Prometheus remote_write, OpenTSDB, Graphite, CSV, JSON, native binary.
  See [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-import-time-series-data) for details.
* VictoriaMetrics can be queried via [Graphite's API](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#graphite-api-usage).

See [How to migrate from InfluxDB to VictoriaMetrics](https://docs.victoriametrics.com/guides/migrate-from-influx/).

## How does VictoriaMetrics compare to [TimescaleDB](https://www.timescale.com/)?

* TimescaleDB insists on using SQL as a query language. While SQL is more powerful than PromQL, this power is rarely required during typical usages of a TSDB. Real-world queries usually [look clearer and simpler when written in PromQL than in SQL](https://medium.com/@valyala/promql-tutorial-for-beginners-9ab455142085).
* VictoriaMetrics requires [up to 70x less storage space compared to TimescaleDB](https://medium.com/@valyala/when-size-matters-benchmarking-victoriametrics-vs-timescale-and-influxdb-6035811952d4) for storing the same amount of time series data. The gap in storage space usage can be decreased from 70x to 3x if [compression in TimescaleDB is properly configured](https://docs.timescale.com/use-timescale/latest/compression/) (it isn't an easy task in general :)).
* VictoriaMetrics requires up to 10x less CPU and RAM resources than TimescaleDB for processing production data. See [this article](https://abiosgaming.com/press/high-cardinality-aggregations/) for details.
* TimescaleDB is [harder to set up, configure and operate](https://docs.timescale.com/timescaledb/latest/how-to-guides/install-timescaledb/self-hosted/ubuntu/installation-apt-ubuntu/) than VictoriaMetrics (see [how to run VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-start-victoriametrics)).
* VictoriaMetrics accepts data in multiple popular data ingestion protocols – InfluxDB, OpenTSDB, Graphite, CSV – while TimescaleDB supports only SQL inserts.
* VictoriaMetrics can be queried via [Graphite's API](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#graphite-api-usage).

## Does VictoriaMetrics use Prometheus technologies like other clustered TSDBs built on top of Prometheus such as [Thanos](https://github.com/thanos-io/thanos) or [Cortex](https://github.com/cortexproject/cortex)?

No. VictoriaMetrics core is written in Go from scratch by [fasthttp](https://github.com/valyala/fasthttp)'s [author](https://github.com/valyala).
The architecture is [optimized for storing and querying large amounts of time series data with high cardinality](https://medium.com/devopslinks/victoriametrics-creating-the-best-remote-storage-for-prometheus-5d92d66787ac). VictoriaMetrics storage uses [certain ideas from ClickHouse](https://medium.com/@valyala/how-victoriametrics-makes-instant-snapshots-for-multi-terabyte-time-series-data-e1f3fb0e0282). Special thanks to [Alexey Milovidov](https://github.com/alexey-milovidov).

## What is the pricing for VictoriaMetrics?

The following versions are open source and free:

* [Single-node version](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/).
* [Cluster version](https://github.com/VictoriaMetrics/VictoriaMetrics/tree/cluster).

We provide commercial support for both versions. [Contact us](https://victoriametrics.com/contact-us/) for pricing.

[VictoriaMetrics Cloud](https://console.victoriametrics.cloud/signUp?utm_source=website&utm_campaign=docs_vm_faq) – the most cost-efficient hosted monitoring platform, operated by VictoriaMetrics core team.

## Why doesn't VictoriaMetrics support the [Prometheus remote read API](https://prometheus.io/docs/prometheus/latest/configuration/configuration/#%3Cremote_read%3E)?

The remote read API requires transferring all the raw data for all the requested metrics over the given time range. For instance,
if a query covers 1000 metrics with 10K values each, then the remote read API has to return `1000*10K`=10M metric values to Prometheus.
This is slow and expensive.
Prometheus' remote read API isn't intended for querying foreign data – aka `global query view`. See [this issue](https://github.com/prometheus/prometheus/issues/4456) for details.

Instead, query VictoriaMetrics directly via [vmui](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#vmui), 
the [Prometheus Querying API](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#prometheus-querying-api-usage)
or via [Prometheus datasource in Grafana](https://docs.victoriametrics.com/victoriametrics/integrations/grafana/).

## Does VictoriaMetrics deduplicate data from Prometheus instances scraping the same targets (aka `HA pairs`)?

Yes. See [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#deduplication) for details.

## Where is the source code of VictoriaMetrics?

Source code for Victoriametrics can be found in the following locations:

* [Single-node version](https://github.com/VictoriaMetrics/VictoriaMetrics)
* [Cluster version](https://github.com/VictoriaMetrics/VictoriaMetrics/tree/cluster)

## Is VictoriaMetrics a good fit for data from IoT sensors and industrial sensors?

VictoriaMetrics is able to handle data from hundreds of millions of IoT sensors and industrial sensors.
It supports [high cardinality data](https://medium.com/@valyala/high-cardinality-tsdb-benchmarks-victoriametrics-vs-timescaledb-vs-influxdb-13e6ee64dd6b),
perfectly [scales up on a single node](https://medium.com/@valyala/measuring-vertical-scalability-for-time-series-databases-in-google-cloud-92550d78d8ae)
and scales horizontally to multiple nodes.

## What is the difference between single-node and cluster versions of VictoriaMetrics?

Both the [single-node](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/) and
[cluster](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/) versions of VictoriaMetrics are built 
on the same core code, so they share many features. That said, here are the key differences between them:

* The [single-node VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/) runs on a single host,
  while [cluster version of VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/) can scale to many hosts.
  The single-node VictoriaMetrics can scale vertically, e.g. its capacity and performance scales almost linearly when increasing
  available CPU, RAM, disk IO and disk space. See [an article about vertical scalability of a single-node VictoriaMetrics](https://valyala.medium.com/measuring-vertical-scalability-for-time-series-databases-in-google-cloud-92550d78d8ae).

* The cluster version of VictoriaMetrics supports [multitenancy](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#multitenancy),
  but single-node VictoriaMetrics does not.

* The cluster version of VictoriaMetrics supports data replication, while single-node VictoriaMetrics relies on the durability
  of the persistent storage pointed by the `-storageDataPath` command-line flag.
  See [these docs](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#replication-and-data-safety) for details.

* The single-node version of VictoriaMetrics delivers higher capacity and performance than the cluster version when 
  running on the same hardware with equal CPU and RAM, as it avoids the overhead of network data transfers between cluster components.

See also [which type of VictoriaMetrics is recommended to use](#which-victoriametrics-type-is-recommended-for-use-in-production---single-node-or-cluster).

## Where can I ask questions about VictoriaMetrics?

Questions about VictoriaMetrics can be asked via the following channels:

* [Slack Inviter](https://slack.victoriametrics.com/) and [Slack channel](https://victoriametrics.slack.com/)
* [Telegram channel](https://t.me/VictoriaMetrics_en)

See the full list of [community channels](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#community-and-contributions).

## Where can I file bugs and feature requests regarding VictoriaMetrics?

File bugs and feature requests [here](https://github.com/VictoriaMetrics/VictoriaMetrics/issues).

## Where can I find information about multi-tenancy?

See [these docs](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#multitenancy). Multitenancy is supported only by the [cluster version](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/) of VictoriaMetrics.

## How to set a memory limit for VictoriaMetrics components?

All VictoriaMetrics components provide command-line flags to control the size of internal buffers and caches: 
`-memory.allowedPercent` and `-memory.allowedBytes` (pass `-help` to any VictoriaMetrics component in order to see the description for these flags). 
These limits don't take into account additional memory, which may be needed for processing incoming queries. 
Hard limits may be enforced only by the OS via [cgroups](https://en.wikipedia.org/wiki/Cgroups), 
Docker (see [these docs](https://docs.docker.com/config/containers/resource_constraints)) or 
Kubernetes (see [these docs](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers)).

Memory usage for VictoriaMetrics components can be tuned according to the following docs:

* [Resource usage limits for single-node VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#resource-usage-limits)
* [Resource usage limits for cluster VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#resource-usage-limits)
* [Troubleshooting for vmagent](https://docs.victoriametrics.com/victoriametrics/vmagent/#troubleshooting)
* [Troubleshooting for single-node VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#troubleshooting)

## How can I run VictoriaMetrics on FreeBSD/OpenBSD?

VictoriaMetrics is included in [OpenBSD](https://github.com/openbsd/ports/blob/c1bfea520bbb30d6e5f8d0f09115ace341f820d6/infrastructure/db/user.list#L383)
and [FreeBSD](https://www.freebsd.org/cgi/ports.cgi?query=victoria&stype=all) ports so just install it from there
or use pre-built binaries from [releases page](https://github.com/VictoriaMetrics/VictoriaMetrics/releases/latest).

## Does VictoriaMetrics support the Graphite query language?

Yes. See [these docs](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#graphite-api-usage).

## What is an active time series?

A time series is uniquely identified by its name plus a set of its labels. For example, `temperature{city="NY",country="US"}` and `temperature{city="SF",country="US"}`
are two distinct series, since they differ by the `city` label. A time series is considered active if it received at least a single sample during the last hour.
The number of active time series is displayed on the official Grafana dashboard for VictoriaMetrics - see [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#monitoring) for details.

## What is high churn rate?

If old time series are constantly substituted by new time series at a high rate, then such a state is called `high churn rate`. High churn rate has the following negative consequences:

* Increased total number of time series stored in the database.
* Increased size of inverted index, which is stored at `<-storageDataPath>/indexdb`, since the inverted index contains entries for every label of every time series with at least a single ingested sample.
* Slow-down of queries over multiple days.

The main reason for high churn rate is a metric label with frequently changed value. Examples of such labels:

* `queryid`, which changes with each query at `postgres_exporter`.
* `pod`, which changes with each new deployment in Kubernetes.
* A label derived from the current time such as `timestamp`, `minute` or `hour`.
* A `hash` or `uuid` label, which changes frequently.

The solution against high churn rate is to identify and eliminate labels with frequently changed values.
[Cardinality explorer](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#cardinality-explorer) can help determining these labels. If labels can't be removed, try pre-aggregating data
before it gets ingested into database with [stream aggregation](https://docs.victoriametrics.com/victoriametrics/stream-aggregation/).

The official Grafana dashboards for VictoriaMetrics contain graphs for churn rate - see [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#monitoring) for details.

## What is high cardinality?

High cardinality usually means a high number of [active time series](#what-is-an-active-time-series). High cardinality may lead to high memory usage
and/or to a high percentage of [slow inserts](#what-is-a-slow-insert). The source of high cardinality is usually a label with
a large number of unique values, which presents a big share of the ingested time series. Examples of such labels:

* `user_id`
* `url`
* `ip`

The solution is to identify and remove the source of high cardinality with the help of [cardinality explorer](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#cardinality-explorer).

The official Grafana dashboards for VictoriaMetrics contain graphs, which show the number of active time series -
see [these docs](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#monitoring) for details.

## What is a slow insert?

VictoriaMetrics maintains in-memory cache for mapping of [active time series](#what-is-an-active-time-series) into internal series ids.
The cache size depends on the available memory for VictoriaMetrics in the host system. If the information about all the active time series doesn't fit the cache,
then VictoriaMetrics needs to read and unpack the information from disk on every incoming sample for time series missing in the cache.
This operation is much slower than the cache lookup, so such an insert is named a `slow insert`.
A high percentage of slow inserts on the [official dashboard for VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#monitoring) indicates
a memory shortage for the current number of [active time series](#what-is-an-active-time-series). Such a condition usually leads
to a significant slowdown for data ingestion and to significantly increased disk IO and CPU usage.
The solution is to add more memory or to reduce the number of [active time series](#what-is-an-active-time-series).

[Cardinality explorer](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#cardinality-explorer) can be helpful for locating the source of high number of active time series.

## How to optimize MetricsQL query?

See [this article](https://valyala.medium.com/how-to-optimize-promql-and-metricsql-queries-85a1b75bf986).

VictoriaMetrics also provides [query tracer](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#query-tracing) 
and [cardinality explorer](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#cardinality-explorer),
which can help during query optimization.

See also [troubleshooting slow queries](https://docs.victoriametrics.com/victoriametrics/troubleshooting/#slow-queries).

## Which VictoriaMetrics type is recommended for use in production - single-node or cluster?

Both [single-node VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/) and
[VictoriaMetrics cluster](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/) are production-ready.

See [Scalability limits of VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/faq/#what-are-scalability-limits-of-victoriametrics).

Single-node VictoriaMetrics requires lower amounts of CPU and RAM for handling the same workload comparing
to cluster version of VictoriaMetrics, since it doesn't need to pass the encoded data over the network
between [cluster components](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#architecture-overview).

The performance of a single-node VictoriaMetrics scales almost perfectly with the available CPU, RAM and disk IO resources on the host where it runs -
see [this article](https://valyala.medium.com/measuring-vertical-scalability-for-time-series-databases-in-google-cloud-92550d78d8ae).

Single-node VictoriaMetrics is easier to setup and operate comparing to cluster version of VictoriaMetrics.

Given the facts above **it is recommended to use single-node VictoriaMetrics in the majority of cases**.

Cluster version of VictoriaMetrics may be preferred over single-node VictoriaMetrics in the following relatively rare cases:

- If [multitenancy support](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#multitenancy) is needed,
  since single-node VictoriaMetrics doesn't support multitenancy. Though it is possible to run multiple single-node VictoriaMetrics
  instances - one per each tenant - and route incoming requests from particular tenant to the needed VictoriaMetrics instance
  via [vmauth](https://docs.victoriametrics.com/victoriametrics/vmauth/).

- If the current workload cannot be handled by a single-node VictoriaMetrics. For example, if you are going to ingest hundreds of millions of active time series
  at ingestion rates exceeding a million samples per second, then it is better to use cluster version of VictoriaMetrics,
  since its capacity can [scale horizontally with the number of nodes in the cluster](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#cluster-resizing-and-scalability).

[Don't choose cluster unless you have to](https://victoriametrics.com/blog/dont-default-to-microservices-you-will-thank-us-later/).

## How to migrate data from single-node VictoriaMetrics to cluster version?

The single-node version of VictoriaMetrics stores data on disk in slightly different format compared to the cluster version of VictoriaMetrics.
This makes it impossible to just copy the on-disk data from `-storageDataPath` directory from single-node VictoriaMetrics to a `vmstorage` node in VictoriaMetrics cluster.
If you need to migrate data from a single-node VictoriaMetrics to the cluster version, then [follow these instructions](https://docs.victoriametrics.com/victoriametrics/vmctl/victoriametrics/).

## Why isn't MetricsQL 100% compatible with PromQL?

[MetricsQL](https://docs.victoriametrics.com/victoriametrics/metricsql/) provides better user experience than PromQL. It fixes a few annoying issues in PromQL. This prevents MetricsQL to be 100% compatible with PromQL. See [this article](https://medium.com/@romanhavronenko/victoriametrics-promql-compliance-d4318203f51e) for details.

## How to migrate data from Prometheus to VictoriaMetrics?

Please see [these docs](https://docs.victoriametrics.com/victoriametrics/vmctl/prometheus/).

## How to migrate data from InfluxDB to VictoriaMetrics?

Please see [these docs](https://docs.victoriametrics.com/victoriametrics/vmctl/influxdb/).

## How to migrate data from OpenTSDB to VictoriaMetrics?

Please see [these docs](https://docs.victoriametrics.com/victoriametrics/vmctl/opentsdb/).

## How to migrate data from Graphite to VictoriaMetrics?

Please use the [whisper-to-graphite](https://github.com/bzed/whisper-to-graphite) tool for reading data from Graphite and pushing them to VictoriaMetrics via [Graphite's import API](https://docs.victoriametrics.com/victoriametrics/integrations/graphite/#ingesting).

## Why do the same metrics have differences in VictoriaMetrics' and Prometheus' dashboards?

There could be a slight difference in stored values for time series. Due to different compression algorithms, VM may reduce the precision for float values with more than 12 significant decimal digits. Please see [this article](https://valyala.medium.com/evaluating-performance-and-correctness-victoriametrics-response-e27315627e87).

The query engine may behave differently for some functions. Please see [this article](https://medium.com/@romanhavronenko/victoriametrics-promql-compliance-d4318203f51e).

## If downsampling and deduplication are enabled how will this work?

[Deduplication](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#deduplication) is a special case of zero-offset [downsampling](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#downsampling). So, if both downsampling and deduplication are enabled, then deduplication is replaced by zero-offset downsampling

## How to upgrade or downgrade VictoriaMetrics without downtime?

Single-node VictoriaMetrics cannot be restarted / upgraded or downgraded without downtime, since it needs to be gracefully shut down and then started again. See [how to upgrade VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#how-to-upgrade-victoriametrics).

[Cluster version of VictoriaMetrics](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/) can be restarted / upgraded / downgraded without downtime according to [these instructions](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#updating--reconfiguring-cluster-nodes).

## Why VictoriaMetrics misses automatic data re-balancing between vmstorage nodes?

VictoriaMetrics doesn't rebalance data between `vmstorage` nodes when new `vmstorage` nodes are added to the cluster.
This means that newly added `vmstorage` nodes will have less data at `-storageDataPath` compared to the older `vmstorage` nodes
until the historical data is removed from the old `vmstorage` nodes when it goes outside the configured [retention](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#retention).

The automatic re-balancing is the process of moving data between `vmstorage` nodes, so every node eventually contains the same amount of data.
It is disabled by default because it may consume additional CPU, network bandwidth and disk IO at `vmstorage` nodes for long periods of time,
which, in turn, can negatively impact VictoriaMetrics cluster availability.

Additionally, it is unclear how to handle the automatic re-balancing if cluster configuration changes while the re-balancing is in progress.

The amounts of data stored in `vmstorage` becomes equal among old `vmstorage` nodes and new `vmstorage` nodes
after historical data is removed from the old `vmstorage` nodes because it goes outside of configured [retention](https://docs.victoriametrics.com/victoriametrics/single-server-victoriametrics/#retention).

The data ingestion load becomes even between old `vmstorage` nodes and new `vmstorage` nodes almost immediately
after adding new `vmstorage` nodes to the cluster, since `vminsert` nodes evenly distribute incoming time series
among the nodes specified in `-storageNode` command-line flag. The newly added `vmstorage` nodes may experience
increased load during the first couple of minutes because they need to register [active time series](https://docs.victoriametrics.com/victoriametrics/faq/#what-is-an-active-time-series).

The query load becomes even between old `vmstorage` nodes and new `vmstorage` nodes after most of queries are executed
over time ranges with data covered by new `vmstorage` nodes. Usually the most of queries are received
from [alerting and recording rules](https://docs.victoriametrics.com/victoriametrics/vmalert/), which query data on limited time ranges
such as a few hours or few days at max. This means that the query load between old `vmstorage` nodes and new `vmstorage` nodes
should become even within few hours / days after adding new `vmstorage` nodes.

## Why VictoriaMetrics misses automatic recovery of replication factor?

VictoriaMetrics doesn't restore [replication factor](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#replication-and-data-safety)
when some of `vmstorage` nodes are removed from the cluster because of the following reasons:

- Automatic replication factor recovery needs to copy non-trivial amounts of data between the remaining `vmstorage` nodes.
  This additional copying requires additional CPU, disk IO and network bandwidth at `vmstorage` nodes. This may negatively impact
  VictoriaMetrics cluster availability during extended periods of time.

- It is unclear when the automatic replication factor recovery must be started. How to distinguish the expected temporary
  `vmstorage` node unavailability because of maintenance, upgrade or config changes from permanent loss of data at the `vmstorage` node?

It is recommended reading [replication and data safety docs](https://docs.victoriametrics.com/victoriametrics/cluster-victoriametrics/#replication-and-data-safety)
for more details.
