# vet_sistema

## Rodando Localmente

> **Nota:** Setup feito para Windows.

### Prerequisitos

É necessários ter os seguintes softwares instalados:

- [Git](https://git-scm.com/downloads)
- Python 3.10 ou superior
- [pip](https://pip.pypa.io/en/stable/getting-started/)
- [VSCode](https://code.visualstudio.com/) (Editor recomendado com Terminal`(Ctrl + ')` integrado)


### Criando um Virtual Environment
Antes de instalar as dependências crie um Virtual Environment.

```shell
python -m venv .venv
```

Virtual Environment permite que as dependências dos projeto sejam instaladas de forma isolada para cada projeto ao invés de serem
instaladas globalmente o que poderia gerar conflitos caso você tenha mais de um projeto. Leia mais sobre [aqui](https://docs.python.org/3/library/venv.html).

Agora entre no Virtual Environment:

```shell
.venv\Scripts\activate
```

Toda vez que você for trabalhar no projeto você deverá executar o comando acima para trabalhar de dentro do Virtual Environment.

#### Troubleshooting

No Windows por default a [política de execução de scripts](https://learn.microsoft.com/pt-br/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4) é restrita. Provavelmente ao tentar executar o comando acima você irá receber um erro de não autorizado.

Para permitir execução de scripts abra o PowerShell como administrador e execute o comando abaixo:

```shell
Set-ExecutionPolicy -ExecutionPolicy AllSigned
```

Isso irá alterar a Política de Execução para permitir execução de scripts se o usuário permiter. Agora tente entrar no Virtual Environment novamente.

### Intalando dependencias
De dentro do Virtual Environment execute o comando abaixo para instalar as dependências:

```shell
python -m pip install -r requirements.txt
```


O arquivo `requirements.txt` contêm as dependências do projeto.

### Executando as migrations
Toda vez que uma nova migração for adicionada por você ou outra pessoa o comando abaixo deverá ser executado novamente.
Você também deve executá-lo na primeira vez durante o setup do projeto.

> **Aviso**: NUNCA modifique um arquivo de migração que já foi mesclado na branch `main` no remote, pois
são altas as chances de quebrar o esquema da database. Para alterar uma tabela ou campo crie um novo arquivo de migração.

De dentro do Virtual Environment rode as migrações para criar as tabelas do banco de dados:

```shell
python manage.py migrate
```

### Subindo o servidor
De dentro do Virtual Environment excute comando abaixo para rodar o servidor Django:

```shell
python manage.py runserver
```

### Criando migrations
Ao final de suas edições dos [models](accounts/models.py) você deve criar uma nova migração para atualizar os esquemas do banco de dados.
Saiba mais [aqui](https://docs.djangoproject.com/en/5.1/intro/tutorial02/#creating-models).

Para criar uma nova migration basta executar o comando abaixo. Um novo arquivo de migration será criado dentro do diretório
`accounts/migrations`

```shell
python manage.py makemigrations accounts
```

> **Nota**: Você deve ter lido acima que não se deve alterar uma migration que já foi mesclada na branch `main` no remote.
Todavia você pode e deve apagar e gerar uma nova migration que você está mexendo localmente. Apenas quando a sua migration
for mesclada na `main` é que ela não poderá ser modificada.