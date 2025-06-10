# Amazon EKS – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado de **Kubernetes** na AWS.
- Permite rodar aplicações containerizadas com **controle total via Kubernetes API**.
- Mais poderoso, porém mais complexo que ECS.

## 🧱 Componentes principais
- **Cluster EKS** – gerenciado pela AWS (control plane).
- **Worker Nodes** – EC2 ou Fargate (executam os pods).
- **Pods** – menor unidade de execução no Kubernetes (geralmente um ou mais containers).
- **Node Groups** – grupo de EC2s para o cluster.

## ⚙️ Modos de execução
- **EKS com EC2**:
  - Você gerencia os nós com EC2 Auto Scaling Groups.
  - Mais controle e flexibilidade.
- **EKS com Fargate**:
  - Sem necessidade de EC2s — execução 100% serverless.
  - Ideal para workloads simples e event-driven.

## 🔐 Permissões e IAM
- EKS usa **IAM para autenticação** e **RBAC do Kubernetes para autorização**.
- Cada Pod pode usar um **IAM Role via IRSA** (IAM Roles for Service Accounts).
- Permissões do cluster controladas via:
  - **aws-auth ConfigMap** (vincula IAM users/roles com permissões Kubernetes).

## 🔁 Integrações importantes
- **IAM Roles for Service Accounts (IRSA)** → dá permissões específicas por Pod.
- **CloudWatch Container Insights** → monitoramento.
- **ECR** → para armazenar imagens.
- **Load Balancer Controller** → para expor apps via ALB ou NLB.

## 🧪 Perguntas comuns no exame

### Q: Preciso executar containers com Kubernetes sem gerenciar o plano de controle
✅ **Use Amazon EKS**

### Q: Cada Pod precisa de permissão específica (ex: S3, DynamoDB)
✅ **Use IRSA (IAM Roles for Service Accounts)**

### Q: Preciso rodar container em Kubernetes sem instância EC2
✅ **Use EKS com Fargate**

### Q: Desenvolvedor precisa acessar cluster com permissões limitadas
✅ **Configure RBAC no Kubernetes + aws-auth map**

### Q: Preciso de um cluster gerenciado para workloads compatíveis com Kubernetes
✅ **Amazon EKS**

## 📌 Dicas rápidas
- IAM controla **quem pode acessar** o cluster.
- RBAC controla **o que pode ser feito** dentro do cluster.
- **IRSA** é o padrão ouro para acesso seguro a serviços AWS via Pod.
- Fargate no EKS é ótimo para workloads pequenos, mas tem limitações (ex: suporte a DaemonSets, etc.).

---

## 🛠️ Exemplo: Permitir Pod acessar S3 com IRSA
1. Criar OIDC provider para o cluster.
2. Criar IAM Role com trust policy para service account do Pod.
3. Vincular Role via annotation no manifest Kubernetes:
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: s3-access-sa
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::123456789012:role/S3AccessRole
