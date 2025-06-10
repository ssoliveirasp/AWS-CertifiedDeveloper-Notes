# Amazon CloudWatch – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço de monitoramento e observabilidade da AWS.
- Coleta dados de **logs, métricas, eventos** e permite ações automatizadas.
- Fundamental para entender o comportamento das aplicações e infraestrutura.

## 🛠️ Componentes principais
- **Métricas**: dados numéricos (CPU, memória, latência, erros).
- **Logs**: registro de eventos e mensagens da aplicação (ex: logs Lambda).
- **Eventos / Alarms**: notificações acionadas com base em métricas (ex: CPU > 80%).
- **Dashboards**: painéis personalizados para visualização das métricas e logs.

## ⚙️ Funcionalidades importantes
- **Logs Insights**: consulta interativa e analítica de logs.
- **Alarms**: configuram triggers para ações (SNS, Lambda, Auto Scaling).
- **Custom Metrics**: enviar métricas personalizadas da aplicação via SDK.
- **CloudWatch Events / EventBridge**: acionamento baseado em eventos do sistema.

## 🔐 Permissões
- Logs e métricas acessam e enviam dados via funções IAM.
- Lambda pode publicar logs automaticamente no CloudWatch Logs.

## 🧪 Perguntas comuns na prova

### Q: Quero monitorar desempenho e falhas da minha aplicação Lambda
✅ Use CloudWatch Logs + Alarms

### Q: Quero configurar alertas para CPU alta em EC2
✅ Configure CloudWatch Alarm baseado na métrica CPUUtilization

### Q: Quero analisar logs com consultas SQL-like
✅ Use CloudWatch Logs Insights

### Q: Quero disparar ações automáticas em resposta a eventos (ex: reiniciar instancia)
✅ Use CloudWatch Events / EventBridge

### Q: Quero métricas específicas da minha aplicação
✅ Envie Custom Metrics via AWS SDK

---

## 📌 Dicas rápidas
- Logs do Lambda vão automaticamente para CloudWatch Logs.
- CloudWatch Logs permite configurar filtros de eventos para alarmes.
- CloudWatch Events (agora EventBridge) é central para arquiteturas orientadas a eventos.
- Dashboards ajudam a visualizar rapidamente o estado geral do sistema.

---

## 🔗 Links úteis
- [CloudWatch User Guide](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [CloudWatch Logs Insights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/AnalyzingLogData.html)
- [CloudWatch Events / EventBridge](https://docs.aws.amazon.com/eventbridge/latest/userguide/what-is-amazon-eventbridge.html)
