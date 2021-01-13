<h1 align="center">Python3 com SQLite3</h1>
<p align="center">Uma breve explicação de como utilizar SQLite3 com python na prática.</p>
<p align="center">Para iniciantes.</p>
<p align="center"> 
   <img src="https://img.shields.io/badge/language-python-blue.svg">
</p>

***

```
O arquvo "sqlitet.py" que contêm toda explicação, este após lido e entendido
pode ser executado, tudo aquilo aprendido poderá então ser visto na prática.
```

## SQLite3 && Python3

```python

# Criando  e Gerenciando  um  banco  de dados  com python3 e SQLite3.

# SQL é uma linguagem muito  boa para  criação de  tabelas, as  quais
# podemos inserir, atualizar, apagar ou apenas vizualizar informações
# de uma forma  simples. Python com  a biblioteca SQLite3 permite uma
# ótima  integração  de uma base  de dados  para  programas sem muita
# complexidade, principalmente para  a automação  deste gerenciamento
# por parte do programa.
# O SQLite  é caracteristico pela ausência de um servidor  que  sirva
# para prover o banco  de dados, tudo  é feito localmente, dentro  do
# própio dispositivo, para isso, é criado uma rquivo  que armazena os
# dados, é bem comum em aplicações para dispositivos móveis.

# Podemos iniciar o programa importando a biblioteca SQLite3.
import sqlite3

# Precisamos  fazer  uma conexão  com o banco de dados, mesmo que ele
# não exista, vamos criar um. Para facilitar,  a conexão será chamada
# de "conn". O arquivo contendo  o conteúdo se chamará "database.db"
# e será armazenado no local onde este programa for executado.
conn = sqlite3.connect('database.db')

# É necessário a criação de um "cursor" para interagir com o banco de
# dados, como para adição de registros.
cursor = conn.cursor()

# Então podemos criar a primeira tabela que receberá o nome de "users".
# Assim como como em qualquer outro tipo de mecanismo SQL, os comandos
# são parecidos com o ingles  e em letra  maiuscula, e  o cursor  será
# utilizado para executar a tarefa.
# As colunas que a tabela recebe serão definidas nessa mesma ação.
cursor.execute("""
    CREATE TABLE IF NOT EXISTS users (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    username TEXT NOT NULL,
    password TEXT NOT NULL
);
""")
# Foram criados alguns campos como username e a pessword, "TEXT NOT NULL"
# informa que o texto não pode estar vazio, ja o campo "id" será inserido
# automaticamente pelo cursor.

# Lista de atributos que podem ser utilizados.
#           CHAR | Caracteres string de tamanho fixo.
#        VARCHAR | Caracteres string de tamanho variável.
#            INT | Números inteiros.
#          FLOAT | Números fracionários (ponto flutuante).
#           DATE | Data no formato mysql (ano-mês-dia).
#       NOT NULL | Indica que o atributo não pode ser nulo (deve possuir um valor).
#  AUTOINCREMENT | Indica que o valor valor do campo será incrementado automaticamente.
#    PRIMARY KEY | Indica que o atributo é uma chave primária (identificador único).
#           TEXT | Armazena texto (não pode ser do tipo “not null”).

# Outros exemplos de como se criar a tabela.
# CREATE TABLE users (criar tabela)
# ALTER TABLE users(alterar tabela)
# DROP TABLE users(apagar tabela)

# Agora ja podemos começar inserindo algumas informações na tabela.
# Apenas  precisamos  inserir os valores que desejamos utilizando o
# cursor para isso.
username1 = "dev"
password1 = "dev123"
cursor.execute(f"""
    INSERT INTO users (username,password) 
    VALUES ('{username1}','{password1}')
""")
# inserimos nossas variáveis na tabela.
# falta apenas salvar as informações nema.
conn.commit()

# Vamos inserir mais informações.
username2 = "python"
password2 = "sqlite3"
cursor.execute(f"""
    INSERT INTO users (username,password) 
    VALUES ('{username2}','{password2}')
""")
# inserimos nossas variáveis na tabela.
# falta apenas salvar as informações nema.
conn.commit()

# Após termos inserido  as informações, podemos  selecionar
# e ver no banco, para fazer o dump das informações, de uma
# forma mais crua, vamos usar apenas o "print".
cursor.execute("""
    SELECT * FROM users;
""")
# Assim selecionamos todos os dados presentes na tabela com
# o atributo "*".
for item in cursor.fetchall():
    print(item)

# Podemos selecionar informações mais especificas.
id = "1"
cursor.execute(f"""
    SELECT username,password FROM users
    WHERE id == '{id}'
    
""")
for item in cursor.fetchall():
    print(item)

# Podemos de uma forma parecida, deletar informações.
usertodelet = "dev"
cursor.execute(f"""
    DELETE FROM users
    WHERE username = '{usertodelet}'
""")
# E salvamos a alteração dando "commmit".
conn.commit()

# Vejamos novamente a tabela.
cursor.execute("""
    SELECT * FROM users;
""")
for item in cursor.fetchall():
    print(item)

# O SQLite3 é uma biblioteca muito completa e possui mais
# varias informações importantes, mais isso ja é  mais do
# que o necessário para  começar  a  fazer implementações  
# bem úteis em projetos mais simples.

```


