# Exemplo de projeto com MultiTenancy

## Descrição
- A ideia geral de conexão com banco de dados é que o Spring sempre precisa de um Bean do tipo DataSource para se conectar ao banco de dados.
- Esse DataSource tem todos os dados de conexão com a base, host, url senha..
- Na forma convencional, nós apenas colocamos os dados da base no application.yml e o Spring ja instância um DataSource com esses dados.
- Mas para MultiTenancy não podemos fazer isso, pois queremos escolher a base a se conectar dinamicamente, por cada requisição.
- Dessa forma, sempre que uma requisição é feita nós precisamos receber algum dado que identifique unicamente o Tenant, ou seja, a base a se conectar.
- Nesse projeto esse dado é o header X-TenantID, com base nele nós escolhemos qual arquivo da pasta allTenants será lido para preencher o DataSource.
- Esse header é capturado no TenantFilter, e é setado o nome do tenant da Thread atual, para que no método determineCurrentLookupKey() ele saiba qual tenant chamar.
- A cada requisição, a classe TenantContext armazena o tenant que será usado na Thread atual.
- O preenchimento dos DataSources é feito apenas uma vez, no boot da aplicação, na classe MultitenantConfiguration. 
