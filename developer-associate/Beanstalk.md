# AWS Elastic Beanstalk – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço **PaaS (Platform as a Service)** para implantar e escalar aplicações web e APIs rapidamente.
- Suporta linguagens como **Java, .NET, Python, Node.js, PHP, Ruby, Go, Docker**.
- Gerencia **infraestrutura automaticamente**: EC2, Load Balancer, Auto Scaling, RDS, etc.

## 📦 Componentes principais
- **Application** – container lógico para versões da app.
- **Environment** – instância da aplicação com infraestrutura.
- **Environment Configuration** – configurações de instância, escalabilidade, variáveis de ambiente.
- **Application Version** – versão do código enviado (zip ou WAR/JAR).

## ⚙️ Tipos de ambiente
- **Web Server Environment** – para apps que recebem requisições HTTP/S.
- **Worker Environment** – processa jobs em background, usando SQS.

## 🧰 Deploy e Automação
- Suporte a deploy automático com **.ebextensions** (YAML).
- Pode fazer deploy com **CLI (`eb cli`)**, Console ou **CI/CD** (CodePipeline).
- Versionamento automático das aplicações.

## 🔐 Permissões e IAM
- Elastic Beanstalk precisa de:
  - **EC2 Instance Profile** – usada pelas instâncias para acessar outros serviços (ex: S3, CloudWatch).
  - **Service Role** – usada pelo Beanstalk para gerenciar recursos em seu nome.

## 📁 Estrutura básica do deploy
- Código zipado com `application.py`, `index.js`, etc.
- Pode conter pasta **`.ebextensions/`** com arquivos `.config` para customização.

## 🧪 Perguntas comuns no exame

### Q: Preciso implantar app sem gerenciar infraestrutura
✅ Use Elastic Beanstalk

### Q: Preciso escalar app com base em carga de CPU
✅ Beanstalk + Auto Scaling configurado no ambiente

### Q: Aplicação precisa de banco relacional persistente
✅ Adicionar RDS na criação do ambiente (não recomendado para produção)

### Q: Preciso rodar tasks em background
✅ Usar Worker Environment + SQS

### Q: Quero executar scripts de inicialização (ex: instalar pacotes)
✅ Usar `.ebextensions/*.config` com comandos

### Q: Em um deployment Rolling no Elastic Beanstalk, algumas instâncias falharam e foram terminadas. O que acontece com elas?
✅ O Elastic Beanstalk cria novas instâncias com a última versão implantada com sucesso.

### Q: Após deployment Beanstalk, os EC2 burst balances foram perdidos. O que pode ter causado isso?
✅ O deployment foi feito usando immutable updates ou traffic splitting. Esses modos criam novas instâncias EC2, substituindo as antigas. 

### Q: Como implantar no Beanstalk sem afetar performance em app de alto tráfego, com bom custo-benefício?
✅ Usar Rolling with additional batch.

### Q: Como manter o RDS fixo e permitir que o ElastiCache seja recriado a cada deploy no Beanstalk? (2 opções)
✅ RDS externo via variáveis de ambiente
✅ ElastiCache em .ebextensions/

## 📌 Dicas rápidas
- A infraestrutura é gerenciada pela AWS, `mas pode ser personalizada`.
- Pode configurar EC2 type, VPC, ELB, Auto Scaling.
- Logs vão para `CloudWatch`.
- Ideal para apps monolíticas que precisam escalar, mas sem container/K8s.

---

## 🧪 Exemplo de `.ebextensions` para instalar pacote
```yaml
packages:
  yum:
    git: []
commands:
  01_set_permissions:
    command: "chmod +x /var/app/staging/start.sh"
