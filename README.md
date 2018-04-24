## ansible-druid

An ansible role to install and configure druid.

## Variables

### Extensions

To modify the extensions set the variable `druid_extensions`.

#### Community extensions

Specify community extensions as

```yml
druid_community_extensions:
  - group_id: io.druid.extensions.contrib
    artifact_id: graphite-emitter
    version: 0.12.0
```

### Ports

Ports are defined by

```yml
druid_broker_port: 8082
druid_coordinator_port: 8081
druid_overlord_port: 8090
```

above are the defaults.

### Service memory and settings

You can customize the per service heap, max new, max direct, and thread settings per service.

```yml
# broker
druid_broker_heap_size: 2g
druid_broker_max_new_size: 1g
druid_broker_max_direct_size: 2g

# coordinator
druid_coordinator_heap_size: 4g

# historical
druid_historical_num_http_threads: 10
druid_historical_buffer_size: 250000000
# number of cores - 1
druid_historical_num_threads: 3
druid_segment_maxsize: 300000000000
druid_historical_heap_size: 4g
druid_historical_max_new_size: 2g
druid_historical_max_direct_size: 10g

# middle manager
druid_mm_worker_capacity: 2
druid_mm_java_opts_array: '["-server", "-Xmx8g", "-Xms4g", "-XX:+UseG1GC", "-XX:G1HeapRegionSize=16m", "-XX:MaxDirectMemorySize=10240g", "-XX:MaxGCPauseMillis=100", "-XX:+PrintGCDetails", "-XX:+PrintGCTimeStamps", "-XX:+PrintReferenceGC", "-XX:+PrintAdaptiveSizePolicy", "-XX:+ExitOnOutOfMemoryError", "-Duser.timezone=UTC", "-Dfile.encoding=UTF-8"]'

# overlord
druid_overlord_heap_size: 4g
druid_overlord_max_new_size: 256m
```

above are the defaults.

### Logging Configuration

You can configure the logging settings by setting the emitter and then
providing a list of key value pairs to set configure values in the
namespace `druid.emitter`.

```yml
druid_emitter: logging
druid_emitter_configuration:
  logging.logLevel=info
```

above are the defaults.

You can also configure the monitors for each service with:

```yml
druid_common_monitoring_monitors:
  io.druid.java.util.metrics.JvmMonitor
druid_historical_monitoring_monitors:
  io.druid.java.util.metrics.JvmMonitor
  io.druid.server.metrics.HistoricalMetricsMonitor
# set monitors on indexing peons
druid_middlemanager_monitoring_monitors:
  io.druid.java.util.metrics.JvmMonitor
druid_realtime_monitoring_monitors:
  io.druid.java.util.metrics.JvmMonitor
  io.druid.segment.realtime.RealtimeMetricsMonitor
# druid_broker_monitoring_monitors
# druid_coordinator_monitoring_monitors
# druid_overlord_monitoring_monitors
```

By default we do not set monitors on the `broker`, `coordinator`, or `overlord`.
They inherit their monitors from common. Uncomment at add list items to their
respective properties in order to specify their monitors.

### Middle manager log storage

Task logs

```yml
druid_indexer_logs_type: s3
druid_indexer_logs_s3Bucket: aws-prod-druid-task-logs
druid_indexer_logs_s3Prefix: prod/logs/v1
```

Peon storage

```yml
druid_middlemanager_indexer_storage_settings:
  archiveBaseKey=prod
  archiveBucket=aws-prod-druid-archive
  baseKey=prod/v1
  bucket=druid
  type=s3
```

## License

Apache 2

## Authors

[pld](https://github.com/pld)
[moshthepitt](https://github.com/moshthepitt)

This work is supported by [Ona](https://ona.io).
