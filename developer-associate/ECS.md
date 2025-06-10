# Amazon ECS – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço de **orquestração de containers** (semelhante ao Kubernetes).
- Gerencia execução de **containers Docker**.
- Suporta dois modos de execução:
  - **EC2 Launch Type** – você gerencia as instâncias.
  - **Fargate Launch Type** – serverless, a AWS gerencia a infraestrutura.

## 📦 Componentes principais
- **Task Definition** – blueprint da aplicação containerizada (imagem, CPU, memória, env vars).
- **Task** – execução de uma Task Definition.
- **Service** – garante que um número fixo de Tasks esteja rodando.
- **Cluster** – grupo lógico de recursos (instâncias ou Fargate).

## ⚙️ Modos de execução
### 🔸 EC2 Launch Type
- Você provisiona e gerencia EC2s.
- Mais controle, mas mais complexidade.

### 🔹 Fargate Launch Type
- Totalmente gerenciado.
- Você só define CPU, RAM e imagem.
- Ideal para workloads event-driven ou escala automática.

## 🔐 Permissões
- ECS usa uma **Task Execution Role (IAM Role)** para puxar a imagem do ECR e logar no CloudWatch.
- **Task Role** é usada **pelo container** para acessar serviços AWS (ex: DynamoDB, S3).
- Importante: execution role ≠ task role.

## 🔁 Integrações úteis
- **Application Load Balancer** para distribuir requisições HTTP/S.
- **ECR** para armazenar imagens Docker.
- **CloudWatch Logs** para capturar logs de container.
- **EventBridge** para disparar tasks sob demanda (ex: tarefas periódicas).

## 🧪 Perguntas comuns no exame

### Q: Preciso rodar containers sem gerenciar servidores
✅ **Use ECS com Fargate**

### Q: Container precisa acessar DynamoDB com segurança
✅ **Anexe uma Task Role com permissões do DynamoDB**

### Q: Preciso executar tarefa sob demanda baseada em evento
✅ **EventBridge → ECS RunTask**

### Q: Gerenciar 3 réplicas de um container REST
✅ **Definir ECS Service com desiredCount = 3**

### Q: Preciso coletar logs dos containers
✅ **Usar CloudWatch Logs via configuração na Task Definition**

## 📌 Dicas rápidas
- **Task Definition** pode ter múltiplos containers (multi-container app).
- **Port mappings** definem como tráfego entra no container.
- Fargate é **pago por vCPU + RAM + tempo de execução**.
- Service com ALB precisa registrar as tasks no target group.
- Pode usar **Secrets Manager ou SSM Parameter Store** para variáveis seguras.

---

## 🛠️ Exemplo de Task Definition (trecho simplificado em JSON)
```json
{
  "containerDefinitions": [
    {
      "name": "meu-app",
      "image": "meu-repo.ecr.aws/app:latest",
      "memory": 512,
      "cpu": 256,
      "essential": true,
      "logConfiguration": {
        "logDriver": "awslogs",
        "options": {
          "awslogs-group": "/ecs/meu-app",
          "awslogs-region": "us-east-1",
          "awslogs-stream-prefix": "ecs"
        }
      }
    }
  ]
}
