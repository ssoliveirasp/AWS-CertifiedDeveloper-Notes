# Amazon API Gateway – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado para criar, publicar, manter, monitorar e proteger APIs RESTful e WebSocket.
- Suporta APIs REST, HTTP e WebSocket.
- Integração nativa com **AWS Lambda**, backend HTTP, AWS services e Mock integrations.

## ⚙️ Tipos de API
- **REST API** (mais tradicional, robusta)
- **HTTP API** (mais leve, custo menor, latência menor, ideal para Lambda e HTTP backends)
- **WebSocket API** (para comunicação bidirecional em tempo real)

## 🔄 Ciclo de vida da API
- Criar recursos e métodos (GET, POST, etc).
- Configurar integração com backend (Lambda, HTTP, Mock).
- Configurar mapeamentos e transformações de payload (Mapping Templates).
- Deployar API em stages (ex: dev, prod).

## 🔐 Segurança e Autenticação
- **API Keys** – controle básico, para limitar uso.
- **IAM Roles/Policies** – controle por assinatura de requisição AWS SigV4.
- **Cognito User Pools** – autenticação OAuth2, JWT.
- **Lambda Authorizers** – autenticação customizada (JWT ou token custom).
- **Usage Plans** – limitar taxa e quota por API Key.

## 📈 Monitoramento e Logs
- Logs de acesso via **CloudWatch Logs** (configurar no stage).
- Métricas de uso via **CloudWatch Metrics** (latência, erros, count).
- Pode habilitar **X-Ray** para tracing.

## 🧪 Perguntas comuns no exame

### Q: Quero criar API para invocar funções Lambda
✅ Use API Gateway com integração Lambda Proxy (simplifica passagem de dados).

### Q: Quero limitar requisições por cliente (rate limiting)
✅ Use API Keys + Usage Plans.

### Q: Quero autenticar usuários via Cognito em API Gateway
✅ Configure Cognito User Pool Authorizer.

### Q: Preciso transformar requisições/ respostas (ex: JSON → XML)
✅ Use Mapping Templates em Integration Request/Response.

### Q: Preciso expor API com baixa latência e custo reduzido
✅ Use HTTP APIs (mais simples que REST APIs).

### Q: Preciso controle total e customização avançada
✅ Use REST APIs.

### Q: Como dar acesso beta para devs a uma nova versão da API Gateway, sem afetar clientes atuais?
✅ Criar um stage de desenvolvimento no API Gateway e direcionar os devs para ele.

## 📌 Dicas rápidas
- REST APIs têm mais recursos (modelos, caching, WAF).
- HTTP APIs são recomendadas para integração simples com Lambda e HTTP backend.
- WebSocket APIs para aplicações que precisam comunicação bidirecional.
- Para segurança, IAM e Cognito são padrão para produção.
- Lambda Authorizers são úteis para lógica custom de autenticação/autorização.

---

## 🛠️ Exemplo básico de integração Lambda Proxy
- No método (ex: POST), defina integração com Lambda.
- Marque opção **Use Lambda Proxy Integration**.
- Lambda recebe evento com `body`, `headers`, `pathParameters`, etc.
- Lambda retorna JSON formatado com statusCode e body.

---

## 🔗 Links úteis
- [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [API Gateway Lambda Proxy Integration](https://docs.aws.amazon.com/apigateway/latest/developerguide/set-up-lambda-proxy-integrations.html)
- [API Gateway HTTP APIs](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api.html)
