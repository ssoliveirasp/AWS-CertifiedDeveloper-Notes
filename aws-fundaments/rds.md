# RDS - Relational Database Service

## Definição
    RDS é um serviço gerenciado pela AWS para banco de dados que utilizam SQL para queries.

## Suporta os seguintes bancos de dados:
     - PostgreSQL.
     - Oracle.
     - MySQL.
     - MariaDB.
     - Microsoft SQL Server.
     - Aurora (banco de dados desenvolvido pela AWS).  

## Vantagens entre RDS vs EC2 + Banco de dados
    - RDS é gerenciado pela AWS.
    - Patching é responsabilidade pela AWS.
    - Backups contínuos. Banco de dados pode ser restaurado para um timestamp.
    - Painel de controle para monitoramento.
    - Read replicas para otimizar leituras.
    - Opção de configuração para Multi Availability Zone para recuperação após desastres.
    - Janela de manutenção para upgrades.
    - Escalonamento (vertical e horizontal).
    - Não é possível acesso via SSH no RDS.

## RDS - Read réplica
    - Até 5 read replicas.
    - Podem estar na mesma ou diferentes Availability Zones.
    - Podem estar em diferentes Regions.
    - Réplicas são assíncronas (async/eventually consistent).
    - Réplicas podem virar Master.
    - Aplicações devem atualizar string de conexão para usar Read Replica.

## RDS - Read réplica em Multi Availability Zone
    - Réplica é síncrona (sync).
    - Usam um único DNS name.
    - Automaticamente direciona os acessos para o banco **Stand-by** quando há o failover.
    - Aumenta a disponibilidade.
    - Failover em caso de perda de AZ e rede.
    - Sem necessidade de intervenção.
    - Não é usado para escalonamento.

## RDS - Availability and Durability

### Deployment Options

#### Single DB Instance

    - Cria uma `instancia unica` sem instancias de standby.

#### Multi-AZ DB instance

    - Cria uma `Primary Instance` e uma `Standby Instance` em `diferentes AZ`. 
    - Não suporta conexão com a instancia de Standby.
    - Provem `Alta Disponibilidade`.

#### Multi-AZ DB Cluster

    - Cria um `Cluster` com um `Primary Instance` e duas `Instancias Standby` em `diferentes AZ`.
    - Suporta conexão de leitura com as `Instancias Standby` atraves do endpoint do tipo `Reader Instance`.
    - Provem `Alta Disponibilidade`.
    
## RDS - StorageScaling

  ### Elastic Block Storage (EBS)

  #### Bancos 
      - MySql, PostgreSQL, MariaDB, Oracle, SQL Server.

  #### Tipos

  ##### General Purpose SSD Storage
     - Provem latencia em milisegundos de apenas um digito.
     - Custo efetivo
     - Limites dados primarios
        - Minimo de 20 GiB
        - Maximo de 64 TiB (Sql Server 16 TiB)

   ##### Provisioned IOPS (SSD) Storage
     - Bom para cargas de trabalho (workloads) com alto (I/O)
     - IOPS
       - Minimo 8.000.
       - Maximo 80.000 (SQL Server 40.000).
     - Storage Primary Data
       - Minimo 100 GiB.
       - Maximo de 64 TiB (Sql Server 16 TiB).
   
   #### Shared Cluster Storage
       - Banco: Amazon Aurora.

   #### Storage AutoScaling
       - Feature quando habilitada permite aumentar capacidade até seu limite GiB configurado  (Maximum storage threshold). 
         - Minimo: 101 Gib
         - Maximo: 65536 GiB (Aprox. 70 TB)

## RDS - Backup

    - Backup é automático e:
      - Snapshot diário completo do banco de dados.
      - Registra log de todas as transações em tempo real.
      - Possível recuperar o banco de dados em qualquer timestamp.
      - 7 dias de backup por padrão podendo ser aumentado até 35 dias.
    - Snapshot do banco de dados:
      - Iniciado pelo usuário.
      - Snapshot pode ser guardado por quanto tempo o usuário quiser.

## RDS - Criptografia

    - Criptografia em repouso com AWS KMS (AES-256).
    - Certificado SSL para criptografar banco de dados em trânsito.
    - Para forçar SSL:
      - PostgreSQL: `rds.force_ssl=1` no console RDS (**Parameter Group**).
      - MySQL: dentro do banco de dados basta executar `GRANT USAGE ON '.' TO 'mysqluser'@'%' REQUIRE SSL`.
    - Para conectar usando SSL:
      - Entre com o SSL trust certificate (pode ser baixado na AWS).
      - Entre com a opção SSL quando conectar ao banco de dados.

## RDS - Segurança
    - Banco de dados RDS normalmente é criado em uma rede privada.
    - RDS usa security groups da mesma forma que o EC2 para definir regras de acesso.
    - IAM Policies definem quem pode gerenciar dados no RDS.
    - Usuário e senha podem ser usados para logar no banco de dados.
    - IAM users também podem ser usados para autenticação (MySQL e Aurora).
    
## RDS vs Aurora
    - Aurora é um BD proprietário da AWS.
    - PostgreSQL e MySQL são suportados pelo Aurora. Isso significa que podemos utilizar o Aurora como se fosse um dos dois bancos.
    - Aurora foi desenvolvido para nuvem e segundo a AWS ele é 5x mais rápido que MySQL RDS e 3x mais rápido que PostgreSQL RDS.
    - Armazenamento Aurora cresce automaticamente em incrementos de 10GB, até 64TB.
    - Aurora pode ter até 15 Read replicas com latência abaixo de 10ms enquanto o MySQL fica até 5ms.
    - Failover no Aurora é instantâneo. Usa HA nativo.
    - Aurora custa 20% mais que RDS, porém é mais eficiente.
