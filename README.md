# ERPNext - ABLA

Branch *"version-13" representa a versão do ERP utilizada em produção. Não há CI/CD configurado. Para aplicação das mudanças em ambiente de produção basta logar no [ERP-Manager](https://erp-mng.abla.com.br/) na página Bench Manager e executar o bench update

## Guia para desenvolvimento

*Para acompanhar o guia recomenda-se familiaridade com a estrutura do frappe/bench utilizada - Ref.: 

. https://frappeframework.com/docs/v13/user/en/basics/architecture

. https://www.youtube.com/watch?v=eCAMPcl7NKc&list=PL3lFfCEoMxvzHtsZHFJ4T3n5yMM3nGJ1W&index=1

### Instalação

Para realizar o setup do erpnext para configuração local utiliza-se o Docker. Existe um guia oficial indicando os passos necessários:

https://github.com/frappe/frappe_docker

Atente à instalação do ERPNext, que deve ser feito usando esse repositório na branch version-13. 
Executando, por exemplo, o comando:

```
bench get-app --branch version-13 erpnext https://github.com/snlv-com-br/erpnext
```

### Alterações

Utilizando o VSCode é possível fazer alterações dentro do código do ERPNext, após propagar essa alterações, com *bench build* ou outros comando apropriados da [CLI Bench](https://frappeframework.com/docs/v13/user/en/bench/resources/bench-commands-cheatsheet), basta subir as alterações para esse repositório.

Recomenda-se o uso dos [hooks.py](https://github.com/snlv-com-br/erpnext/blob/version-13/erpnext/hooks.py) para alterações de html e css, e outras manipulações de variáveis.

---
## Implementando as alterações para uso dos sindicatos

### 📝 Inserindo clientes na plataforma:

Pré-requisitos:

#### Criação prévia dos seguintes itens: _`Tipo`, `Grupo de clientes`, `Território`, `Setor`_

O _`Tipo`_ de cliente é pré definido na plataforma como _Empresa_ para pessoa jurídica ou _Individual_ para pessoa física. No caso, basta inserir no csv uma das opções usando o _`Company`_ ou _`Individual`_.

<img width="500" alt="" src="https://media.discordapp.net/attachments/940697375767416883/940697388941713418/unknown.png">

Existem alguns _`Grupo de clientes`_ já criados como _Filiado_, _Desfiliado_ e _Parceiro_. Caso haja a necessidade de um novo grupo é possível a criação.  

<img alt="" src="https://media.discordapp.net/attachments/940697375767416883/940699263053234236/unknown.png">

A lacuna _`Território`_ é obrigatória na importação ou criação de novos clientes, sendo assim já existe cadastrado o território _Brazil_, com z mesmo. 

<img alt="" src="https://cdn.discordapp.com/attachments/940697375767416883/940700230838526022/unknown.png">

O _`Tipo de Setor`_ é usado para categorizar o porte da empresa, podendo ser _EPP_, _ME_, _MEDIA_, _MEDIA GRANDE_ ou _GRANDE_, também é possível a criação de outras categorias.

<img alt="" src="https://cdn.discordapp.com/attachments/940697375767416883/940700671093669938/unknown.png">

#### Criando o `.csv` para importação:

O arquivo (_.csv ou .xlsl_) precisa `obrigatoriamente` conter os seguintes campos: 

 - ID
 - Tipo
 - Grupo de clientes
 - Território 
 - Setor

Ademais são incluídos os seguintes campos `não-obrigatórios`:

- Nome completo
- NIF/NIPC
- ID de Email
- Nr. de Telemóvel
- Endereço primário
- Dados do cliente

<img alt="" src="https://media.discordapp.net/attachments/940697375767416883/940705731928277064/unknown.png">

Os campos são preenchidos com as seguintes informações:

- ID= _`esse campo fica vazio`_
- Tipo= _`Company`_ ou _`Individual`_
- Grupo de clientes= _`Filiado`_, _`Desfiliado`_ ou _`Parceiro`_
- Território= _`Brazil`_
- Setor= _`EPP`_, _`ME`_, _`MEDIA`_, _`MEDIA GRANDE`_ OU _`GRANDE`_
- Nome completo= _`Nome completo do cliente`_
- NIF/NIPC= _`CPF`_ ou _`CNPJ`_
- ID de Email= _`Email do cliente`_
- Nr. de Telemóvel= _`Telefone do cliente`_
- Endereço primário= _`CEP, endereço, número e bairro`_
- Dados do cliente= _`Cidade do cliente`_


### 📝 Inserindo potenciais clientes na plataforma:

#### Criando o `.csv` para importação:

O arquivo (_.csv ou .xlsl_) precisa `obrigatoriamente` conter os seguintes campos: 

 - ID
 - Status

Ademais são incluídos os seguintes campos `não-obrigatórios`:

- Nome da organização
- Endereço de e-mail
- Nr. de Telemóvel

<img alt="" src="https://cdn.discordapp.com/attachments/940697375767416883/940719048273039460/unknown.png">

Os campos são preenchidos com as seguintes informações:

- ID= _`esse campo fica vazio`_
- Status= _`esse campo fica vazio`_
- Nome da organização= _`Nome do potencial cliente ou parceiro`_
- Endereço de e-mail= _`Email do potencial cliente ou parceiro`_
- Nr. de Telemóvel= _`Telefone do potencial cliente ou parceiro`_

### 📝 Inserindo Subscritos na plataforma:
#### Para a inclusão dos subscritos na plataforma é necessário criar um _`Item`_ e associá-lo à um _`Plano de assinatura`_:

- _`Item`_: O _item_ é adicionado na seção Estoque. Ele é associado à um grupo e à ele é atribuído um código.
- _`Plano de assinatura`_: Para criar um novo _Plano de assinatura_ é necessário associá-lo à um _item_ e definir parâmetros como: _intervalo_, _custo_ etc.

<img alt="" src="https://cdn.discordapp.com/attachments/940697375767416883/940725375103815780/unknown.png">

#### Criando o `.csv` para importação de subscritos:

O arquivo (_.csv ou .xlsl_) precisa `obrigatoriamente` conter os seguintes campos: 

 - ID
 - Parte
 - Tipo de Parte
 - ID (Planos)
 - Plano (Planos)
 - Quantidade (Planos)

<img alt="" src="https://cdn.discordapp.com/attachments/940697375767416883/940730610505371768/unknown.png">

Os campos são preenchidos com as seguintes informações:

- ID= _`esse campo fica vazio`_
- Tipo de Parte= _`Customer`_
- Parte= _`Nome do cliente assinante`_
- ID (Planos)= _`esse campo fica vazio`_
- Plano (Planos)= _`EPP`_, _`ME`_, _`MEDIA`_, _`MEDIA GRANDE`_ ou _`GRANDE`_
- Quantidade (Planos)= _`1`_

---
## Guia para Produção -> Ubuntu 20.04

Para instalação em ambiente de produção utilizou-se as seguintes fontes de referência:

. https://github.com/frappe/frappe/wiki/The-Hitchhiker%27s-Guide-to-Installing-Frappe-on-Linux#tried-and-tested

. Para erro de permissão ao autenticar com servidor mariadb:
    https://discuss.erpnext.com/t/fresh-install-ends-with-error-access-denied-for-user-root-localhost/70519/2
    
. Para configuração de multi tenancy, supervisor e nginx
    https://codewithkarani.com/2021/09/16/setup-erpnext-for-production/
    https://codewithkarani.com/2021/08/24/setting-up-multi-tenancy-in-erpnext/
   
