Ambiente DOCKER para utilização do Moodle
=========================================

Estrutura:
----------------

1. **html**
    * Arquivos da aplicação. No caso o Moodle;
    * Vcê pode fazer o download do pacote fechado do Moodle ou via Git;
    * **Download via GIT**:
        1. ``git clone https://github.com/moodle/moodle.git``
        2. ``git  branch -t MOODLE_32_STABLE  origin/MOODLE_32_STABLE``  Configura para a versão 3.2.x do Moodle;
2. **moodledatas** 
    * Espaço reservado para criar sua pasta do Moodledata.;
    * Padrão sugerido: moodledata_[nome_da_aplicacao];
    
3. **php7.0-ubuntu**
    * Dockfile contendo as configurações do serviço.    

4. **postgres**
    * **./postgres/postgres-data**: a pasta deve ser criada por você. Crie /postgres/postgres-data. É o volume que guardará    os dados na sua máquina local
    * /**scripts**: 
        * init.sql: por padrão cria uma base de dados chamada Moodle; **[Você pode alterar]**
        
Você deve/pode Alterar:
------------------

1. ./postgres/script/init.sql: altere o nome do banco de dados para criar uma nova base;
2. ./moodledatas/: crie aqui uma nova pasta moodledata para nova instância Moodle;


Iniciar container:
--------------------
```git
git clone https://github.com/srssaulo/moodle-dev-env.git
```
 - Vá até a raíz do projeto e execute o docker-compose.yml
 
```docker
     docker-compose  -f docker-compose-php5.6.yml up -d
```

   ou
            
```docker
       docker-compose -f docker-compose-php7.0.yml up -d
```

   ou
    
```docker
       docker-compose -f docker-compose-php7.2.yml up -d
```
 - Acesse localhost:8080
 
Destruir container:
--------------------
  - Vá até a raíz do projeto e execute o docker-compose.yml
  
 ```docker
      docker-compose -f docker-compose-php5.6 down
 ```
 
   ou
             
 ```docker
        docker-compose -f docker-compose-php7.0 down
 ```

Volumes:
--------------------
 - Caso queira enviar um arquivo .sql para restore na base de dados baste ir para:
   ```shell
   cd ./postgres/tmp
   ``` 
 - Caso queira enviar acessar os logs do servidor apache:
      ```shell
      cd ./php5.6-ubuntu/logs #escolha a versão
      ``` 