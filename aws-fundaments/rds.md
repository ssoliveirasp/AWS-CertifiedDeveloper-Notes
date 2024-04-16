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

- Réplica é síncrona (sync).
- Usam um único DNS name.
- Aumenta a disponibilidade.
- Sem necessidade de intervenção.
- Não é usado para escalonamento.
- Replicado Master e em cada replica.

## RDS - Failover Availability Zone
- Failover em caso de perda de AZ e rede.
- Automaticamente direciona os acessos para o banco **Stand-by** quando há o failover.
- em failover tempo de mudança de zona secundaria é de 60-120 segundos.

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

## DB Instance Types

GP - General Purpose (Standard Class - includes M Classes)
MO - Memory Optimized (includes r and x classes)
Burstable classes (includes t classes)


| Banco       | GP  | GP  | MO  | MO  | MO  |
| ----------- | --- | --- | --- | --- | --- |
| MySql       | T2  | T3  | R3  | X1  | Z1  |
| PostgresSQL | X   | X   | X   |     |     |
| MariaDB     | X   | X   | X   |     |     |
| Aurora      | X   |     | X   |     |     |
| Oracle      | X   |     | X   |     |     |
| SQL Server  | X   |     |     |     |     |
|             |     |     |     |     |     |


## RDS - Aurora

- PostgreSQL e MySQL são suportados pelo Aurora. 
- Aurora foi desenvolvido para nuvem e segundo a AWS ele é 5x mais rápido que MySQL RDS e 3x mais rápido que PostgreSQL RDS.
- Aurora custa 20% mais que RDS, porém é mais eficiente.
- Armazenamento Aurora cresce automaticamente em incrementos de 10GB, até 64TB.
- Failover no Aurora é instantâneo. Usa HA nativo.
- Aurora pode ter até 15 Read replicas com latência abaixo de 10ms enquanto o MySQL fica até 5ms.
- Multiplas AZ na mesma VPC.

![Aurora Multi-AZ](/docs/assets/AuroraMulti-AZ.png)

### RDS - Aurora - Endpoints de Conexão
     - Cluster Endpoint
        - Permite leitura\gravação diretamente na instancia Master.
    - Reader Endpoint
        - Permite leitura usando load balancer das replicas de leitura.
    - Custom Endpoint
        - Permite leitura\gravao criando um ponto de entrada personalizado que direcione consultas específicas para locais específicos no cluster

    - Ponto Geral
      - Internamente utiliza rota 53 DNS.

### RDS - Aurora - Replicacao
- Compartilhamento do mesmo volume logico entre todas as instancias.
- Não necessita de replicação (Master -> replicas).

### RDS - Aurora - Failover
- Automatico ou Manual failover 
   - Demora 30 segundos para promover como master outra instancia.

### RDS - Aurora - Throughput
      - Master pode ser reiniciado em 60 segundos ou menos.
      - Cluster parado a mais de 7 dias será automaticamente reiniciado.
      - Backup diarios por default são retidos pelo máximo de 35 dias.
      - Snapshop 
        - podem ser criados sob demanda manualmente.
        - São armazenados indefinitivamente e deletadas manualmente.
        - Restore são executadas em um novo banco.

### RDS - Aurora - Consistencia de Dados
- usa 'Quorum'
   - Mínimo de réplicas de armazenamento necessárias para confirmar uma operação de gravação como valida, mesmo em falhas de instâncias.

- usa 'Gossip Protocol' 
   - Coordena e mantem a consistência dos dados distribuídos em um cluster
     - As instâncias compartilhem informações sobre disponibilidade e topologia da rede, garantindo alta disponibilidade e durabilidade dos dados.
   - protocolo 'Peer gossip' usado para copiar dados entre os 6 nós de armazenamento. 

- Unico que suporta 3 ou mais zonas de disponibilidade (AZ)

![Aurora Multi-AZ](/docs/assets/AuroraDataConsistency.png)

### RDS - Aurora - Multi-Master

      - Maximo 4 instancia como Master.
      - Read replicas não podem ser adicionados.
      - Não utiliza o servico 'Load Balance'.
        - Esta logica precisa ser aplicada pelo cliente.
      
![RDS - Aurora - Multi-Master](/docs/assets/RDS_AuroraMultiMaster.png)


### RDS - Aurora - Serveless
      - Capacidade minima e maxima.
      - Instancia automaticamente iniciada e parada conforme demanda.
      - Desabilita todas as instancias se não tiver demanda (Se habilitado).
        - pagando pela capacidade de armazenamento.
