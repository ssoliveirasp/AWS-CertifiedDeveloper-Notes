# Amazon SQS (Simple Queue Service) – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado de **fila de mensagens** para desacoplar componentes de sistemas distribuídos.
- Garantia de entrega **pelo menos uma vez**.
- Suporta dois tipos de fila:
  - **Standard Queue**: alta taxa, entrega **não ordenada** e possível duplicação.
  - **FIFO Queue**: entrega **ordenada** e sem duplicatas, menor throughput.

## ⚙️ Principais recursos
- Mensagens podem ter até 256 KB.
- Tempo de retenção configurável (1 minuto a 14 dias).
- Visibility Timeout: evita múltiplos consumidores processando a mesma mensagem simultaneamente.
- Dead Letter Queue (DLQ) para mensagens que falham várias vezes.
- Integração com Lambda, SNS, ECS, etc.

## 🧪 Perguntas comuns na prova

### Q: Quero desacoplar serviços com filas garantidas, entrega pelo menos uma vez
✅ Use SQS (Standard ou FIFO conforme necessidade de ordenação)

### Q: Preciso processamento assíncrono e confiável
✅ SQS com consumidores processando mensagens da fila.

### Q: Quero redirecionar mensagens com falha para análise posterior
✅ Configure Dead Letter Queue

---

# Amazon SNS (Simple Notification Service) – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado de **pub/sub e notificações**.
- Publica mensagens para múltiplos assinantes simultaneamente.
- Protocolos suportados: HTTP/HTTPS, Email, SMS, Lambda, SQS, Application (push mobile).

## ⚙️ Principais recursos
- Tópicos para organizar mensagens e assinantes.
- Fan-out pattern: uma mensagem publicada no SNS pode ser entregue a várias filas SQS, Lambdas, etc.
- Mensagens são entregues **pelo menos uma vez**.
- Suporte a filtros de mensagens para assinantes.

## 🧪 Perguntas comuns na prova

### Q: Quero enviar notificações para múltiplos serviços simultaneamente
✅ Use SNS (ex: disparar notificações para Lambda + SMS + SQS)

### Q: Preciso fan-out para desacoplar sistemas com vários consumidores
✅ Publique no SNS que distribui para múltiplos assinantes (SQS, Lambda)

### Q: Quero filtro de mensagens para assinantes específicos
✅ Use Message Filtering no SNS

---

## 📌 Diferenças rápidas SQS x SNS
| Característica         | SQS                         | SNS                             |
|-----------------------|-----------------------------|--------------------------------|
| Tipo de comunicação   | Point-to-point (fila)        | Publish-subscribe (tópico)      |
| Delivery              | Pull (consumidor busca)      | Push (SNS envia para assinantes)|
| Ordem das mensagens   | Opcional (FIFO)              | Não garantida                   |
| Duplicação           | Possível em Standard          | Pode ocorrer                   |
| Uso comum             | Processamento assíncrono, desacoplamento | Notificações em tempo real, fan-out |

---

## 🔗 Links úteis
- [Amazon SQS Developer Guide](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/welcome.html)
- [Amazon SNS Developer Guide](https://docs.aws.amazon.com/sns/latest/dg/welcome.html)
