# AWS IAM – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Gerencia **identidades e permissões** para acessar recursos AWS.
- Principais componentes:
  - **Users** – acesso individual (console/API).
  - **Groups** – agrupam usuários e políticas.
  - **Roles** – acessos temporários, usados por serviços ou usuários externos.
  - **Policies** – definem permissões (JSON).

## 📄 Tipos de Policies
- **IAM Policy** (user-based): ligada a usuários, grupos ou roles.
- **Resource-based Policy**: ligada diretamente ao recurso (ex: S3, Lambda).
- **Permissions Boundaries**: limita o que uma role/policy pode fazer (controle superior).
- **Service Control Policies (SCPs)**: usada em AWS Organizations (não cai muito nessa prova).

## 🔐 Assunção de Role
- Role pode ser assumida por:
  - **Serviço AWS** (ex: Lambda → S3).
  - **Usuário IAM com `sts:AssumeRole`**.
  - **Usuário federado ou identidade externa** (ex: SSO, Cognito, OIDC).

## ⚙️ Boas práticas de segurança
- **MFA (Multi-Factor Authentication)** para usuários e root.
- **Principle of Least Privilege** sempre.
- Use **roles para aplicações**, **users para pessoas**.
- Nunca use usuário root no dia a dia.
- Utilize **IAM Access Analyzer** para encontrar acessos públicos indevidos.

## 🧪 Perguntas comuns no exame

### Q: Permitir que Lambda acesse S3 e DynamoDB
✅ **Crie Execution Role com política anexada**

### Q: Usuário só pode listar objetos de um bucket específico
✅ **IAM Policy com `"Action": "s3:ListBucket"` e `"Resource": "arn:aws:s3:::meu-bucket"`**

### Q: Preciso permitir outro serviço (ex: EventBridge) invocar minha Lambda
✅ **Resource-based policy na função Lambda**

### Q: Limitar escopo de permissões de uma role
✅ **Use Permission Boundary**

### Q: Conceder acesso temporário a recurso por token externo (ex: login via Google)
✅ **Use Federated Identity (ex: Cognito ou OIDC)**

### Q: Conceder permissão de login temporário via API
✅ **Use `sts:AssumeRole`**

### Q: Como permitir que uma Lambda acesse S3 com segurança?  
✅ Anexe uma **IAM Role** com permissão `s3:*` ao Lambda.

### Q: Quais entidades da AWS podem ser usadas para implantar certificados SSL/TLS? (Escolha 2)
✅ IAM
✅ AWS Certificate Manager (ACM)
**IAM pode armazenar e gerenciar certificados para alguns serviços, como CloudFront. Já o ACM é a opção recomendada para gerenciar certificados SSL/TLS com renovação automática e fácil integração com serviços como ELB e API Gateway.**

### Q: Qual é a única resource-based policy suportada pelo serviço IAM?
✅ Trust policy

### Q: Finance recebeu política IAM para acessar o Billing, mas não conseguem ver o serviço no console. Por quê?
✅ É necessário ativar o acesso IAM ao Billing no console para os usuários.

## 📌 Dicas rápidas
- `"Effect": "Allow"` ou `"Deny"` são obrigatórios em cada statement.
- Use `"*"` com muito cuidado — é perigoso e só em situações controladas.
- Políticas são aplicadas de forma **acumulativa** (exceto negações).
- **Explicit Deny** sempre vence um Allow.
**trust policies** são aplicadas a roles (funções) no IAM e definem quem pode assumir a role ("sts:AssumeRole").


---

## 📦 Exemplo de IAM Policy (JSON)
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:PutObject", "s3:GetObject"],
      "Resource": "arn:aws:s3:::meu-bucket/*"
    }
  ]
}
