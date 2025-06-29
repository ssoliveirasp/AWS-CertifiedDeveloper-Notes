# AWS Elastic Load Balancer (ELB/ALB/NLB) – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço gerenciado para distribuir automaticamente o tráfego entre múltiplas instâncias ou containers.
- Melhora a disponibilidade e escalabilidade das aplicações.
- Existem três tipos principais:
  - **Classic Load Balancer (CLB)** – legado, básico para HTTP/HTTPS e TCP.
  - **Application Load Balancer (ALB)** – camada 7, ideal para HTTP/HTTPS com roteamento avançado.
  - **Network Load Balancer (NLB)** – camada 4, ultra rápido e para tráfego TCP/UDP de alta performance.

## ⚙️ Características principais

| Tipo         | Camada       | Suporte Protocolo            | Casos de Uso Típicos                  |
|--------------|--------------|-----------------------------|-------------------------------------|
| CLB          | 4 e 7        | HTTP, HTTPS, TCP            | Aplicações legadas                  |
| ALB          | 7 (HTTP/HTTPS)| HTTP, HTTPS, WebSockets     | Microservices, roteamento baseado em caminho ou host |
| NLB          | 4 (TCP/UDP)  | TCP, UDP, TLS               | Altíssima performance e baixa latência, cargas pesadas |

- ALB suporta:
  - Roteamento baseado em URL (path-based) e hostname (host-based).
  - Suporte nativo para WebSockets.
  - Autenticação via OIDC/SAML com integração Cognito.
- NLB suporta IP estático e endereços Elastic IP.

## 🔐 Segurança
- Integração com **AWS Certificate Manager (ACM)** para TLS/SSL.
- Suporte a Security Groups (ALB) e Network ACLs (NLB).
- Logs de acesso podem ser enviados para S3 para auditoria.

## 🧪 Perguntas comuns na prova

### Q: Quero balancear tráfego HTTP com roteamento por URL
✅ Use ALB com regras de listener baseadas em path ou host

### Q: Preciso de alta performance para TCP com baixa latência
✅ Use NLB para cargas intensivas em TCP/UDP

### Q: Quero usar WebSockets na minha aplicação
✅ ALB suporta WebSockets nativamente

### Q: Preciso de IP fixo para load balancer
✅ NLB suporta Elastic IPs, ALB não

### Q: Quero usar HTTPS com certificado gerenciado
✅ Use ACM para fornecer certificados para ALB ou NLB com TLS

### Q: Desenvolvedor configurou um ALB, mas esqueceu de associar target groups. Que erro aparecerá nos logs?
✅ HTTP 503 - Service Unavailable

### Q: Um ELB com cross-zone load balancing ativado distribui tráfego entre 2 instâncias na AZ1 e 8 na AZ2. Quanto de tráfego cada instância da AZ1 recebe?
✅ Cada instância da AZ1 recebe 10% do tráfego, com o cross-zone ativo, o ELB ignora a zona e distribui igualmente entre todas as 10 instâncias.

### Q: Como analisar latência e IP dos clientes em um Application Load Balancer?
✅ Usar ALB access logs

---

## 📌 Dicas rápidas
- `ALB` é o mais usado para aplicações web modernas e microservices.
- `NLB` é ideal para aplicações que exigem performance de rede pura.
- `CLB` é legacy e deve ser evitado em novos projetos.
- `Health Checks` para garantir que o load balancer envia tráfego apenas para instâncias saudáveis.
- `ALB access logs` registram detalhes completos de cada requisição, incluindo IP de origem, latência, tempo de resposta.

---

## 🔗 Links úteis
- [Elastic Load Balancing User Guide](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)
- [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)
- [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html)
