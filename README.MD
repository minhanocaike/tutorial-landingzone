# Terraform Azure Landing Zone

# Introdução 📃

Este repositório tem como objetivo servir de exemplo para um modelo de implementação de landing zone
com Terraform. Os diretorios listados são um modelo de abordagem para estruturação do seu projeto.


# Diretórios 📁

```jsx
├── azure-pipelines
│   ├── azure-pipelines.yml
│   ├── terraform-apply.yml
│   ├── terraform-plan.yml
│   └── terraform-validate.yml
│   └── terraform-validate.yml
├── core
│   ├── nonproduction
│   └── production
├── modules
│   ├── computing
│   ├── container
│   ├── database
│   ├── key-vault
│   ├── monitoring
│   ├── networking
│   ├── security
│   ├── storage-account
│   └── ...
├── README.md
└── settings
    └── scripts

```

```jsx
├── azure-pipelines
```
Os scripts utilizados para execução das esteiras no Azure DevOps, podem estar contidos neste diretório.

```
├── modules

```
Este diretório contêm os arquivos e diretórios que serão implementados em cloud seguindo as melhores práticas,
utilizando os módulos terraform para reutilização de recursos com as regras de implementação bem definidas.

```
── core
   ├── nonproduction
   │   ├── infrahub
   │   │   ├── connectivity
   │   │   │    ├── backend.tf
   │   │   │    ├── data.tf
   │   │   │    ├── main.tf
   │   │   │    └── variables.tf
   │   │   └── corp
   │   │        ├── backend.tf
   │   │        ├── data.tf
   │   │        ├── main.tf
   │   │        └── variables.tf
   │       └── ...
   │   └── corp
   │       └── project-name
   │           ├── backend.tf
   │           ├── data.tf
   │           ├── main.tf
   │           └── variables.tf
   │       └── ...
   └──
         

```
Este diretório contêm os arquivos raiz para a criação da infraestrutura por ambiente e projeto

Está organizado da seguinte forma:

- **nonproduction** → Contém as landing zones não produtivas agrupando por projeto os arquivos principais para provisionamento do terraform.
- **production** → Contém as landing zones de produção agrupando por projeto os arquivos principais para provisionamento do terraform.
- **infrahub** → Nesse diretório estão os arquivos que são necessários para criação dos recursos base de infraestrutura para cada landing zone, que serão integrados com conectividade.
- **connectivity** → Nesse diretório estão os arquivos para provisionamento dos recursos na subscriptoin hub (**Disia - Connectivity**). Obs: Aparece somente no diretório ***production*** pois não possui um ambiente de testes para landing zone hub.


```jsx
└── settings
    └── scripts
```
O diretório *settings* agrupa arquivos e scripts para utilização no backend (template para publicação no azure), etc.

# Deploy 📥

Para executar os scripts é necessário a esteira de infraestrutura para o projeto com os scripts de implantação.

---

Para visualizar o que será criado/alterado executar: `Terrafom plan`

Para implantação efetiva no ambiente executar: `Terraform apply`

# Principais Arquivos ‼️

```
main.tf
```

Este arquivo irá conter o provisionamento dos principais recursos para o projeto (chamada de módulos terraform e recursos locais)

```
variables.tf
```

Neste arquivo serão incluídas todas as variáveis utilizadas no módulo em questão 

|— Para variáveis utilizadas para nomear recursos ou definir nomes dentro do projeto, utilizar camelCase 

|— Para variáveis que definam o tamanho em termos númericos (tamanho de disco, tamanho de RAM) separar por "_", exemplo: ram_size_gb

```
outputs.tf
```

Contêm as saídas do módulo que serão gerados no main.tf

```
backend.tf
```

Arquivo para configuração de providers utilizados no projeto, as variáveis e credenciais com permissão de execução estão configuradas no grupo de váriaveiss referente a landing zone no Azure DevOps.
