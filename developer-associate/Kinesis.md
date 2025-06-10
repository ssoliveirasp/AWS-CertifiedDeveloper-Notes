# Amazon Kinesis – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Plataforma para **processamento de dados em tempo real (streaming)**.
- Componentes principais:
  - **Kinesis Data Streams (KDS)** – stream de dados customizável.
  - **Kinesis Data Firehose** – entrega de dados automatizada (near real-time).
  - **Kinesis Data Analytics** – análises SQL em tempo real.
  - **Kinesis Video Streams** – vídeo em tempo real (menos comum na prova).

## 🔁 Kinesis Data Streams (KDS)
- Fluxo de dados dividido em **shards**.
- Cada shard:
  - 1 MB/s de ingestão.
  - 2 MB/s de leitura.
  - 5 leituras por segundo.
- Retenção de dados:
  - Padrão: 24 horas.
  - Pode estender até **7 dias**.

## 🚚 Kinesis Firehose
- Sem gerenciamento de shard.
- Bufferiza e entrega dados automaticamente para:
  - **S3**, **Redshift**, **Elasticsearch (OpenSearch)**, **Splunk**, **HTTP endpoints**.
- Pode usar **Lambda para transformação inline** dos dados.
- Latência: **60 segundos a alguns minutos**.

## 🧠 Kinesis vs SQS
| Foco                     | Kinesis                      | SQS                      |
|--------------------------|------------------------------|--------------------------|
| Estilo de dados          | Streaming (tempo real)       | Mensagens (fila)         |
| Processamento paralelo   | Shards                       | Consumidores separados   |
| Reprocessamento fácil    | Sim (via Shard Iterator)     | Limitado (DLQ)           |

## 🔐 Permissões
- IAM roles/policies para produtores e consumidores.
- Kinesis pode invocar Lambda, Firehose pode invocar transformações.

## ⚙️ Integrações
- Kinesis Streams → Lambda (stream-based processing).
- Kinesis Firehose → entrega automatizada (ETL leve).
- Kinesis Analytics → queries SQL em tempo real sobre Streams.

## 🧪 Perguntas comuns no exame

### Q: Preciso processar dados em tempo real com latência mínima
✅ **Kinesis Data Streams + Lambda**

### Q: Preciso entregar dados automaticamente no S3 para análise
✅ **Kinesis Data Firehose**

### Q: Preciso transformar os dados antes de gravar no destino
✅ **Kinesis Firehose + Lambda**

### Q: Preciso reprocessar eventos antigos do stream
✅ **Use Shard Iterator (com timestamp ou sequence)**

### Q: Retenção de dados para reprocessamento de até 5 dias
✅ **Configure retention do stream para até 7 dias**

### Q: Processar um stream com SQL em tempo real
✅ **Kinesis Data Analytics**

## 📌 Dicas rápidas
- **Shard = unidade de paralelismo** (pense como partição).
- Lambda é invocada por **lote de registros** do stream.
- Evite shard hot: distribua bem a chave de particionamento.
- Firehose = zero administração (sem shard, sem leitura manual).
- Use **CloudWatch** para monitorar throughput de shards.

---

## 🔗 Links úteis
- [Kinesis Overview – AWS Docs](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)
- [Kinesis Streams vs Firehose](https://docs.aws.amazon.com/firehose/latest/dev/delivery-stream.html)
- [Kinesis Developer Guide](https://docs.aws.amazon.com/streams/latest/dev/developing-producers-consumers.html)

