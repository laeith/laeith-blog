+++
title = "Wire formats - comparison & benchmarking"
date = 2021-03-30
+++

Recently I had to make my mind up and choose a serialization format for IPC/Wire communication between current and future services. As usual, unfortunately there are quite a few possibilities and there doesn't seem to be a silver bullet.

Every time we want to send data from one system to another over network, or a file, we have to somehow represent it in bytes, this is achieved by data encoding. It's a translation of in-memory objects to byte sequences and *vice versa*.  Given that applications evolve it's reasonable to assume that our communication will evolve as well, on top of it might not be possible to update all systems at once, and we may be forced to do a rolling-update. For such scenarios it's vital to analyze how schema can evolve. Fortunately for me this is considered a second-tier requirement but for anyone interested I suggest taking a look at Martin Kleppmann 'Designing Data-Intensive Applications' chapter 4.

In this post I will look at several formats and try to compare their performance, easy of use and potential.

### Methodology

I'm going to compare simple scenarios like serialization, deserialization and sometime special combinations using provided Java clients for each respective format.

Micro-benchmarking is notoriously tricky to get right, and even when we get it right it's hard to draw correct conclusions. On top of that, I'm using a JVM-based language that makes it even worse. Profiling is a must, even with these simple benchmarks I had to profile the code to weed out quite a few obvious problems.

It's turns out it's crucial to use data that is **as close to production data as possible**, for benchmarking I used message schema that is fairly representative for my use-case - but it can make *significant* difference. 
[comment]: <> (For example if the data consisted mostly of strings than the speed difference between Protobuf and JSON was negligible. TODO: Verify)
Additionally, performance will vary depending not only on **how you use the client but also what client is used** (i.e. Java Avro client vs C++ Avro client etc.) 

Note that the purpose of this benchmark is to *compare* serialization/deserialization speed, this means that these values probably don't represent 'optimal' speed that could be achieved - there are potential optimizations that could be applied like: avoid autoboxing, using alternative client/approach, using more judicious types (do we really need an int for a version field?) etc.
Unfortunately it means that this might be unfair for some formats, especially those that allow for more fine-grained control.
On the other hand, **it's probably better to measure the most likely usage** instead of trying to hyper-tune everything - [see where hyper optimization may lead.](https://benchmarksgame-team.pages.debian.net/benchmarksgame/index.html) I tried my best to balance fairness with 'typical usage'.

Last but not least, [the code for these benchmarks is available here.](https://github.com/laeith/playground) Feel free to suggest fixes.


**Schema**:
```protobuf
message PingPong {
  int64 id = 1;                 // 1
  int32 version = 2;            // 2
  string message = 3;           // "Random message - " + System.currentTimeMillis()
  bool is_important = 4;        // true
  repeated string names = 5;    // ["John-1", "John-1", "John-2"]
  repeated int32 ints = 6;      // [1, 22, 333, 4444, 55555]
  repeated double doubles = 7;  // [1.132314, 2.111111, 3.314155, 4.1231488, 5.12395832]
}
```
All other formats have equivalent/similar schemas, for details see code.

### Benchmarks

Let's cut to the chase, on my desktop (Ryzen 3900x): throughput - more is better:

{{ image(src="main_chart.png", alt="Main chart") }}

Tabular:

{{ image(src="table_full.png", alt="Table full") }}

There are a few surprises, the first one is relatively poor performance for the default Avro implementation, results are almost on par with typical JSON read/write speed. I definitely expected better.

For Avro serialization I also provide slightly more optimized version while I'm not doing the same for deserialization. For a typical user I consider it to be a little too error-prone to operate on a single mutable object/ByteBuffer post deserialization, especially when it's not advised as 'the standard approach'. Eventually, it can perform quite well during serialization, see 'Why benchmarking is tricky part 1' below for details.

The format itself is only partially responsible for speed, it sets a theoretical upper limit. Typical JSON serialization as done in Jackson (via reflection) has very polished user experience but performs rather poorly. Surprisingly, DSL-Json shows how much can be achieved by a ~~better~~ faster implementation. I have to admit that this lets-generate-classes-during-compilation approach turned out to be quite seamless and performance improvements - 50% higher throughput in serialization and twice as fast during reading is impressive.
DSL-Json is a strong contender when external systems enforce JSON usage.




- Zero copy vs typical usage
  - Random access

### Schema impact, what about string only?
- Throughput for serialization / deserialization


### Json

### Apache Avro

### Protocol Buffers

### Thrift
- Well.. I need to built the tool on my own?

### Apache Arrow

### Why benchmarking is tricky part 1
Even a single client can be used in multiple ways, this is especially acute in case of Avro where *the naive* usage provides speeds on par with JSON, but two relatively minor changes can give us 2.5x improvement:

'Typical/purity' Avro usage: **1132.303 ± 27.516**

When we take a look at CPU flame it becomes obvious what's the problem:

{{ image(src="avro_pre_builder_reuse", alt="Avro pre flamegraph") }}

In the naive implementation we spend half the time for builders recreation. We introduce builder and ByteBuffer reuse and run the benchmark again:

Avro with builder with bytebuffer reuse: **2550.451 ± 109.546**

{{ image(src="avro_post_fix", alt="Avro post flamegraph") }}

Interestingly, reusing builders in Protobuf Java implementation is counterproductive and yields similar performance results.

That's one of the reasons benchmarking on your own is for important, even if someone achieves poor results in their application it doesn't mean that you must suffer the same fate in your system.

### Why benchmarking is tricky part 2
Assuming we get reasonably reliable results it's still not so easy to apply it in real world. Let's say that we use the abovementioned benchmarks to guide our choices, let's say we are content with Jackson JSON results... 

TODO: Example with string only data for protobuf vs json

### Estimating benchmark results uncertainty - https://pkolaczk.github.io/estimating-benchmark-errors/

### Simple binary encoding
- This is very interesting, it's "zero-copy" approach, same as in FlatBuffers,
  Serialized format allows random access to a specific data elements without parsing all data. But in order to achieve that
  i

- Avro as a dynamic 'schema-less' approach



### Ideas
- Zero-copy for protobuf?
- What's the point of json/xml/...? Internal vs external API

There are many other formats, to name a few MessagePack, FlatBuffers

If you have to make the same decision, remember that it's crucial to run your own benchmarks, preferably with production-like data. 

Maybe you need to serialize only String data? Then Json might be equally fast?

### Closing words

Benchmarking, especially comparison, is tricky: usually it's advised to write two versions alongside and check differences, but even in only slightly more complex scenarios writing two *same* versions is a non-obvious task.

In the end, does it really make any difference?
Well, for high frequency trading it can be of paramount importance when processing time is typically measured in microseconds (even 10s of microseconds - without using FPGAs/ASICs).
On the other hand, if business logic takes milliseconds or more serialization time might be on par with measurement error.

### Suggested literature
* Designing Data-Intensive applications
* Documentations



### Binary comparison

### Schema evolution


#### Footnotes
1. [Codebase for benchmarks](https://github.com/laeith/playground)
2. Async profiler used to investigate code performance
3. 