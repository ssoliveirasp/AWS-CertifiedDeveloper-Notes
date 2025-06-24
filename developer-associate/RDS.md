# Amazon RDS – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceito geral
- Serviço gerenciado de banco de dados relacional.
- Suporta: **MySQL, PostgreSQL, MariaDB, Oracle, SQL Server e Amazon Aurora**.
- Reduz o trabalho operacional (backup, patching, replicação, escalabilidade).

---

## ⚙️ Funcionalidades principais

### ✅ Gerenciamento simplificado
- **Backups automáticos** (7 a 35 dias).
- **Snapshots manuais**.
- **Atualizações automáticas** opcionais.
- **Multi-AZ** para alta disponibilidade.
- **Read Replicas** para escalabilidade de leitura.

### ✅ Integração com aplicações
- Conectado por endpoint (host, porta, usuário, senha).
- Pode ser acessado por **Lambda, EC2, ECS**, etc.
- Configure com **Security Groups** para controlar acesso.

### ✅ Escalabilidade
- Aumento de **armazenamento automático** (Storage Auto Scaling).
- **Read Replicas** (em mesma região ou regiões diferentes) para balanceamento de carga.

### ✅ Segurança
- Criptografia em repouso com **AWS KMS**.
- Tráfego criptografado com **SSL**.
- Integração com **IAM Authentication** (em alguns engines).
- Isolamento com **VPC** e controle com **Security Groups**.

---

## 🧪 Perguntas comuns na prova

### Q: Como evitar downtime durante manutenção ou falha?
✅ Use **Multi-AZ deployment**

### Q: Como escalar a leitura sem impactar o banco principal?
✅ Crie uma **Read Replica**

### Q: Como proteger dados sensíveis armazenados no banco?
✅ Ative **criptografia com KMS**

### Q: Como manter o banco entre deployments com Elastic Beanstalk?
✅ **Crie RDS fora do ambiente Beanstalk** e conecte por **variáveis de ambiente**

### Q: Preciso de alta performance com compatibilidade PostgreSQL/MySQL
✅ Use **Amazon Aurora**

### Q: Como otimizar a performance de leitura em RDS PostgreSQL com mínimo esforço de desenvolvimento?
✅ Criar read replicas no RDS e ajustar o código para usar o endpoint das réplicas para consultas.

---

## 📌 Dicas rápidas
- **Multi-AZ ≠ performance** (é para disponibilidade).
- **Read Replicas = performance** (para leitura).
- Backup automático é habilitado por padrão.
- Banco pode ser escalado verticalmente (vCPU/RAM) e horizontalmente (replicas).

---

## 🔗 Links úteis
- [RDS User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [RDS vs Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-compare.html)
- [Using RDS with Lambda](https://docs.aws.amazon.com/lambda/latest/dg/services-rds-tutorial.html)
