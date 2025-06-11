# Amazon EventBridge – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado de **event bus** para construir arquiteturas orientadas a eventos.
- Permite conectar aplicações usando eventos de serviços AWS, aplicações customizadas e SaaS (ex: Zendesk, Datadog).
- Substituto moderno e mais poderoso do CloudWatch Events.

## ⚙️ Componentes principais
- **Event Bus**: canal por onde os eventos trafegam (default, custom, partner).
- **Rules**: filtram eventos com base em padrão (JSON) e direcionam para destinos (targets).
- **Targets**: serviços que recebem o evento (ex: Lambda, SQS, SNS, Step Functions, etc.).

## 🔐 Segurança
- Controle de acesso com IAM (quem pode emitir eventos e criar regras).
- Eventos são enviados com segurança interna pela AWS (sem configuração de rede).
- Pode usar criptografia com KMS para alguns destinos como SQS/SNS.

## 🧪 Perguntas comuns na prova

### Q: Quero acionar uma função Lambda quando um recurso é criado ou modificado
✅ Crie uma **rule** no EventBridge e defina a função Lambda como destino

### Q: Quero escutar eventos personalizados de minha aplicação
✅ Use um **custom event bus** e envie eventos usando o SDK AWS (PutEvents)

### Q: Preciso conectar um app externo (SaaS) com minha arquitetura AWS
✅ Use **partner event sources** integradas com EventBridge

### Q: Quero rotear eventos diferentes para serviços diferentes
✅ Use **padrões de filtro** em regras do EventBridge

---

## 📌 Dicas rápidas
- Substitui o uso antigo de CloudWatch Events com mais poder de roteamento.
- Pode reagir a eventos de praticamente qualquer serviço AWS.
- Suporta eventos com payloads customizados (ex: app envia JSON próprio).
- Ideal para arquiteturas desacopladas e orientadas a eventos.

---

## 🔗 Links úteis
- [EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)
- [Creating Rules](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-create-rule.html)
- [Event Patterns](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-patterns.html)
- [Using Custom Event Buses](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-custom-event-bus.html)
