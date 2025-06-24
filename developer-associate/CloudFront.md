# Amazon CloudFront – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceito geral
- Serviço de **CDN (Content Delivery Network)** da AWS.
- Distribui conteúdo com **baixa latência** e **alta performance**.
- Usa uma rede global de **Edge Locations** para cache de conteúdo.

---

## ⚙️ Funcionalidades principais

### ✅ Distribuição de conteúdo
- **Estático**: HTML, CSS, JS, imagens (de S3, por exemplo).
- **Dinâmico**: APIs, vídeos, apps.

### ✅ Origem (origin)
- Pode ser:
  - S3 bucket
  - HTTP server (EC2, ALB, API Gateway, etc.)

### ✅ Cache e performance
- Usa **Edge Locations** para cache local.
- TTL (Time to Live) configurável.
- Suporte a **invalidation** para forçar atualização do cache.
- **failover de origem** permite usar duas origens em caso de falha na primária, redireciona para a secundária, garantindo alta disponibilidade.

### ✅ Segurança
- Integração com **AWS WAF** para proteger contra ataques web.
- **Signed URLs / Signed Cookies** para controle de acesso ao conteúdo.
- HTTPS com **certificados do ACM** (via SNI).
- Integra com **Shield** para proteção DDoS.
- **Origin Access Control (OAC)** e **Origin Access Identity (OAI)** para restringir acesso ao S3 somente via CloudFront.

---

## 🔐 Integrações
- 🔐 **S3 + CloudFront**: distribui arquivos públicos ou privados.
- 🔐 **API Gateway + CloudFront**: acelera resposta de APIs.
- 🔐 **Lambda@Edge**: executa código JS nas edge locations para modificar requisições e respostas.

---

## 🧪 Perguntas comuns na prova

### Q: Como proteger acesso a arquivos S3, permitindo apenas via CloudFront?
✅ Use **Origin Access Control (OAC)** ou **OAI**.

### Q: Como melhorar a performance global de um site hospedado no S3?
✅ Configure um **CloudFront Distribution** apontando para o bucket.

### Q: Como garantir que usuários vejam conteúdo atualizado?
✅ Use **Cache Invalidation** via API ou console.

### Q: Como entregar conteúdo apenas para usuários autenticados?
✅ Use **Signed URLs** ou **Signed Cookies**.

### Q: Qual das credenciais de segurança só pode ser criada pelo root user da conta AWS?
✅ CloudFront Key Pairs. Usadas para assinar URLs e cookies no CloudFront.

---

## 📌 Dicas rápidas
- TTL define por quanto tempo o conteúdo fica cacheado nas Edge Locations.
- Invalidation pode ter custo adicional (primeiras 1.000/mês gratuitas
