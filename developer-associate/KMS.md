# AWS KMS (Key Management Service) – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceito geral
- Serviço gerenciado para criação, armazenamento e controle de chaves criptográficas.
- Usado para criptografia de dados em repouso e em trânsito dentro da AWS.
- Permite controle de acesso granular às chaves.

---

## ⚙️ Funcionalidades principais
- Suporta **Customer Master Keys (CMKs)**, que podem ser:
  - Gerenciadas pela AWS (AWS-managed keys)
  - Gerenciadas pelo cliente (Customer-managed keys)
- Integração nativa com serviços AWS (S3, EBS, RDS, Lambda, DynamoDB, etc).
- Suporta criptografia simétrica e assimétrica.
- Gerenciamento de permissões via políticas KMS e IAM.
- Registro de uso das chaves via CloudTrail para auditoria.
- Rotação automática de chaves (opcional, geralmente anual).

---

## 🔐 Segurança
- Controle de acesso detalhado: quem pode usar, administrar e gerenciar as chaves.
- As chaves nunca saem do KMS (processo seguro dentro do hardware).
- Políticas de chave e permissões IAM determinam ações permitidas.
- Logs de uso gravados no CloudTrail para auditoria.

---

## 🧪 Perguntas comuns na prova

### Q: Como criptografar objetos no S3 usando uma chave própria?
✅ Configure SSE-KMS com uma **Customer Managed Key (CMK)** no bucket.

### Q: Quero controlar quem pode usar minhas chaves para descriptografar dados
✅ Use políticas KMS e IAM para definir permissões específicas.

### Q: Posso automatizar a rotação das chaves?
✅ Sim, habilite rotação automática em CMKs.

### Q: Como auditar quem usou minhas chaves?
✅ Use **CloudTrail** para registrar chamadas à KMS.

### Q: Qual é o tamanho máximo de dados suportado pelo AWS KMS para criptografia direta?
✅ AWS KMS suporta até 4 KB (4096 bytes) de dados para criptografia direta.

### Q: Como funciona a criptografia com KMS?
❌ KMS não recebe dados diretamente para criptografar.
---

## 📌 Dicas rápidas
- CMKs são centrais para segurança e compliance na AWS.
- Use KMS para criptografar dados sensíveis em muitos serviços AWS.
- IAM e KMS policies devem ser configuradas cuidadosamente para não bloquear acesso.
- Rotação automática ajuda na conformidade sem impacto na aplicação.

---

## 🔗 Links úteis
- [AWS KMS Developer Guide](https://docs.aws.amazon.com/kms/latest/developerguide/)
- [Encrypting data with KMS](https://docs.aws.amazon.com/kms/latest/developerguide/services-s3.html)
- [KMS and CloudTrail integration](https://docs.aws.amazon.com/kms/latest/developerguide/logging-using-cloudtrail.html)
