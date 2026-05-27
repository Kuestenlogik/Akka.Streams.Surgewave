# Akka.Streams.Surgewave

Akka.Streams connector for [Surgewave](https://github.com/Kuestenlogik/Surgewave) — Sources, Sinks, and Flows for reactive Surgewave topic integration. Analogous to [Akka.Streams.Kafka](https://github.com/akkadotnet/Akka.Streams.Kafka) (Alpakka).

> **NuGet PackageId:** `Kuestenlogik.Akka.Streams.Surgewave` &nbsp;·&nbsp; **Namespace:** `Kuestenlogik.Akka.Streams.Surgewave`
>
> The `Akka.*` prefix on nuget.org is verified-reserved by the Akka.NET team, so this package — and the C# namespaces it ships — live under the `Kuestenlogik.*` prefix (Petabridge pattern, consistent with the rest of the Kuestenlogik / Surgewave package family).

## Installation

```bash
dotnet add package Kuestenlogik.Akka.Streams.Surgewave
```

```csharp
using Kuestenlogik.Akka.Streams.Surgewave;
```

> **v0.2.0 Breaking Change:** the C# namespace was renamed from `Akka.Streams.Surgewave` to `Kuestenlogik.Akka.Streams.Surgewave` so the on-disk source tree, the NuGet package id and the namespace are aligned. v0.1.1 consumers need to update their `using` statements.

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
