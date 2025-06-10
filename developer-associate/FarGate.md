# AWS Fargate – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço de **container serverless** da AWS.
- Executa containers **sem necessidade de provisionar/manter EC2s**.
- Pode ser usado com:
  - **Amazon ECS**
  - **Amazon EKS (limitações específicas)**

## 🚀 Vantagens principais
- Sem gerenciamento de servidores (EC2).
- Escala automática e rápida.
- Paga somente por **vCPU + memória + tempo de execução**.
- Ideal para microsserviços, jobs assíncronos e aplicações event-driven.

## 📦 Componentes principais (via ECS)
- **Task Definition** – blueprint do container (imagem, CPU, RAM, env vars).
- **Task** – instância em execução da Task Definition.
- **Service** – mantém tasks ativas, pode usar Load Balancer.
- **Cluster** – necessário mesmo em Fargate (gerenciado pela AWS).

## 🔐 Permissões
- Usa **IAM Task Role** para dar permissões ao container (ex: S3, DynamoDB).
- Usa **IAM Execution Role** para permitir ao Fargate criar logs, puxar imagem do ECR.

## 🔁 Integrações comuns
- **CloudWatch Logs** – envio automático de logs se configurado na Task Definition.
- **ECR** – repositório de imagens Docker.
- **ALB (Application Load Balancer)** – usado para exposição de serviços HTTP.
- **EventBridge** – pode iniciar Tasks sob demanda ou programadas (cron/eventos).

## 🧪 Perguntas comuns no exame

### Q: Preciso rodar container sem gerenciar servidores
✅ **Use ECS com Fargate**

### Q: Preciso rodar uma task sob evento CloudWatch/EventBridge
✅ **Configure Rule para chamar ECS RunTask com Fargate**

### Q: Preciso que o container tenha acesso ao S3
✅ **Anexar IAM Task Role com permissão S3 à Task Definition**

### Q: Preciso coletar logs dos containers
✅ **Configure logDriver para CloudWatch Logs**

### Q: Quero deploy com baixa latência e rápida escalabilidade
✅ **Use ECS com Fargate + Service + ALB**

## 📌 Dicas rápidas
- Suporte a somente **Linux containers**.
- Fargate **não permite acesso direto à infraestrutura** (sem SSH, sem daemon).
- **Limite de vCPU/memória por task**:
  - Ex: 0.25 vCPU / 0.5 GB RAM até 4 vCPU / 30 GB RAM (podem mudar).
- **ECS Anywhere** ≠ Fargate: ECS Anywhere é para execução em servidores on-premises.
- Use **Platform Version 1.4.0+** para recursos modernos como EFS, secrets, etc.

---

## 🛠️ Exemplo de Task Definition para Fargate (resumo)
```json
{
  "family": "my-app-task",
  "executionRoleArn": "arn:aws:iam::123456789012:role/ecsTaskExecutionRole",
  "networkMode": "awsvpc",
  "requiresCompatibilities": ["FARGATE"],
  "cpu": "512",
  "memory": "1024",
  "containerDefinitions": [
    {
      "name": "app",
      "image": "123456789012.dkr.ecr.us-east-1.amazonaws.com/myapp:latest",
      "logConfiguration": {
        "logDriver": "awslogs",
        "options": {
          "awslogs-group": "/ecs/myapp",
          "awslogs-region": "us-east-1",
          "awslogs-stream-prefix": "ecs"
        }
      }
    }
  ]
}
