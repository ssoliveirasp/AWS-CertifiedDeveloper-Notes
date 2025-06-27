# AWS SAM (Serverless Application Model) – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 O que é o AWS SAM?
- Framework da AWS para **desenvolver, testar e implantar** aplicações **serverless**.
- Baseado no **CloudFormation**, com sintaxe simplificada para recursos como:
  - Lambda
  - API Gateway
  - DynamoDB
  - Step Functions
  - S3

---

## 🧪 Perguntas comuns no exame

### Q: Qual das opções NÃO é um tipo de recurso válido no AWS SAM?
❌ AWS::Serverless::UserPool

### Q: O que significa a seção Transform: 'AWS::Serverless-2016-10-31' em um documento YAML?
✅ Indica que o template é um AWS Serverless Application Model (SAM).

---

## ⚙️ Componentes principais

### ✅ Template simplificado (`template.yaml`)
- Define recursos serverless com menos código que o CloudFormation tradicional.
- Exemplo:
```yaml
Resources:
  MyFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.handler
      Runtime: nodejs18.x
      Events:
        HelloApi:
          Type: Api
          Properties:
            Path: /hello
            Method: get
