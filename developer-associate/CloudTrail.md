# AWS CloudTrail – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço que registra e monitora chamadas de API na conta AWS.
- Captura ações realizadas por usuários, serviços e aplicações.
- Essencial para auditoria, compliance e análise forense.

## ⚙️ Funcionalidades principais
- Registra eventos de API (chamadas SDK, CLI, Console).
- Logs armazenados em buckets S3 configuráveis.
- Suporte para múltiplas regiões e contas (multi-region, multi-account).
- Integração com CloudWatch Logs para monitoramento e alertas.

## 🔐 Segurança
- Logs protegidos com políticas S3 e IAM.
- Possibilidade de enviar logs para contas separadas para segurança adicional.
- CloudTrail não pode ser desativado para a conta raiz.

## 🧪 Perguntas comuns na prova

### Q: Quero auditar todas as chamadas de API na minha conta AWS
✅ Use CloudTrail para registrar eventos e manter logs de auditoria

### Q: Quero monitorar atividades suspeitas e gerar alertas
✅ Integre CloudTrail com CloudWatch Logs e configure alarmes

### Q: Quero centralizar logs de várias contas e regiões
✅ Use Trail multi-region e enviar logs para bucket S3 centralizado

### Q: Quero garantir que os logs não sejam alterados
✅ Ative políticas de bucket S3 para proteção e versionamento dos logs

---

## 📌 Dicas rápidas
- CloudTrail registra eventos de gerenciamento (ex: criação de recursos) e eventos de dados (ex: leitura de objetos S3, dependendo da configuração).
- Logs são entregues com atraso de alguns minutos.
- CloudTrail complementa o CloudWatch para monitoramento, mas não substitui.
- Útil para compliance com normas como PCI-DSS, HIPAA.

---

## 🔗 Links úteis
- [AWS CloudTrail User Guide](https://docs.aws.amazon.com/cloudtrail/latest/userguide/cloudtrail-user-guide.html)
- [CloudTrail Logging Events](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-event-reference.html)
- [Integrating CloudTrail with CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CloudWatch-CloudTrail-Integration.html)
