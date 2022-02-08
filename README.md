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

### [📝 Blog] Inserindo clientes na plataforma:

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

 -ID

 -Tipo

 -Grupo de clientes

 -Território 

 -Setor

Ademais são incluídos os seguintes campos `não-obrigatórios`:

-Nome completo

-NIF/NIPC

-ID de Email

-Nr. de Telemóvel

-Endereço primário

-Dados do cliente

<img alt="" src="https://media.discordapp.net/attachments/940697375767416883/940705731928277064/unknown.png">

Os campos são preenchidos com as seguintes informações:

-ID= _`esse campo fica vazio`_

-Tipo= _`Company`_ ou _`Individual`_

-Grupo de clientes= _`Uma das opções criadas na seção`_

-Território= _`Uma das opções criadas na seção`_

-Setor= _`Uma das opções criadas na seção`_

-Nome completo= _`Nome completo do cliente`_

-NIF/NIPC= _`CPF`_ ou _`CNPJ`_

-ID de Email= _`Email do cliente`_

-Nr. de Telemóvel= _`Telefone do cliente`_

-Endereço primário= _`CEP, endereço, número e bairro`_

-Dados do cliente= _`Cidade do cliente`_
## Guia para Produção -> Ubuntu 20.04

Para instalação em ambiente de produção utilizou-se as seguintes fontes de referência:

. https://github.com/frappe/frappe/wiki/The-Hitchhiker%27s-Guide-to-Installing-Frappe-on-Linux#tried-and-tested

. Para erro de permissão ao autenticar com servidor mariadb:
    https://discuss.erpnext.com/t/fresh-install-ends-with-error-access-denied-for-user-root-localhost/70519/2
    
. Para configuração de multi tenancy, supervisor e nginx
    https://codewithkarani.com/2021/09/16/setup-erpnext-for-production/
    https://codewithkarani.com/2021/08/24/setting-up-multi-tenancy-in-erpnext/
   
<br/>

<div align="center">
    <img src="https://raw.githubusercontent.com/frappe/erpnext/develop/erpnext/public/images/erpnext-logo.png" height="128">
    <h2>ERPNext</h2>
    <p align="center">
        <p>ERP made simple</p>
    </p>

[![CI](https://github.com/frappe/erpnext/actions/workflows/ci-tests.yml/badge.svg?branch=develop)](https://github.com/frappe/erpnext/actions/workflows/ci-tests.yml)
[![Open Source Helpers](https://www.codetriage.com/frappe/erpnext/badges/users.svg)](https://www.codetriage.com/frappe/erpnext)
[![Coverage Status](https://coveralls.io/repos/github/frappe/erpnext/badge.svg?branch=develop)](https://coveralls.io/github/frappe/erpnext?branch=develop)

[https://erpnext.com](https://erpnext.com)

</div>

- ~ ERPNext ~ as a monolith includes the following areas for managing businesses:

1. [Accounting](https://erpnext.com/open-source-accounting)
1. [Warehouse Management](https://erpnext.com/distribution/warehouse-management-system)
1. [CRM](https://erpnext.com/open-source-crm)
1. [Sales](https://erpnext.com/open-source-sales-purchase)
1. [Purchase](https://erpnext.com/open-source-sales-purchase)
1. [HRMS](https://erpnext.com/open-source-hrms)
1. [Project Management](https://erpnext.com/open-source-projects)
1. [Support](https://erpnext.com/open-source-help-desk-software)
1. [Asset Management](https://erpnext.com/open-source-asset-management-software)
1. [Quality Management](https://erpnext.com/docs/user/manual/en/quality-management)
1. [Manufacturing](https://erpnext.com/open-source-manufacturing-erp-software)
1. [Website Management](https://erpnext.com/open-source-website-builder-software)
1. [Customize ERPNext](https://erpnext.com/docs/user/manual/en/customize-erpnext)
1. [And More](https://erpnext.com/docs/user/manual/en/)

ERPNext requires MariaDB.

ERPNext is built on the [Frappe Framework](https://github.com/frappe/frappe), a full-stack web app framework built with Python & JavaScript.

- [User Guide](https://erpnext.com/docs/user)
- [Discussion Forum](https://discuss.erpnext.com/)

---

### Containerized Installation

Use docker to deploy ERPNext in production or for development of [Frappe](https://github.com/frappe/frappe) apps. See https://github.com/frappe/frappe_docker for more details.

### Full Install

The Easy Way: our install script for bench will install all dependencies (e.g. MariaDB). See https://github.com/frappe/bench for more details.

New passwords will be created for the ERPNext "Administrator" user, the MariaDB root user, and the frappe user (the script displays the passwords and saves them to ~/frappe_passwords.txt).

### Virtual Image

You can download a virtual image to run ERPNext in a virtual machine on your local system.

- [ERPNext Download](http://erpnext.com/download)

System and user credentials are listed on the download page.

---

## License

GNU/General Public License (see [license.txt](license.txt))

The ERPNext code is licensed as GNU General Public License (v3) and the Documentation is licensed as Creative Commons (CC-BY-SA-3.0) and the copyright is owned by Frappe Technologies Pvt Ltd (Frappe) and Contributors.

---

## Contributing

1. [Issue Guidelines](https://github.com/frappe/erpnext/wiki/Issue-Guidelines)
1. [Report Security Vulnerabilities](https://erpnext.com/security)
1. [Pull Request Requirements](https://github.com/frappe/erpnext/wiki/Contribution-Guidelines)
1. [Translations](https://translate.erpnext.com)
1. [Chart of Accounts](https://charts.erpnext.com)

---

## Logo and Trademark

The brand name ERPNext and the logo are trademarks of Frappe Technologies Pvt. Ltd.

### Introduction

Frappe Technologies Pvt. Ltd. (Frappe) owns and oversees the trademarks for the ERPNext name and logos. We have developed this trademark usage policy with the following goals in mind:

- We’d like to make it easy for anyone to use the ERPNext name or logo for community-oriented efforts that help spread and improve ERPNext.
- We’d like to make it clear how ERPNext-related businesses and projects can (and cannot) use the ERPNext name and logo.
- We’d like to make it hard for anyone to use the ERPNext name and logo to unfairly profit from, trick or confuse people who are looking for official ERPNext resources.

### Frappe Trademark Usage Policy

Permission from Frappe is required to use the ERPNext name or logo as part of any project, product, service, domain or company name.

We will grant permission to use the ERPNext name and logo for projects that meet the following criteria:

- The primary purpose of your project is to promote the spread and improvement of the ERPNext software.
- Your project is non-commercial in nature (it can make money to cover its costs or contribute to non-profit entities, but it cannot be run as a for-profit project or business).
Your project neither promotes nor is associated with entities that currently fail to comply with the GPL license under which ERPNext is distributed.
- If your project meets these criteria, you will be permitted to use the ERPNext name and logo to promote your project in any way you see fit with one exception: Please do not use ERPNext as part of a domain name.

Use of the ERPNext name and logo is additionally allowed in the following situations:

All other ERPNext-related businesses or projects can use the ERPNext name and logo to refer to and explain their services, but they cannot use them as part of a product, project, service, domain, or company name and they cannot use them in any way that suggests an affiliation with or endorsement by ERPNext or Frappe Technologies or the ERPNext open source project. For example, a consulting company can describe its business as “123 Web Services, offering ERPNext consulting for small businesses,” but cannot call its business “The ERPNext Consulting Company.”

Similarly, it’s OK to use the ERPNext logo as part of a page that describes your products or services, but it is not OK to use it as part of your company or product logo or branding itself. Under no circumstances is it permitted to use ERPNext as part of a top-level domain name.

We do not allow the use of the trademark in advertising, including AdSense/AdWords.

Please note that it is not the goal of this policy to limit commercial activity around ERPNext. We encourage ERPNext-based businesses, and we would love to see hundreds of them.

When in doubt about your use of the ERPNext name or logo, please contact Frappe Technologies for clarification.

(inspired by WordPress)
