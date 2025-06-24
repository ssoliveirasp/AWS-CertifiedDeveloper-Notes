# AWS Budgets – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceito geral
- Serviço que permite **definir, monitorar e alertar** sobre **custos e uso** dentro da conta AWS.
- Ajuda a manter controle financeiro e prever gastos inesperados.
- Pode criar orçamentos por **serviço, linked account, tag, reserva, etc**.

---

## ⚙️ Tipos de orçamento

1. **Cost Budget** – orçamento baseado em custo ($).
2. **Usage Budget** – baseado no uso de recursos (ex: horas EC2).
3. **Savings Plans / RI Budget** – para uso de planos de economia/reservas.
4. **Forecasted Budgets** – baseado em projeções (com dados de uso histórico).

---

## 🔔 Alertas
- Pode enviar **alertas por e-mail ou SNS** quando:
  - Um valor ultrapassa o orçamento real.
  - A previsão de gastos excede o orçamento.
- Suporte para múltiplos alertas por orçamento.

---

## 🔐 Segurança
- Controle de criação e edição de orçamentos via IAM.
- Ideal para equipes de FinOps, devs com responsabilidade financeira e monitoramento multi-conta.

---

## 🧪 Perguntas comuns na prova

### Q: Quero ser avisado se os custos ultrapassarem 80% do orçamento mensal
✅ Use **AWS Budgets com alerta por e-mail/SNS** baseado em percentual de uso

### Q: Quero prever se irei ultrapassar o orçamento antes do fim do mês
✅ Configure um **Forecasted Budget** e ative alertas

### Q: Tenho vários projetos marcados por tag e quero orçamento por projeto
✅ Use **Budgets com filtro por Tag**

### Q: Configurei o Budget há 2 semanas, mas ainda não recebo alertas
✅ AWS Budgets **precisa de até 5 semanas de dados históricos** para previsão correta

---

## 📌 Dicas rápidas
- AWS Budgets ≠ Cost Explorer (Budgets gera alertas, CE é para análise).
- Pode integrar com **AWS Chatbot** para enviar alertas para Slack/Teams.
- Orçamento pode ser **mensal, diário ou trimestral**.
- Funciona bem em organizações com múltiplas contas via AWS Organizations.

---

## 🔗 Links úteis
- [AWS Budgets Docs](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html)
- [Criando budgets com alertas](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create.html)
- [AWS Budgets vs Cost Explorer](https://docs.aws.amazon.com/cost-management/latest/userguide/what-is-aws-cost-explorer.html)
