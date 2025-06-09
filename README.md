# Blog

Passo a passo para Criar um Blog com Azure Container Apps
Abaixo está um guia prático, baseado nos tutoriais oficiais da Microsoft e exemplos disponíveis, para você criar e publicar um blog (ou qualquer aplicação web) usando Azure Container Apps. O processo pode ser seguido mesmo sem acesso direto ao repositório do GitHub mencionado, pois os passos são universais para qualquer aplicação containerizada.

Pré-requisitos

Conta no Microsoft Azure (pode ser gratuita)

Azure CLI instalada em seu computador

Docker instalado, caso vá construir sua imagem localmente

Git instalado para clonar repositórios de exemplo

1. Instale e Configure a CLI do Azure
Abra o terminal e execute:

bash
az login
az upgrade
az extension add --name containerapp --upgrade --allow-preview true
az provider register --namespace Microsoft.App
az provider register --namespace Microsoft.OperationalInsights
Esses comandos garantem que você tenha a CLI e as extensões necessárias para trabalhar com Container Apps.

2. Defina Variáveis de Ambiente
No terminal, defina as variáveis que serão usadas nos comandos seguintes:

bash
export RESOURCE_GROUP="meu-blog-containerapps"
export LOCATION="brazilsouth" # ou a região de sua preferência
export ENVIRONMENT="env-meu-blog"
export APP_NAME="meu-blog"
Essas variáveis facilitam a execução dos comandos, pois você não precisa repetir os nomes a cada etapa.

3. Obtenha o Código do Blog
Se você já tem o código do seu blog (por exemplo, um projeto Node.js, Python, etc.), coloque-o em uma pasta com um Dockerfile. Se quiser usar um exemplo, clone um repositório de exemplo (substitua pelo seu projeto se preferir):

bash
git clone https://github.com/azure-samples/containerapps-albumapi-csharp.git
cd containerapps-albumapi-csharp/src
Troque pelo repositório do seu blog, se aplicável.

4. Crie o Grupo de Recursos
bash
az group create --name $RESOURCE_GROUP --location $LOCATION
O grupo de recursos organiza todos os recursos relacionados à sua aplicação no Azure.

5. Compile e Implemente o Container App
Se você já tem um Dockerfile pronto no diretório do seu projeto, basta rodar:

bash
az containerapp up \
  --name $APP_NAME \
  --resource-group $RESOURCE_GROUP \
  --location $LOCATION \
  --environment $ENVIRONMENT \
  --source .
Este comando faz tudo: cria o registro de container, constrói a imagem, publica no Azure Container Registry, cria o ambiente e o Container App, e faz o deploy da sua aplicação.

6. Acesse seu Blog
No final do comando acima, será exibido o endereço público (FQDN) do seu Container App. Basta acessar esse link no navegador para ver seu blog rodando na nuvem.
