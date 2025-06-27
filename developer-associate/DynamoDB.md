# DynamoDB – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Banco de dados **NoSQL totalmente gerenciado**.
- Armazena dados em **tabelas** com **chave primária** obrigatória.
- Chave primária pode ser:
  - Simples: apenas **Partition Key**.
  - Composta: **Partition Key + Sort Key**.
- Escalável automaticamente (on-demand ou provisionado).

## 🔐 Permissões
- Controladas via **IAM Policies**.
- Também suporta **fine-grained access control** com base no item.
- Autorização por **atributo de usuário (token JWT ou Cognito)**.

## 🚀 Performance e Escalabilidade
- Baixa latência (<10 ms).
- **Provisioned** ou **On-Demand** throughput.
- Unidades de capacidade:
  - **RCU** (Read Capacity Unit)
  - **WCU** (Write Capacity Unit)
- **DAX** (DynamoDB Accelerator) → cache in-memory com latência <1ms.
- **Global Tables** → replicação multi-região.

## 📦 Indexes
- **LSI** (Local Secondary Index): mesma Partition Key, Sort Key diferente. Criado junto com a tabela.
- **GSI** (Global Secondary Index): Partition e Sort Keys diferentes. Criado a qualquer momento.

## 🔁 Streams
- **DynamoDB Streams**: captura alterações (inserção, modificação, exclusão).
- Pode acionar **AWS Lambda** para eventos near real-time.

## 💣 TTL (Time to Live)
- Expiração automática de itens com base em um campo de data/hora.

## 🧪 Perguntas comuns no exame

### Q: Preciso escalar automaticamente sem definir capacidade
✅ **Use modo On-Demand**

### Q: Cache para reduzir latência de leitura
✅ **Use DAX**

### Q: Quero escutar eventos quando dados mudam
✅ **Use DynamoDB Streams + Lambda**

### Q: Permitir acesso somente ao item do usuário logado
✅ **Fine-Grained Access Control + Cognito Identity or IAM Role**

### Q: Preciso de outro índice com mesma Partition Key e outra ordenação
✅ **Use LSI**

### Q: Preciso indexar com outra chave totalmente diferente
✅ **Use GSI**

### Q: Replicação automática entre regiões
✅ **Global Tables**

### Q: Otimizar leitura eventual, com menor custo
✅ **Eventually consistent**

### Q: Como modelar dados de jogos com nome, versão e categoria, incluindo info adicional variável, e permitir buscas por nome, versão e categoria?
✅ Criar uma tabela DynamoDB com name como partition key e version como sort key.
✅ Criar um Global Secondary Index (GSI) com category como partition key e name como sort key.

### Q: Como fazer os dados do DynamoDB expirarem automaticamente após uma semana?
✅ Usar TTL (Time To Live)