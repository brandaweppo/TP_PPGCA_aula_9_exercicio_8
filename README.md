# Técnicas de Programação/PPGCA
## Exercício 8 - Aula 9

###### 1. Fazer um diretório local chamado *"solicitacoes-v2"*

###### 2. Acessar diretório correspondente
```
cd solicitacoes-v2/
```

###### 3. Criar diretórios da estrutura conforme os comandos abaixo:
```
mkdir app
```
e
```
mkdir nginx
```
e
```
mkdir scripts
```
e
```
mkdir web
```

###### 4. Fazer download do arquivo *"docker-compose"* e inserí-lo dentro da raiz do diretório do projeto, chamado *"solicitacoes-v2"*:


###### 5. Listar diretórios existentes dentro de *solicitacoes-v2* e verificar se há "app", "nginx", "scripts", "web" e "docker-compose" com o comando abaixo:
```
ls
```

###### 5. Fazer download dos arquivos *"app.sh"* e *"envia.py"* e inserí-los dentro do diretório chamado *"app"*.

###### 6. Fazer download do arquivo *"default.conf"* e inserí-lo dentro do diretório chamado *"nginx"*.

###### 7. Fazer download dos arquivos *"check.sql"* e *"init.sql"* e inserí-los dentro do diretório chamado *"scripts"*.

###### 8. Fazer download do arquivo *"index.html"* e inserí-lo dentro do diretório chamado *"web"*.

###### 9. Acessar o diretório *"nginx"* e criar outro diretório chamado *"dados"*, conforme os comandos abaixo:

```
cd nginx/

```
e

```
mkdir dados

```

###### 10. Retornar ao diretório anterior através do comando abaixo:

```
cd ..

```

###### 11. Verificar se não há nada rodando do arquivo *"docker-compose"* com o comando abaixo:
```
docker-compose ps 
```
ou
```
docker-compose ps -a
```

###### 12. Se estiver algum componente ativo executar o comando abaixo para desativá-los:
```
docker-compose down
```

###### 13. Ativar o arquivo *"docker-compose"*, deixando-o em background utilizando o omando abaixo:
```
docker-compose up -d
```

###### 14. Executar o comando abaixo para verificar se os serviços estão ativos, identificados pelo status "up" conforme mostra a imagem logo a seguir:
```
docker-compose ps
```
![Captura de Tela (66)](https://user-images.githubusercontent.com/65691783/83930228-e34cf700-a76c-11ea-8249-8597a3192734.png)

###### 15. Acessar o navegador web e verificar se a aplicação está no *"localhost"*, conforme mostra a imagem abaixo:

![Captura de Tela (62)](https://user-images.githubusercontent.com/65691783/83930336-6f5f1e80-a76d-11ea-9a02-34be99d1ecc7.png)

###### 16. Acessar o navegador web e fazer uma teste de formulário, preenchendo os campos e acionando o botão *"Enviar"*, verificar se os títulos dos campos e as respostas preenchidas aparecem na própria página do *"localhost"*, conforme mostra a imagem abaixo:

![Captura de Tela (65)](https://user-images.githubusercontent.com/65691783/83930584-b7327580-a76e-11ea-8946-2eb63375d13a.png)

###### 17. Executar o comando indicado abaixo para visualizar o banco de dados:
```
docker-compose exec db psql -U postgres -d solicitacoes -c 'select * from pedidos'
```

###### 18. Verificar todos os logs do banco de dados estão sendo registrados utilizando o comando abaixo:
```
docker-compose logs -f -t
```


###### 19. Verificar se as informações inserirdas na página web estão registradas na base de dados utilizando o comando abaixo. Logo abaixo segue uma imagem ilustrativa.
```
docker-compose exec db psql -U postgres -d solicitacoes -c 'select * from pedidos'
```
![Captura de Tela (67)](https://user-images.githubusercontent.com/65691783/83930718-55bed680-a76f-11ea-9135-f70525a39018.png)

###### 20. Faça um backup das informações inseridas na página web que estão registradas na base de dados salvando-as em um arquivo de formato sql dentro do diretório *"dados"*, utilizando o comando abaixo:
```
docker-compose exec -u postgres db pg_dump -Fc solicitacoes > dados/dump_date.sql
```
