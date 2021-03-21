+++
title = "Wire formats - benchmarking & comparison"
date = 2021-03-30
+++

Why do we even need this?
Pickle, serializable etc.
Text serialization, UTF etc.

### Methodology

- Ping-pong? Or just serialize and deserialize?
    - Synchronously
    - Asynchronously
- Single machine
- throughput per se not as important
- Comparison is the only value
- Intended usage

- Space taken / size
- Throughput for serialization / deserialization
- Zero copy vs typical usage

### Binary comparison

### Schema evolution

### Json

### Apache Avro

### Protocol Buffers

### Thrift

### Simple binary encoding

### Apache Arrow

### Estimating benchmark results uncertainty - https://pkolaczk.github.io/estimating-benchmark-errors/

### Async profiler, flame graphs

### Ideas
- CPU pinning?
- Zero-copy approach?
- Zero-copy for protobuf?
- Threads vs processes?
- What's the point of json/xml/...? Internal vs external API