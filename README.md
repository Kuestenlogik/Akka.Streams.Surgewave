# Akka.Streams.Surgewave — ARCHIVED

> **This repository is archived.** Active development has moved to
> [**Kuestenlogik/Akka.Surgewave**](https://github.com/Kuestenlogik/Akka.Surgewave),
> a consolidated Mono-Repo that ships **two** NuGet packages from a single tag:
> `Kuestenlogik.Surgewave.AkkaStreams` and `Kuestenlogik.Surgewave.AkkaPersistence`.

## History

- This repo published [`Kuestenlogik.Akka.Streams.Surgewave`](https://www.nuget.org/packages/Kuestenlogik.Akka.Streams.Surgewave) v0.1.0 and v0.1.1.
- v0.2.0+ ships only from the [Akka.Surgewave](https://github.com/Kuestenlogik/Akka.Surgewave) repo under the new id [`Kuestenlogik.Surgewave.AkkaStreams`](https://www.nuget.org/packages/Kuestenlogik.Surgewave.AkkaStreams).
- The v0.1.x packages remain on nuget.org for existing consumers; they receive no further updates.

## Migration

```bash
# remove old
dotnet remove package Kuestenlogik.Akka.Streams.Surgewave
# add new
dotnet add package Kuestenlogik.Surgewave.AkkaStreams
```

```csharp
// before
using Akka.Streams.Surgewave;

// after
using Kuestenlogik.Surgewave.AkkaStreams;
```

The API surface is otherwise compatible — `SurgewaveConsumer`, `SurgewaveProducer`, `Committer`, etc. exist in the new namespace.

## License

Apache-2.0
