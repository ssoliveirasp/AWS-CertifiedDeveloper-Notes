# AWS Lambda – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- **Compute serverless** baseado em eventos.
- Executa **funções sem gerenciar servidores**.
- Suporta várias linguagens: Node.js, Python, Java, C#, Go, Ruby, etc.
- **Limite de execução:** até 15 minutos por invocação.
- **Modelo de billing:** por uso (tempo + memória).

## ⚙️ Execução
- Lambda executa código em **container isolado**.
- **Cold start:** ocorre no primeiro invoke ou após inatividade (especialmente em VPC).
- **Provisioned concurrency:** reduz impacto do cold start.

## 🧩 Integrações (principais triggers)
- **API Gateway** → serverless APIs.
- **S3** → trigger por upload (ex: processar imagem).
- **DynamoDB Streams** → processar eventos.
- **SNS / SQS** → fanout ou filas assíncronas.
- **CloudWatch Events / EventBridge** → agendamentos (cron).
- **Step Functions** → orquestração.

## 🔐 Permissões
- Lambda assume um **Execution Role (IAM Role)**.
- O serviço que chama a Lambda também precisa de permissões.
- Pode usar **resource-based policies** para permitir invocações de outros serviços.

## 🚀 Performance e Escalabilidade
- Escala automaticamente por invocação (concurrent executions).
- Padrão: **1.000 execuções concorrentes por conta** (limitável).
- Pode configurar **Memory (128MB–10GB)** → afeta CPU.
- **Ephemeral storage:** 512MB padrão, até 10GB configurável.

## 🧪 Perguntas comuns no exame

### Q: Preciso executar código em resposta a upload no S3
✅ S3 Event + Lambda Trigger

### Q: Garantir baixa latência em funções que sofrem cold start
✅ Provisioned Concurrency

### Q: Preciso processar mensagens de uma fila em ordem
✅ Use Lambda com SQS FIFO Queue

### Q: Garantir que Lambda possa acessar S3 e DynamoDB
✅ Execution

### Q: Como formatar a resposta de uma função Lambda chamada por API Gateway via requisição GET?
✅ Usar API Gateway Mapping Templates.
**Os Mapping Templates permitem transformar a resposta da Lambda antes de enviá-la ao cliente, controlando o formato e filtrando dados sensíveis ou desnecessários.**

### Q: Como evitar inconsistências e perda de dados em uma API Lambda que pode receber requisições duplicadas com IDs únicos?
✅ Persistir o ID único de cada requisição em uma tabela DynamoDB e fazer o Lambda verificar esse ID antes de processar.

### Q: Como reduzir o tempo médio de execução de uma função Lambda com uso intenso de CPU?
✅ Definir a memória no valor máximo ao implantar a função.