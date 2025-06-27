# AWS Secrets Manager – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado para armazenar, gerenciar e rotacionar segredos (ex: senhas, chaves API, tokens).
- Automatiza a rotação segura dos segredos integrando com AWS Lambda.
- Criptografia padrão com KMS (Key Management Service).

## ⚙️ Funcionalidades principais
- Armazenamento seguro de segredos com controle de acesso via IAM.
- Rotação automática de segredos usando funções Lambda customizadas.
- Integração fácil com aplicações via AWS SDK e APIs.
- Auditoria via CloudTrail para acesso e modificações.

## 🔐 Segurança
- Segredos criptografados em repouso com KMS.
- Controle granular de permissões via IAM policies.
- Logs de acesso com CloudTrail para compliance.

## 🧪 Perguntas comuns na prova

### Q: Quero armazenar credenciais de banco e rotacionar automaticamente
✅ Use Secrets Manager com Lambda para rotação automática

### Q: Quero que aplicação recupere segredo de forma segura e programática
✅ Use AWS SDK para buscar segredo em Secrets Manager

### Q: Quero controlar quem pode acessar quais segredos
✅ Use políticas IAM vinculadas a usuários, funções e serviços

### Q: Quero auditar acesso e alterações em segredos
✅ Use CloudTrail para monitorar Secrets Manager

### Q: Como armazenar e rotacionar credenciais de banco RDS de forma segura, sem deixá-las no código?
✅ Usar AWS Secrets Manager

---

## 📌 Dicas rápidas
- Secrets Manager é mais completo que Parameter Store para segredos críticos.
- Rotação automática exige criar função Lambda que implementa a lógica de atualização.
- Pode armazenar segredos JSON com múltiplos pares chave-valor.
- Evite hardcoding de senhas e tokens no código: sempre use Secrets Manager.

---

## 🔗 Links úteis
- [AWS Secrets Manager User Guide](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)
- [Rotation Lambda Templates](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets-lambda-function-overview.html)
- [AWS SDK Secrets Manager](https://docs.aws.amazon.com/secretsmanager/latest/userguide/programming.html)
