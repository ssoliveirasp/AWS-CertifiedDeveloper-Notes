# AWS Step Functions – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço de orquestração de workflows serverless.
- Cria máquinas de estado visuais para coordenar múltiplos serviços AWS.
- Ideal para orquestrar funções Lambda, tarefas ECS, chamadas API e mais.

## ⚙️ Componentes principais
- **State Machine**: define o fluxo do processo com estados (Task, Choice, Wait, Parallel, etc).
- **Estados**: representam passos no fluxo (ex: execução Lambda, decisões, espera).
- **Transitions**: transições entre estados definem o caminho do workflow.
- **Input/Output**: dados passados entre estados, podem ser manipulados com JSONPath.

## 🧪 Perguntas comuns na prova

### Q: Quero orquestrar funções Lambda em sequência com lógica condicional
✅ Use Step Functions para criar máquinas de estado com Choice States.

### Q: Quero controlar execução de processos longos, com espera e retries
✅ Step Functions suporta Wait states e políticas de retry/fail.

### Q: Quero visualizar e monitorar execução do workflow
✅ Use console Step Functions para ver estados, logs e falhas.

### Q: Quero orquestrar tarefas distribuídas (ex: Lambda + ECS)
✅ Step Functions integra com múltiplos serviços AWS.

### Q: Quero implementar processamento paralelo
✅ Use Parallel State para rodar múltiplas tarefas simultaneamente.

---

## 📌 Dicas rápidas
- Definição da máquina é em JSON ou YAML (Amazon States Language).
- Pode usar Map State para processamento em lote.
- Integração nativa com CloudWatch para métricas e logs.
- Muito útil para arquiteturas serverless e microservices.

---

## 🔗 Links úteis
- [Step Functions Developer Guide](https://docs.aws.amazon.com/step-functions/latest/dg/welcome.html)
- [Amazon States Language](https://states-language.net/spec.html)
- [Step Functions API Reference](https://docs.aws.amazon.com/step-functions/latest/apireference/Welcome.html)
