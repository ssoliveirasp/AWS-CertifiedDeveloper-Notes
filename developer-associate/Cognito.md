# AWS Cognito – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado para autenticação, autorização e gerenciamento de usuários.
- Suporta autenticação via usuários próprios ou provedores externos (Google, Facebook, SAML).
- Composto por duas partes principais:
  - **User Pools**: gerenciamento de diretórios de usuários e autenticação.
  - **Identity Pools (Federated Identities)**: fornece credenciais temporárias para acessar AWS services.

## ⚙️ Funcionalidades principais
- Registro, login, recuperação de senha e MFA para usuários.
- Suporte a OAuth 2.0, OpenID Connect e SAML 2.0.
- Integração fácil com AWS SDK para aplicações web e móveis.
- Identity Pools integra com IAM para fornecer permissões AWS temporárias.

## 🔐 Segurança
- Suporte a MFA (autenticação multifator).
- Criptografia dos dados dos usuários.
- Políticas IAM para controle granular do acesso federado.

## 🧪 Perguntas comuns na prova

### Q: Quero gerenciar usuários e autenticação da minha aplicação
✅ Use Cognito User Pools para autenticação e gerenciamento

### Q: Quero fornecer acesso temporário a serviços AWS para usuários autenticados
✅ Use Cognito Identity Pools para fornecer credenciais AWS temporárias

### Q: Quero integrar login via Google ou Facebook
✅ User Pools suportam provedores externos como IdP (Identity Provider)

### Q: Quero habilitar autenticação multifator para mais segurança
✅ Ative MFA no User Pool para proteção adicional

### Q: App .NET precisa de autenticação que retorne um JWT. Qual serviço AWS usar?
✅ Cognito User Pools

---

## 📌 Dicas rápidas
- User Pools cuidam da autenticação, Identity Pools cuidam da autorização para AWS resources.
- Integração com API Gateway para autenticar chamadas usando tokens JWT do User Pool.
- Permite customização via triggers Lambda para fluxo de autenticação.
- Ideal para apps móveis e web que precisam de login seguro e integração com AWS.

---

## 🔗 Links úteis
- [AWS Cognito Developer Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html)
- [Identity Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html)
