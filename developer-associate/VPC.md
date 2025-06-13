# AWS CI/CD – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Visão geral
AWS oferece um conjunto de ferramentas gerenciadas para **CI/CD (Integração Contínua e Entrega Contínua)**, permitindo automatizar **build, teste, entrega e deploy** de aplicações.

## ⚙️ Principais serviços

### 1. **AWS CodeCommit**
- Repositório Git gerenciado.
- Suporte a Git padrão (push/pull/clone).
- Controle de acesso via IAM.
- Alternativa ao GitHub/Bitbucket para código privado.

### 2. **AWS CodeBuild**
- Serviço gerenciado de build.
- Compila código, roda testes e gera artefatos.
- Usa arquivos `buildspec.yml` para definir os comandos.
- Escala automaticamente, cobra por tempo de build.

### 3. **AWS CodeDeploy**
- Automação de deploy para:
  - EC2
  - ECS (com ou sem Fargate)
  - Lambda
- Estratégias de deploy: linear, canary, blue/green, all-at-once.
- Permite rollback automático em caso de falha.

### 4. **AWS CodePipeline**
- Orquestração de CI/CD como pipeline completo.
- Define estágios: source → build → test → deploy.
- Integra com CodeCommit, GitHub, S3, CodeBuild, CodeDeploy e terceiros.

### 5. **AWS CodeStar**
- Interface para configurar projetos CI/CD rapidamente.
- Menos usado na prática (pode ser mencionado, mas não costuma cair muito na prova).

---

## 🔐 Segurança
- Todos os serviços usam IAM para controle de acesso.
- Pode definir roles de serviço para permitir que o pipeline execute ações (ex: build, deploy).
- CodePipeline pode ser integrado com approval steps manuais.

---

## 🧪 Perguntas comuns na prova

### Q: Quero armazenar meu código fonte com versionamento Git
✅ Use **CodeCommit**

### Q: Preciso compilar e rodar testes automatizados ao fazer push no repositório
✅ Use **CodeBuild**

### Q: Quero fazer deploy automatizado em EC2 com rollback em caso de erro
✅ Use **CodeDeploy** com estratégias como Blue/Green

### Q: Preciso criar um fluxo completo de CI/CD do código ao deploy
✅ Use **CodePipeline** com stages integrando CodeCommit, CodeBuild e CodeDeploy

---

## 📌 Dicas rápidas
- `buildspec.yml` define os comandos do build no CodeBuild.
- No CodeDeploy, para Lambda você pode usar **traffic shifting** (ex: canary 10%).
- Use S3 como source para CodePipeline, se não usar CodeCommit.
- Para monitoramento e debugging, integre com **CloudWatch Logs** e **X-Ray**.

---

## 🔗 Links úteis
- [AWS CodePipeline Overview](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)
- [AWS CodeBuild User Guide](https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html)
- [AWS CodeDeploy Strategies](https://docs.aws.amazon.com/codedeploy/latest/userguide/deployment-configurations.html)
- [Sample buildspec.yml](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)
