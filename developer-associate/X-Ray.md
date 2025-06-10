# AWS X-Ray – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço para **tracing distribuído** e análise de performance de aplicações.
- Ajuda a identificar gargalos, latências e erros em arquiteturas distribuídas (ex: microservices, serverless).
- Captura e visualiza dados de requisições que atravessam múltiplos serviços AWS.

## ⚙️ Funcionalidades principais
- Segmentos e subsegmentos representam partes da requisição.
- Trace Maps: visualização gráfica do caminho da requisição.
- Análise de latência, erros, e gargalos em serviços como Lambda, API Gateway, EC2, ECS.
- Integração fácil com SDKs AWS para instrumentação automática ou manual.

## 🔐 Segurança
- Dados criptografados em trânsito e repouso.
- Controle de acesso via IAM.

## 🧪 Perguntas comuns na prova

### Q: Quero monitorar e analisar a performance de uma aplicação distribuída
✅ Use AWS X-Ray para tracing e visualização de chamadas

### Q: Quero identificar onde ocorrem erros ou lentidão em microservices
✅ Use X-Ray para detalhamento por serviço e endpoint

### Q: Como instrumentar minha aplicação para X-Ray?
✅ Use SDK AWS X-Ray (para Lambda, EC2, ECS) e ativar tracing no API Gateway

### Q: Quero visualizar a jornada completa da requisição
✅ Use Trace Maps para entender o fluxo e dependências

---

## 📌 Dicas rápidas
- Ative tracing nas funções Lambda e serviços API Gateway para coleta automática.
- Pode enviar dados customizados (anotações e metadados) para enriquecer análises.
- Integra com CloudWatch para alertas baseados em métricas X-Ray.
- Essencial para debugging em arquiteturas serverless complexas.

---

## 🔗 Links úteis
- [AWS X-Ray Developer Guide](https://docs.aws.amazon.com/xray/latest/devguide/aws-xray.html)
- [Instrumenting Applications](https://docs.aws.amazon.com/xray/latest/devguide/xray-sdk.html)
- [X-Ray API Reference](https://docs.aws.amazon.com/xray/latest/api/API_Operations.html)
