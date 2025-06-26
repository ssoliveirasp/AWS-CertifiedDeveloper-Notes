# Amazon EC2 – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço de **infraestrutura como serviço (IaaS)**.
- Permite criar e gerenciar **máquinas virtuais (instâncias)** na nuvem.
- Suporte para múltiplos sistemas operacionais e tipos de instância.
- Uso típico: aplicações legadas, scripts de background, servidores de app/banco.

## 🧱 Componentes principais
- **AMI (Amazon Machine Image)** – imagem da instância.
- **Instance Type** – define CPU, RAM, rede, etc.
- **Security Group** – firewall virtual (controle de portas/serviços).
- **Key Pair** – usada para acesso SSH.
- **Elastic IP** – IP público fixo opcional.
- **EBS (Elastic Block Store)** – volumes persistentes.

## ⚙️ Auto Scaling & Elastic Load Balancer (ELB)
- **Auto Scaling Group (ASG)**: cria/destroi instâncias com base em demanda.
- **ELB**: distribui requisições entre instâncias.

## 🔐 Permissões e IAM
- EC2 pode ter uma **IAM Role associada** → usada para acessar outros serviços (ex: S3, CloudWatch).
- Exemplo: EC2 grava logs no CloudWatch → IAM Role com permissão `logs:PutLogEvents`.

## 🧪 Perguntas comuns no exame

### Q: Preciso que a instância EC2 acesse o S3
✅ **Anexar IAM Role com política S3 à instância EC2**

### Q: Preciso monitorar CPU e reiniciar automaticamente se falhar
✅ **Use CloudWatch Alarm + Auto Recovery**

### Q: Aplicação precisa escalar automaticamente conforme carga
✅ **Use Auto Scaling Group com métrica de CPU**

### Q: EC2 precisa logar dados em tempo real
✅ **Instalar agente do CloudWatch Logs + IAM Role**

### Q: Instância deve ser acessada apenas via porta 443 (HTTPS)
✅ **Configurar Security Group liberando apenas porta 443**

### Q: Backup automático de dados da instância
✅ **Use Snapshots dos volumes EBS**

### Q: Sobre o user data no EC2, quais afirmações são verdadeiras?
✅ Por padrão, os scripts de `user data` são executados como root
✅ Por padrão, o `user data` roda apenas no primeiro boot

### Q: Por que usar Elastic Load Balancer em EC2 espalhadas por regiões e AZs?
✅ Garante alta disponibilidade
✅ Separa tráfego público e privado

### Q: Você quer parar uma instância EC2 na região us-east-2, mas sua CLI está configurada com us-east-1 como padrão. Qual a melhor forma?
✅ Usar o parâmetro --region

### Q: ELB marca todas as instâncias EC2 como unhealthy, mas o acesso direto pelo IP funciona. Quais podem ser os motivos? (Escolha 2)
✅ O security group da EC2 não permite tráfego do security group do ALB
✅ A rota (path) da health check está configurada incorretamente

## 📌 Dicas rápidas
- Security Groups são **stateful** (resposta é automaticamente liberada).
- Pode associar IAM Role **somente no momento de criação**, ou depois via console/API.
- EC2 pode gerar eventos para **CloudWatch Events/EventBridge**.
- **User Data**: scripts shell executados no 1º boot (ex: instalar app, baixar configs).
- **Spot Instances** são baratas, mas podem ser interrompidas (não ideais para produção).
- **Launch Template** define configurações para instâncias EC2, como ID da AMI, tipo da instância, par de chaves, grupos de segurança e outros parâmetros..
- **Dedicated Instances** rodam em Servidor exclusivo (Hardware) dedicado para um único cliente
- **Dedicated Host** servidor físico totalmente dedicado a você.

---

## 📦 Exemplo de User Data (script de bootstrap)
```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
