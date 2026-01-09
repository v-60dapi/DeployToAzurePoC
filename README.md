# Deploy VNet com NAT Gateway - Lab

Este template ARM cria uma infraestrutura de rede completa no Azure.

## Recursos Provisionados

- 1 Virtual Network (10.0.0.0/16)
- 2 Subnets (subnet-frontend: 10.0.1.0/24 e subnet-backend: 10.0.2.0/24)
- 1 NAT Gateway com Public IP Standard
- Associação automática do NAT Gateway às subnets

## Deploy to Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fv-60dapi%2fDeployToAzurePoC%2frefs%2fheads%2fmain%2fazuredeploy.json)

## Parâmetros Configuráveis

| Parâmetro | Valor Padrão | Descrição |
|-----------|--------------|-----------|
| vnetName | vnet-lab | Nome da Virtual Network |
| vnetAddressSpace | 10.0.0.0/16 | CIDR da VNet |
| subnet1Name | subnet-frontend | Nome da primeira subnet |
| subnet1Prefix | 10.0.1.0/24 | CIDR da primeira subnet |
| subnet2Name | subnet-backend | Nome da segunda subnet |
| subnet2Prefix | 10.0.2.0/24 | CIDR da segunda subnet |
| natGatewayName | nat-gateway-lab | Nome do NAT Gateway |
| publicIpName | pip-nat-gateway | Nome do Public IP |
| location | [resourceGroup().location] | Região do deployment |

## Instruções de Deployment

1. Clique no botão **Deploy to Azure**
2. Faça login no portal Azure
3. Selecione sua **Subscription**
4. Crie ou selecione um **Resource Group** (ex: rg-lab-natgateway)
5. Escolha a **Region** (recomendado: Brazil South)
6. Ajuste os parâmetros se necessário
7. Clique em **Review + create**
8. Clique em **Create**

Tempo estimado de deployment: 3-5 minutos
