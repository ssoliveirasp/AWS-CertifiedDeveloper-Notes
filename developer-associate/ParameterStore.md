# AWS Systems Manager Parameter Store – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado para armazenar dados de configuração e segredos simples (parâmetros).
- Pode armazenar strings, strings criptografadas (com KMS), e dados hierárquicos.
- Útil para gerenciar configurações e segredos leves sem custo adicional (na maioria dos casos).

## ⚙️ Funcionalidades principais
- Suporte para parâmetros hierárquicos (ex: /app/dev/db_password).
- Integração com AWS KMS para criptografia de parâmetros sensíveis.
- Controle de acesso via IAM.
- Histórico e versionamento de parâmetros.
- Integração com AWS Lambda, EC2, ECS para leitura de parâmetros em runtime.

## 🔐 Segurança
- Parâmetros criptografados são armazenados com KMS.
- IAM controla quem pode acessar/modificar parâmetros.
- Logs via CloudTrail para auditoria.

## 🧪 Perguntas comuns na prova

### Q: Quero armazenar configurações e segredos leves de forma segura
✅ Use Parameter Store com criptografia KMS para segredos sensíveis

### Q: Quero versionar configurações e acessar versões específicas
✅ Parameter Store mantém histórico e versões de parâmetros

### Q: Quero integrar com Lambda para buscar parâmetros em runtime
✅ Lambda pode usar SDK para ler parâmetros no Parameter Store

### Q: Quero controlar acesso granularmente
✅ Use políticas IAM específicas para acesso a parâmetros

### Q: Como gerar relatório para auditoria mostrando quem e quando acessou o SSM Parameter Store?
✅ Usar AWS CloudTrail para registrar todas as chamadas API feitas pelos usuários.


---

## 📌 Dicas rápidas
- Para segredos críticos e com rotação automática, prefira Secrets Manager.
- Parameter Store é bom para configs, flags e segredos menos sensíveis.
- Pode usar parâmetros em CloudFormation para passar configs dinâmicas.
- Fácil de usar para armazenar URLs, strings, paths, flags, etc.

---

## 🔗 Links úteis
- [Parameter Store User Guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)
- [Using Parameter Store with Lambda](https://docs.aws.amazon.com/systems-manager/latest/userguide/integration-lambda-parameter-store.html)
- [AWS KMS Encryption](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)
