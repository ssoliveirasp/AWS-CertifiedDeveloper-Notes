- [DynamoDB (NoSql)](#dynamodb-nosql)
  - [NoSQL (Not Only SQL)](#nosql-not-only-sql)
  - [DynamoDB](#dynamodb)
  - [Modelagem de Dados](#dynamodb---modelagem-de-dados)
  - [Throttling](#dynamodb---throttling)
  - [Escrevendo dados](#dynamodb---escrevendo-dados)
  - [Apagando dados](#dynamodb---apagando-dados)
  - [Batching writes](#dynamodb---batching-writes)
  - [Lendo dados](#dynamodb---lendo-dados)
  - [Query](#dynamodb---query)
  - [Scan](#dynamodb---scan)
  - [Local Secondary Index (LSI)](#dynamodb---local-secondary-index-lsi)
  - [Global Secondary Index (GSI)](#dynamodb---global-secondary-index-gsi)
  - [Concurrency](#dynamodb---concurrency)
  - [DAX (DynamoDB Accelerator)](#dynamodb---dax-dynamodb-accelerator)
  - [Streams](#dynamodb---streams)
  - [Segurança](#dynamodb---segurança)
  - [Backup e Restore](#dynamodb---backup-e-restore)
  - [Migracao](#dynamodb---migracao)
    
# DynamoDB (NoSql)

## NoSQL (Not Only SQL)

### Caracteristicas
- SchemaLess 
- Banco de dados não relacional.
- Todos os dados usados no Query ficam em uma linha

### Limitaçoes
- Não suportam Join.
- Não fazem Aggregation, como por exemplo **SUM**

### Escalonamento
- Escalonamento horizontal.
- São distribuídos.

## DynamoDB

### Caracteristicas
- Baixo custo.
- DynamoDB é feito de tabelas.
- Primary Key é obrigatório e deve ser definido no momento em que criamos a tabela.

### Escalonamento
- Escalonamento automático.
- Escalonável para quantidade muito grande de dados pois é um banco de dados distribuído.

### Limitações
- Tamanho máximo do item é de 400KB.

### Performance
- Gerenciado pela AWS com réplicas em 3 AZ's garantindo alta disponibilidade.
- Milhões de requisições por segundo, trilhões de linhas, centenas de terabytes de armazenamento.
- Rápido e consistente em performance (baixa latência).
- Global Tables:
  - Multi Region, replicável e alta performance.

### Seguranca
- Integrado com IAM para segurança, autorização e administração.
  
#### Encryption at rest
- Owned by Amazon DybamoDB
- AWS managed key
- Stored in your account and owned and managed by you.

### Streams
- Event Driven Programming com DynamoDB Streams.

### Table Classes
- DynamoDB Standard
  - Usado com mais frequencia.
    
- DynamoDB Standard-IA
  - Acesso infrequente e preço mais barato.

### Desenvolvimento
- É possível instalar DynamoDB em uma máquina local para desenvolvimento.

## DynamoDB - Modelagem de Dados

### Caracteristicas
- Uma tabela pode ter infinitos itens (equivalente a rows nos bancos relacionais).
- Cada item tem Attributes, podendo ser adicionados a qualquer momento ou ser nulo.

### Tipos de dados suportados:
  - Scalar types: String, Number, Binary, Boolean, null.
  - Document type: List, Map.
  - Set types: String set, Number set, Binary set.

### DynamoDB - Partition Key

- Somente Partition Key (hash):
  - Partition Key deve ser única para cada item.
  - Partition Key deve ser diversificada para os dados serem distribuídos.

- Partition Key + Sort Key:
  - A combinação deve ser única.
  - Dados são agrupados pela Partition Key.
  - Sort Key == Range Key.

### DynamoDB - Provisioned Throughput

- Tabela deve ter leitura e escrita provisionadas.
- Read Capacity Units (RCU).
- White Capacity Units (WCU).
- Opção de configurar auto-scaling para throughput.
- Throughput pode temporariamente exceder o limite estabelecido usando 'burst credit'.
- Se o burst credit acabar, você receberá um **ProvisionedThroughputException**.
- É recomendado fazer um Exponential Back-Off Retry.

### DynamoDB - Write Capacity Units (WCU)

- 1 Write Capacity Unit (WCU) representa uma escrita por segundo para 1 item até 1KB em tamanho.
- Se o item for maior que 1KB, mais WCU será consumido.
- Exemplos de cálculos:
  - Escrever 10 itens de 2KB por segundo = 20 WCU (10 \* 2 = 20).
  - Escrever 6 itens de 4.5KB por segundo = 30 WCU (6 \* 5 = 30).
  - Escrever 120 itens de 2KB por minuto = 4 WCU ((2 \* 120) / 60 = 4).

### DynamoDB - Read Capacity Units (RCU)

- 1 Read Capacity Unit (RCU) representa 1 Strongly Consistent Read por segundo ou 2 Eventually Consistent Reads por segundo para um item até 4KB.
- Se o item for maior que 4KB, mais RCU serão consumidos.
- Exemplos de Cálculos:
  - 10 Strongly Consistent Read por segundo de 4KB = 10 RCU ((10 \* 4) / 4 = 10).
  - 16 Eventually Consistent Read por segundo de 12KB = 24 RCU ((16/2) \* (12/4) = 24).
  - 10 Strongly Consistent Read por segundo de 6KB = 20 RCU ((10 \* 8)/4 = 20).

### DynamoDB - Strongly Consistent Read VS Eventually Consistent Read

- Eventually Consistent Read: Se lermos um item logo após uma escrita, podemos receber seu valor anterior devido a replicação do dado.
- Strongly Consistence Read: Se lermos um item depois de uma escrita, leremos o valor atualizado.
- Por padrão o DynamoDB usa Eventually Consistence Reads, porém os métodos GetItem, Query e Scan possuem um parâmetro chamado ConsistentRead que pode ser modificado para True.

### DynamoDB - Partitions Internal

- _Dados são divididos em partitions_.
  - A regra para divisão:
    - Partition DataSize
       -  Tamanho total particicao > 10gb
    - RCU and WCU Partition
      - Partition RCU > 3000.
      - Partition WCU > 1000.
- Partition Key passa por um algoritmo para saber para qual Partition deve ir.
- Computar o número de partições:
  - Capacidade: (Total RCU / 3000) + (Total de WCU / 1000).
  - Tamanho: Tamanho total / 10GB.
  - Número de partições: CEILING(MAX(Capacity, Size)).
- WCU e RCU são distribuídos igualmente entre as partições.
  - _Balanceamento_
    - Capacidade (400 RCUs | 400 WCUs) em um exemplo de 4 partiçoes cada partição teria um limite flexivel (100 RCUS | 400 WCUS).
  - _Hot Partition (Partição Ativa)_
    - Ocorre quando uma partição excede o seu limite flexivel (RCU | WCU).
    - Leitura e gravações param de funcionar nesta partição.
  - _ProvisionedThroughputExceededException_
    - Erro de limitações ou gargalos durante uma Hot Partition.
    - AWS SDK repetirá automaticamente varias vezes com espera exponencial integrada [exponential backoff]  (1x, 2x, 4x, 8x, ...x).
  - _Manage imbalances DynamoDB_
    - Burst capacity
      - Aws oferece a partição com 'Hot Partition' capacidade extra grátis e um 'periodo curto de tempo'.
    - Adaptive Capacity
      - Permite a partição com 'Hot Partition' consumir mais capacidade (thtoughput) indefitivamente. 
 
### DynamoDB - Modelagem de Dados - Referencias
[Exemplo Modelagem AWS](https://docs.aws.amazon.com/pt_br/amazondynamodb/latest/developerguide/bp-modeling-nosql-B.html)


## DynamoDB - Throttling

- Se excedemos RCU ou WCU recebemos um ProvisionedThroughputExceededException.
  - Possíveis razões:
    - Hot Key: Um Partition Key está sendo acessado muitas vezes.
    - Hot Partition.
    - Itens muito grandes: Pois RCU e WCU dependem do tamanho do item.
  - Soluções possíveis:
    - Exponential Back-Off quando uma exceção é encontrada (recurso incluso no SDK).
    - Distribuir Partition Keys o máximo possível.
    - Se for problema com RCU, podemos usar o DynamoDB Accelerator (DAX).

## DynamoDB - Escrevendo dados

- PutItem:
  - Escreve dados no DynamoDB, criando ou substituindo.
  - Consome WCU.
    
- UpdateItem:
  - Atualiza dados no DynamoDB, atualizando parte dos atributos.
  - Possibilidade de usar Atomic Counters e incrementá-los.
    
- [Conditional Writes](https://docs.aws.amazon.com/pt_br/amazondynamodb/latest/developerguide/WorkingWithItems.html#WorkingWithItems.ConditionalUpdate):
  - A expressão inteira deve ser avaliada como verdadeira para realizar atualização. Caso contrário, haverá falha na operação.
  - Utilizando AWS CLI update-item utiliza o parametro 'update-expression'.
  - Pode ser utilizado para contribuir com acesso simultâneo aos itens.
  - Não impacta a performance.

## DynamoDB - Apagando dados

- DeleteItem:
  - Deleta um item.
  - É possível fazer um DeleteItem usando condicionais.
- DeleteTable:
  - Apaga toda a tabela e seu conteúdo.
  - Mais rápido que DeleteItem para apagar todos os itens.

## DynamoDB - Batching writes

- BatchWhiteItem:
  - Máximo de 25 PutItem ou DeleteItem por chamada.
  - Máximo de 16MB de dados escritos.
  - Máximo de 400KB de dados por item.
- Batching permite reduzir a latência, reduzindo o número de API Calls ao DynamoDB.
- Operações são feitas em paralelo para melhor eficiência.
- É possível que alguns itens do Batch falhem, nesse caso será preciso tentar novamente utilizando o algoritmo Exponential Back-off.

## DynamoDB - Lendo dados

- GetItem:
  - Leitura baseado no Primary Key.
  - Primary Key = Hash ou hash-range.
  - Eventually Consistent Read é o padrão.
  - Opção de usar o Strongly Consistent Read (consome mais RCU e pode demorar mais).
  - ProjectionExpression pode ser especificado para incluir somente certos atributos.
- BatchGetItem:
  - Até 100 itens.
  - Até 16MB.
  - itens são lidos em paralelo para minimizar a latência.

## DynamoDB - Query

- Query retorna itens com base em:
  - Valor do Partition Key usando o operador `=`.
  - Valor do SortKey usando um dos operadores a seguir: `=`, `<`,`<=`,`>`,`>=`,`Between`,`Begin`.
  - FilterExpression pra filtros no lado do cliente.
- Retorna:
  - Até 1MB.
  - Ou número de itens especificado em `Limit`.
- Possível fazer paginação com o resultado.
- Pode-se usar query com Table, Local Secondary Index ou Global Secondary Index.

## DynamoDB - Scan

- Utilizar o Scan com filtros é ineficiente.
- Retorno de até 1MB. Usar paginação.
- Consome muito RCU.
- Pode-se diminuir o impacto usando Limit ou reduzir o tamanho do resultado.
- Para melhor performance, use Parallel Scans:
  - Múltiplas instâncias varrem múltiplas partições ao mesmo tempo.
  - Aumenta o throughput e o RCU consumido.
  - Limitar o impacto do Parallel Scans do mesmo jeito que é feito com Scans.
- Pode-se usar ProjectionExpression + FilterExpression.

## DynamoDB - Local Secondary Index (LSI)

- Deve ser definido no momento da criação da tabela.
- Key alternativo para tabela, local ao hash key.
- Sort Key consiste de exatamente um atributo.
- O atributo que você escolher deve ser String, Number ou Binary.
- Máximo de 5 LSI por tabela.

## DynamoDB - Global Secondary Index (GSI)

- Para aumentar a velocidade dos Queries para atributos que não são keys, use GSI.
- GSI = Partition Key + Sort Key (opcional).
- Index é uma "nova" tabela e podemos projetar atributos a ela:
  - A Partition Key e Sort Key da tabela original são sempre projetada (KEYS_ONLY).
  - Pode-se especificar atributos para projetar (INCLUDE).
  - Pode-se usar todos os atributos da tabela principal (ALL).
- Deve-se definir RCU/WCU para o índice.
- Possibilidade de adicionar/modificar GSI.
- Maximo de 20 GSI por tabela.
  
## DynamoDB - Concurrency

- DynamoDB tem uma função chamada **Conditional Update/Delete**.
- Isso garante que o item não foi modificado antes de ser alterado.
- Isso faz o DynamoDB Optimistic Locking / Concurrency Database.

## DynamoDB - DAX (DynamoDB Accelerator)

- Não é necessário nenhuma alteração no DynamoDB.
- Escrita vai para o DAX e ele escreve no DynamoDB.
- Latência de microssegundos para leituras e queries no cache.
- Resolver o problema de Hot Key (muitas leituras na mesma partição).
- 5 minutos de TTL (time to live) padrão do cache.
- Até 10 nodes no cluster.
- Multi AZ, sendo no mínimo 3 nodes recomendados para produção.
- Segurança: Criptografia em repouso com KMS, VPC, IAM, CloudTrail, etc.

## DynamoDB - Streams

- Mudanças no DynamoDB (Create, Update, Delete) podem iniciar um DynamoDB Stream.

### Integracoes 
    
  #### Lambda
  - Até 2 lambdas inscritos em um unico stream.
  - Esse Stream pode ser lido pela AWS Lambda para:
  - Reagir a mudanças em tempo real, como por exemplo enviar um e-mail de boas vindas.
       - Análise.
       - Criar derivative tables / views.
       - Insert no ElasticSearch.
  - Possível implementar Cross Region Replication usando Streams.
  - Stream tem 24 horas de retenção.

  #### Kinesis Data Streams
  - Perda de Ordenação.
    - possivel reordenar utilizando o atributo "ApproximateCreationDateTime"

   https://www.youtube.com/watch?v=kOWotp042PI

## DynamoDB - Segurança

### Caracteristicas:
  - VPC Endpoint disponível para acessar o DynamoDB sem internet.
  - Acesso totalmente controlado pelo IAM.
  - Criptografia em repouso usando KMS.
  - Criptografia em transito usando SSL/TLS.

###  Table Access Provisioning (Policies)
  A AWS aborda alguns casos de uso comuns fornecendo políticas autônomas do IAM que são criadas e administradas pela AWS. Essas políticas gerenciadas pela AWS concedem as permissões necessárias

#### Aws Politicas (Actions - "Pré-Definidas")
   - dynamodb:GetItem
   - dynamodb:BatchGetItem
   - dynamodb:Query
   - dynamodb.Scan
   - dynamodb:ReadOnlyAccess
   - dynamodb:PutItem
   - dynamodb:UpdateItem
   - dynamodb:BatchWriteItem
   - dynamodb:DeleteItem  
   - dynamodb:FullAccess

#### Criar Politicas Personalizadas
- Effect
  - Allow
  - Deny

- Resource        
  - "arn:table/{nome tabela}"
  - "arn:table/{nome tabela}/index/*"

- Condition
  - Chave de Condição
    
      - dynamodb:LeadingKeys (Chaves Principais)
         - Utilizar modificador "ForAllValues".
         
      - dynamodb:Select      (Query ou Scan)
        - ALL_ATTRIBUTES
        - ALL_PROJECTED_ATTRIBUTES
        - SPECIFIC_ATTRIBUTES
           - dynamodb.Attributes   
        - COUNT

## DynamoDB - Backup e Restore
  - Restauração Point in time, igual ao RDS.
  - Sem impacto na performance.

## DynamoDB - Migracao
- Amazon DMS pode ser usado para migrar para DynamoDB dados do: Mongo, Oracle, MySQL, S3, etc.
