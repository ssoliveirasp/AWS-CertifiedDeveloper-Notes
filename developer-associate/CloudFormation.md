# AWS CloudFormation – Resumo para AWS Developer Certification (DVA-C02)

## 🧠 Conceitos-chave
- Serviço de **Infraestrutura como Código (IaC)** da AWS.
- Permite criar, atualizar e gerenciar recursos AWS usando templates YAML ou JSON.
- Garante **reprodutibilidade, versionamento e automação** da infraestrutura.

## 🛠️ Componentes principais
- **Stack**: conjunto de recursos AWS criados e gerenciados juntos.
- **Template**: arquivo JSON ou YAML que define recursos, parâmetros, outputs e dependências.
- **Change Sets**: revisão prévia das mudanças antes de atualizar uma stack.
- **Stacks Aninhadas**: reutilização de templates via referência em outros templates.

## ⚙️ Recursos importantes
- **Parâmetros**: entrada dinâmica para customizar stacks.
- **Outputs**: valores exportados após criação (ex: Endpoints, IDs).
- **Mappings**: tabelas estáticas para valores condicionais (ex: região → AMI).
- **Condicionais**: criação condicional de recursos.

## 🔄 Ciclo de vida
1. Criar stack (template + parâmetros)
2. CloudFormation provisiona recursos na ordem correta.
3. Pode atualizar stack com novas versões do template.
4. Se erro, faz rollback automático (configurável).

## 🔐 Permissões
- Usado com **IAM roles/policies** para controlar quem pode criar/atualizar stacks.
- Stacks podem criar roles para recursos (ex: EC2 instance profile).

## 🧪 Perguntas comuns no exame

### Q: Quero criar infraestrutura versionada e reproduzível
✅ Use CloudFormation

### Q: Quero revisar mudanças antes de aplicar atualização
✅ Use Change Sets

### Q: Preciso passar valores dinâmicos para template (ex: nome da VPC)
✅ Use Parâmetros

### Q: Quero compartilhar outputs entre stacks diferentes
✅ Use Export/Import via Outputs e `Fn::ImportValue`

### Q: Preciso criar recursos apenas em algumas regiões
✅ Use Mappings + Condicionais

### Q: Quero reaproveitar código entre templates
✅ Use Stacks Aninhadas (Nested Stacks)

### Q: Preciso rodar comandos pós-criação no EC2
✅ Use AWS::CloudFormation::Init ou UserData (menos comum no dev)

### Q: Um stack no CloudFormation falhou ao ser implantado na us-east-2 com export ELBDNSName. Qual o motivo?
✅ Exported Output Values devem ter nomes únicos por região no CloudFormation.

## 📌 Dicas rápidas
- **Funções Intrínsecas** importantes:
  - `!Ref` — referência simples (ex: parâmetro, recurso).
  - `!GetAtt` — obter atributo de recurso (ex: IP, ARN).
  - `!Sub` — substituição de strings com variáveis.
  - `!ImportValue` — importar output de outro stack.
- Sempre valide templates antes de aplicar (`aws cloudformation validate-template`).
- Change Sets evitam erros inesperados em produção.
- Pode usar junto com CodePipeline para deploy automatizado de infra.

---

## 🔗 Links úteis
- [CloudFormation User Guide](https://docs.aws.amazon.com/cloudformation/index.html)
- [Intrinsic Functions](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference.html)
- [Change Sets](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/using-cfn-updating-stacks-changesets.html)
