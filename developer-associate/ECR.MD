# AWS Elastic Container Registry (ECR) – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado de registro de imagens Docker, integrado com AWS.
- Facilita armazenamento, gerenciamento e deploy de imagens containerizadas.
- Integrado com ECS, EKS e AWS Fargate para deployment simplificado.

## ⚙️ Funcionalidades principais
- Armazenamento seguro e escalável de imagens Docker.
- Suporte para versões e tags de imagens.
- Integração com IAM para controle de acesso.
- Suporte para criptografia de imagens em repouso usando AWS KMS.
- Pode usar autenticação via AWS CLI, SDKs e Docker CLI.

## 🔐 Segurança
- Controle de acesso granular via políticas IAM.
- Imagens criptografadas com KMS.
- Permite escaneamento de vulnerabilidades (integrado com Amazon Inspector).

## 🧪 Perguntas comuns na prova

### Q: Quero armazenar imagens Docker de forma segura e integrada com AWS
✅ Use AWS ECR para gerenciamento e armazenamento

### Q: Quero controlar quem pode acessar e publicar imagens
✅ Controle acesso com políticas IAM para repositórios ECR

### Q: Como autenticar Docker CLI para push/pull no ECR?
✅ Use `aws ecr get-login-password` para autenticar Docker CLI

### Q: Quero fazer deploy automático de imagens no ECS/EKS
✅ ECR integra nativamente com ECS, EKS e Fargate para deploy simples

### Q: Quero detectar vulnerabilidades nas imagens
✅ Ative o escaneamento de imagens do ECR com Amazon Inspector

---

## 📌 Dicas rápidas
- ECR elimina a necessidade de usar registries externos para Docker.
- Imagens ficam disponíveis regionalmente.
- Pode replicar imagens entre regiões para alta disponibilidade.
- Permite versionamento e controle via tags.

---

## 🔗 Links úteis
- [AWS ECR Developer Guide](https://docs.aws.amazon.com/ecr/latest/userguide/what-is-ecr.html)
- [Docker CLI Authentication with ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/Registries.html#registry-auth)
- [Image Scanning in ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/image-scanning.html)
