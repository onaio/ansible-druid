## ansible-druid

An ansible role to install and configure druid.

## Variables

### Extensions

To modify the extensions set the variable `druid_extensions`.

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

## License

Apache 2

## Authors

[Ona Engineering](https://ona.io)
