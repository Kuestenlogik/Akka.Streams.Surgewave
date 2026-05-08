# Akka.Streams.Surgewave — Roadmap

## v0.1 — PlainSource + PlainSink [done]

- [x] PlainSourceStage (GraphStage with backpressure)
- [x] PlainSinkStage (fire-and-forget producer)
- [x] ConsumerSettings / ProducerSettings from HOCON
- [x] Subscriptions: Topics, TopicPattern, Assignment, AssignmentWithOffset
- [x] IControl / SurgewaveConsumerControl for lifecycle management

## v0.2 — CommittableSource + Committer [done]

- [x] CommittableSourceStage with CommittableOffset per message
- [x] CommittableOffset with async commit
- [x] Committer.Sink for batched offset commits
- [x] Committer.CommitFlow for passthrough commits
- [x] CommitterSettings (MaxBatch, MaxInterval, Parallelism)

## v0.3 — FlexiFlow + PassThrough [done]

- [x] FlexiFlowStage with IEnvelope/IResults passthrough pattern
- [x] ProducerMessage: Single, Multi, PassThroughOnly
- [x] ProducerResult, MultiResult, PassThroughResult
- [x] SurgewaveProducer factory: PlainSink, FlexiFlow, TransactionalFlow

## v0.4 — Partitioned + ManualOffset Sources [done]

- [x] PlainPartitionedSourceStage (sub-source per partition)
- [x] ExternalOffsetSourceStage (external offset store callbacks)
- [x] AtMostOnceSource (commit before processing)
- [x] TransactionalSource (EOS consumer)

## v0.5 — DI + Hosting [done]

- [x] WithSurgewaveStreams() fluent configuration
- [x] SurgewaveStreamsSetup (Consumer, Producer, SchemaRegistry, Committer)
- [x] HOCON generation from typed setup objects
- [x] DrainingControl for orderly shutdown with drain

## v0.6 — Tests [done]

- [x] PlainSourceSpec (Subscriptions factory methods)
- [x] CommittableSourceSpec (ConsumeResult construction)
- [x] PlainSinkSpec (ProducerRecord construction)
- [x] FlexiFlowSpec (ProducerMessage/Result roundtrip)
- [x] CommitterSpec (settings defaults)
- [x] ConsumerSettingsTests (fluent API chaining)
- [x] ProducerMessageTests (IEnvelope/IResults interface contracts)
- [x] E2E: produce → consume roundtrip with embedded in-memory Surgewave broker
- [x] E2E: headers preservation verified (content-type)

## v1.0 — Production Ready

- [ ] Transactional flow with real Surgewave EOS (TransactionBuilder)
- [ ] Content-type based auto-deserialization in ConsumerSettings (when Surgewave Client supports it)
- [ ] PlainPartitionedSource rebalance handling (partition assignment/revocation)
- [ ] Backpressure benchmarks
- [ ] NuGet package publish

## Future

- [ ] Avro/Protobuf typed sources and sinks
- [ ] GraphDSL helpers for common Surgewave patterns
- [ ] Metrics/OpenTelemetry integration
- [ ] Testcontainers.Surgewave for CI/CD
