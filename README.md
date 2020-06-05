# Técnicas de Programação/PPGCA
## Exercício 8 - Aula 9

*##ROTEIRO RESUMIDO##*

# Técnicas de Programação/PPGCA
## Exercício 8 - Aula 9

###### 1. Fazer download da pasta compactada *"solicitacoes-v2"*

###### 2. Acessar diretório correspondente
```
cd solicitacoes-v2/
```

###### 3. Listar diretórios existentes dentro de *solicitacoes-v2* e verificar se há "app", "dados", "nginx", "scripts", "web" e "docker-compose"
```
ls
```
###### 4. Verificar se não há nada rodando do arquivo *docker-compose*
```
docker-compose ps 
```
ou
```
docker-compose ps -a
```
###### 5. Se estiver algum componente ativo executar comando para desativá-los
```
docker-compose down
```
###### 6. Ativar o arquivo *docker-compose*
```
docker-compose up -d
```
###### 7. Executar comando para verificar se os serviços estão ativos, identificados pelo status "up"
```
docker-compose ps
```
###### 8. Acessar o navegador web e verificar se a aplicação está no *localhost*

###### 9. Acessar o navegador web e fazer uma teste de formulário, preenchendo os campos e acionando o botão *"Enviar"*, verificar se os títulos dos campos e as respostas preenchidas aparecem na própria página do *"localhost"*.

###### 10. Executar comando para visualizar o banco de dados
```
docker-compose exec db psql -U postgres -d solicitacoes -c 'select * from pedidos'
```
###### 11. Verificar quais componentes estão ativos
```
docker-compose ps
```
###### 12. Desativar os componentes estão ativos
```
docker-compose down
```
###### 13. Verificar quais componentes estão ativos
```
docker-compose ps
```
###### 14. Ativar o arquivo *"docker-compose"*
```
docker-compose up -d
```
###### 15. Verificar se os componentes estão ativos, identificados pelo status *"up"*
```
docker-compose ps
```
###### 16. Verificar todos os logs do banco de dados
```
docker-compose logs -f -t
```
###### 17. Verificar se as informações inserirdas na página web estão registradas na base de dados
```
docker-compose exec db psql -U postgres -d solicitacoes -c 'select * from pedidos'
```
###### 18. Fazer um backup das informações inserirdas na página web estão registradas na base de dados em formato sql dentro do diretório *"dados"*
```
docker-compose exec -u postgres db pg_dump -Fc solicitacoes > dados/dump_'date +%d-%m-%Y"_"%H_%M_%S'.sql
```
