# AWS CodePipeline e CodeBuild – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- **CodePipeline**: serviço de integração e entrega contínua (CI/CD) para automação de builds, testes e deploys.
- **CodeBuild**: serviço gerenciado de build, compila código, executa testes e produz artefatos.

## ⚙️ Como funcionam juntos
- CodePipeline define o fluxo (pipeline) com etapas: source → build → test → deploy.
- CodeBuild executa a fase de build/teste dentro da pipeline.

## 🚀 Principais características
- Integra-se com CodeCommit, GitHub, S3, Jenkins e mais.
- Suporte a múltiplas fases e ações customizadas.
- Buildspec.yml: arquivo para configurar comandos de build no CodeBuild.
- Escalabilidade automática e ambientes isolados para builds.

## 🔐 Permissões
- Pipelines e builds usam **IAM Roles** para acesso aos recursos.
- Pode usar variáveis de ambiente e segredos gerenciados.

## 🧪 Perguntas comuns na prova

### Q: Quero automatizar build, testes e deploy na AWS
✅ Use CodePipeline com CodeBuild para build/test e deploy (ex: Elastic Beanstalk, Lambda)

### Q: Como configurar comandos de build no CodeBuild?
✅ Use arquivo **buildspec.yml** com fases (install, pre_build, build, post_build)

### Q: Quero integrar repositórios GitHub e AWS CodeCommit
✅ CodePipeline suporta fontes GitHub e CodeCommit

### Q: Preciso rodar testes automáticos antes do deploy
✅ Configure ação de build no CodeBuild que roda os testes

### Q: Quero pipeline escalável e gerenciada
✅ CodePipeline e CodeBuild escalam automaticamente sem servidores próprios

---

## 📌 Dicas rápidas
- CodePipeline orquestra, CodeBuild executa os builds.
- Buildspec.yml é o coração da configuração do CodeBuild.
- Pode usar AWS CloudFormation para criar pipelines automaticamente.
- Pode integrar notificações com SNS ou CloudWatch Events.

---

## 🔗 Links úteis
- [CodePipeline User Guide](https://docs.aws.amazon.com/codepipeline/latest/userguide/welcome.html)
- [CodeBuild User Guide](https://docs.aws.amazon.com/codebuild/latest/userguide/welcome.html)
- [Buildspec Reference](https://docs.aws.amazon.com/codebuild/latest/userguide/build-spec-ref.html)
