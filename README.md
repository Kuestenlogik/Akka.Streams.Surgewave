# Akka.Streams.Surgewave

Akka.Streams connector for [Surgewave](https://github.com/Kuestenlogik/Surgewave) — Sources, Sinks, and Flows for reactive Surgewave topic integration. Analogous to [Akka.Streams.Kafka](https://github.com/akkadotnet/Akka.Streams.Kafka) (Alpakka).

## Features

- **PlainSource / CommittableSource** — Consumer sources with backpressure and offset commit
- **PlainSink / FlexiFlow** — Producer stages with delivery feedback and passthrough support
- **Transactional** — End-to-end exactly-once consume-transform-produce pipelines
- **Committer** — Batched offset commits with configurable intervals
- **Schema Registry** — Typed serialization/deserialization via Surgewave Schema Registry
- **Partitioned Sources** — Sub-source per partition for partition-local processing

## Quick Start

```csharp
var control = SurgewaveConsumer
    .CommittableSource(consumerSettings, Subscriptions.Topics("orders"))
    .SelectAsync(10, async msg =>
    {
        await ProcessOrder(msg.Record.Key, msg.Record.Value);
        return msg.CommittableOffset;
    })
    .ToMaterialized(
        Committer.Sink(CommitterSettings.Create(system)),
        DrainingControl<Done>.Create)
    .Run(materializer);
```

## License

Apache-2.0
