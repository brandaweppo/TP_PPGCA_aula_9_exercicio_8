# Técnicas de Programação/PPGCA
## Exercício 8 - Aula 9

###### 1. Copiar diretório da *Aula 8* e renomear como *solicitacoes-v2*

###### 2. Acessar diretório criado
```
cd solicitacoes-v2/
```

###### 3. Listar diretórios existentes dentro de *solicitacoes-v2* e verificar se há os diretórios *scripts*, *web* e o arquivo *docker-compose*
```
ls
```

###### 4. Criar um diretório *app*
```
mkdir app
```

###### 5. Acessar o diretório *app*
```
cd app/
```

###### 6. Criar um arquivo para script chamado *app.sh*
```
fc > app.sh
```

###### 7. Listar arquivos para verificar se o arquivo anterior foi criado
```
ls
```

###### 8. Editar arquivo de configuração de script *app.sh*
```
#!/bin/sh

pip install bottle==0.12.13
python -u envia.py
```

###### 9. Criar arquivo *envia.py*
```
fc > envia.py
```

###### 10. Listar arquivos para verificar se o arquivo anterior foi criado
```
ls    
```

###### 11. Acessar diretório anterior
```
cd ..
```

###### 12. Editar arquivo *envia.py*
```
from bottle import route, run, request

@route('/', method='POST')
def send():
	nome = request.forms.get('nome')
	assunto = request.forms.get('assunto')
	mensagem = request.forms.get('mensagem')

	return 'Mensagem enviada: Nome: {} Assunto: {} Mensagem: {}'.format(
		nome, assunto, mensagem
	)
if __name__== '__main__':
	run(host='0.0.0.0', port=8080, debug=true)
```

###### 13. Editar a linha 10 do arquivo *index.html* conforme informações abaixo
```
        <form action="http://localhost:8080" method="POST">
```
###### 14. Editar arquivo *docker-compose* a partir da linha 19
```
  app:
    image: python:3.7.2
    volumes:
      - ./app:/app
    working_dir: /app
    command: bash ./app
    ports:
      - 8080:8080
```
###### 15. Verificar se não há nada no arquivo *docker-compose*
```
docker-compose ps 
```
ou
```
docker-compose ps -a
```
###### 16. Se estiver algum componente ativo executar comando para desativá-los
```
docker-compose down
```
###### 17. Ativar o arquivo *docker-compose*
```
docker-compose up -d
```
###### 18. Executar comando para verificar se os serviços estão ativos, identificados pelo status "up"
```
docker-compose ps
```
###### 19. Acessar o navegador web e verificar se a aplicação está no *localhost*

###### 20. Acessar o navegador web e fazer uma teste de formulário, preenchendo os campos e acionando o botão *"Enviar"*, verificar se os títulos dos campos e as respostas preenchidas aparecem na própria página do *"localhost"*.

###### 21. Criar um diretório chamado *"nginx"*
```
mkdir ngnix
```
###### 22. Acessar diretório *"nginx"*
```
cd nginx/
```
###### 23. Criar um arquivo de configuração do *"nginx"* dentro do diretório *"nginx"*
```
fc > default.config
```
###### 24. Editar arquivo *default.config*, mapeá-lo para que ele seja colocado no lugar correto no *"nginx"* para executar o Proxy-reverso
```
server {
	listen 80;
	server_name localhost; 

	location / {
		root:/usr/share/nginx/html;
		index index.html index.htm;
	}

	error_page 500 502 504 /50x.html
	location = /50x.html {
		root /usr/share/nginx/html;
	}

	location /api {
		proxy_pass http://app:8080;
		proxy_http_version 1.1;
	}
}
```
###### 25. Editar arquivo *docker-compose* em relação aos volumes *web*
```
volumes:
      # Site
      - ./web:/usr/share/nginx/html
      # Proxy Reverso
      - ./nginx/default.config:/etc/nginx/conf.d/default.conf
```
###### 26. Retirar o mapeamento de portas no arquivo *docker-compose* em relação à *app*
```
    #ports:
    #  - 8080:8080
```
###### 27. Editar arquivo *"index.html"* para redirecional a porta para */api*
```
<form action="http://localhost/api" method="POST">
```
###### 28. Verificar componentes que estão ativos 
```
docker-compose ps
```
###### 29. Baixar todos os componentes ativos
```
docker-compose down
```
###### 30. Verificar componentes que estão ativos 
```
docker-compose ps
```
ou
```
docker-compose stop
```
ou
```
docker-compose down
```
ou
```
docker-compose ps -a
```
###### 31. Ativar todos os serviços novamente
```
docker-compose up -d
```
###### 32. Acessar o navegador web e fazer uma teste de formulário, preenchendo os campos e acionando o botão *"Enviar"*, verificar se os títulos dos campos e as respostas preenchidas aparecem na própria página do *"localhost"*.

###### 33. Executar comendo para visualizar o banco de dados
```
docker-compose exec db psql -U postgres -d solicitacoes -c 'select * from pedidos'
```
###### 34. Editar arquivo *docker-compose* para criação de duas redes a partir da 4ª linha
```
networks:
  db:
  web:
```
###### 35. Editar arquivo *docker-compose* para para que o banco de dados tenha a rede *"db"*
```
    networks:
        - db
```
###### 36. Editar arquivo *docker-compose* para para que web tenha a rede *"web"*
```
    networks:
      - web
```
###### 37. Editar arquivo *docker-compose* para o serviço *web* dependa do *app*
```
    depends_on:
      - app  
```
###### 38. Editar arquivo *docker-compose* para o informar o *app* de suas respectivas redes, assim como sua dependência do banco de dados
```
    networks:
      - db
      - web
    depends_on:
      - db
```
###### 39. Editar arquivo *"app.sh"* para fazer a dependência da base
```
pip install bottle==0.12.13 psycopg2==2.7.1
```
###### 40. Editar arquivo *"envia.py"* para que ele importe o *psycopg2*
```
import psycopg2
```
###### 41. Editar arquivo *"envia.py"* para que ele envie as informações para o banco de dados
```
DSN = 'dbname=solicitacoes user=postgres host=db'
SQL = 'INSERT INTO pedidos (nome, assunto, mensagem) VALUES (%s, %s, %s)'

def registro_pedido(nome, assunto, mensagem):
	connecta = psycopg2.connect(DSN)
	cursosql = connecta.cursor()
	cursosql.execute(SQL, (nome, assunto, mensagem))
	cursosql.commit()
	cursosql.close()

	print('Mensagem registrada!')
```
e
	print('Mensagem registrada!')
```
	registro_pedido(nome, assunto, mensagem)
	print('Mensagem registrada!')
```
###### 42. Retornar ao diretório *"solicitacoes-v2"*
```
cd ..
```
###### 43. Verificar quais componentes estão ativos
```
docker-compose ps
```
###### 44. Desativar os componentes estão ativos
```
docker-compose down
```
###### 45. Verificar quais componentes estão ativos
```
docker-compose ps
```
###### 46. Ativar o arquivo *"docker-compose"*
```
docker-compose up -d
```
###### 47. Verificar se os componentes estão ativos, identificados pelo status *"up"*
```
docker-compose ps
```
###### 48. Verificar todos os logs do banco de dados
```
docker-compose logs -f -t
```
###### 49. Verificar se as informações inserirdas na página web estão registradas na base de dados
```
docker-compose exec db psql -U postgres -d solicitacoes -c 'select * from pedidos'
```
###### 50. Criar um diretório chamado *"dados"*
```
mkdir dados
```
###### 51. Fazer um backup das informações inserirdas na página web estão registradas na base de dados em formato sql dentro do diretório *"dados"*
```
docker-compose exec db -u postgres db pg_dump -Fc solicitacoes > dados/dump_'date +%d-%m-%Y"_"%H_%M_%S'.sql
```
