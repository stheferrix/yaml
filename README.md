# YAML

What It Is: YAML is a human friendly data serialization standard for all programming languages.
Ou seja: Um padrão de serialização de dados amigável para qualquer linguagem de programação

É usado para arquivos de configuração assim como o JSON e o XML.
Um exemplo prático são os templates do AWS CloudFormation e Cloudfront que usam este formato ou JSON, dê uma olhada aqui.

- YAML tem a extensão … “.yaml” e é case sensitive.

O primeiro caractere é o hash (#) use ele para comentar o arquivo.

Para comentários basta usar o caractere (#).

Yaml não permite multiplas linhas em comentário.

Pode se ter vários documentos com fluxos únicos, basta usar o (---) para iniciar o documento e (…) para finalizar.

As strings podem ser com ou sem aspas duplas (“ ”) ou únicas (‘ ’), geralmente use elas quando se tem caracteres especiais

Para data é seguido o padrão ISO 8601. (yyyy-mm- ddThh:mm:ss.ffffff)

É importante indentar o código com espaços.

As listas podem conter colchetes ([]), e caso precisar pode usar uma estrutura parecida com dicionário em python ({}) com chaves para o item ‘chave:valor’ os membros da lista são indicados por (-) hífen.

Caso queira que o YAML leia mais de uma linha em uma chave pode ser usado o caractere maior (>), no retorno ele junta tudo e retorna uma linha somente. Quando se usa o pipe (|) ele retorna com varias linhas de acordo com a estrutura que foi criada. 
                 

Para validar se seu YAML segue o padrão pode ser usado este site:http://www.yamllint.com/

Como exemplo prático podemos ver esse docker-compose.yaml

```
version: "3.7"
# Declaração dos serviços.
services:
  # Configuração do container do Postgres.
  pgsql-metabase-docker:
    # Nome da imagem a ser buscada.
    image: postgres
    # Permite escolher reiniciar caso o serviço pare.
    restart: always
    # Especificação do expose das portas.
    ports:
      - 5432:5432
    # Criação das váriaveis de ambiente.
    environment:
      # Senha para o banco.
      POSTGRES_PASSWORD: postgres
      # Usuário
      POSTGRES_USER: metabase
      #Nome do Banco
      POSTGRES_DB: metabase
    # Indicação do diretório para volume.  
    volumes:
      # Use um diretório que já esteja criado.
      - /HOME/docker/volumes/postgres:/var/lib/postgresql/data

 # Configuração do container do Metabase.
  metabase-docker:
    # Nome da imagem a ser buscada.
    image: metabase/metabase
    # Permite escolher reiniciar caso o serviço pare.
    restart: always
    # Especificação do expose das portas.
    ports:
      - 3002:3000
    # Indicação do diretório para volume.  
    volumes:
    # Use um diretório que já esteja criado.
      - /HOME/docker/volumes/metabase-data:/metabase-data
    # Criação das váriaveis de ambiente.
    environment:
      # Nome do tipo de Banco.
      MB_DB_TYPE: postgres   
      # Nome do Banco.
      MB_DB_DBNAME: metabase  
      # Porta de Conexão.
      MB_DB_PORT: 5432  
      #  Nome do Usuário a se conectar no Banco.
      MB_DB_USER: metabase  
      # Nome da senha do Usuário.
      MB_DB_PASS: postgres  
      # Nome do Host de conexão.
      MB_DB_HOST: pgsql-metabase-docker 
    # Especificação de dependência.  
    depends_on:
      - pgsql-metabase-docker
    # Especificação do contianer a ser linkado.  
    links:
      - pgsql-metabase-docker
```
