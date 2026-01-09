# Deploy VNet com NAT Gateway e VM de Teste

Este template ARM cria uma infraestrutura de rede completa no Azure com uma Virtual Machine para validação de conectividade através do NAT Gateway.

## Arquitetura Provisionada

- **1 Virtual Network** (10.0.0.0/16)
- **2 Subnets** 
  - subnet-frontend (10.0.1.0/24)
  - subnet-backend (10.0.2.0/24)
- **1 NAT Gateway** com Public IP Standard
- **1 Virtual Machine** (Windows Server 2022 ou Ubuntu 22.04)
- **1 Network Security Group** (permite RDP/SSH)
- **1 Public IP** para acesso à VM
- **Associação automática** do NAT Gateway às subnets

## Deploy to Azure

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fv-60dapi%2fDeployToAzurePoC%2frefs%2fheads%2fmain%2fazuredeploy.json)

## Parâmetros Configuráveis

### Recursos de Rede

| Parâmetro | Valor Padrão | Descrição |
|-----------|--------------|-----------|
| vnetName | vnet-lab | Nome da Virtual Network |
| vnetAddressSpace | 10.0.0.0/16 | CIDR da VNet |
| subnet1Name | subnet-frontend | Nome da primeira subnet |
| subnet1Prefix | 10.0.1.0/24 | CIDR da primeira subnet |
| subnet2Name | subnet-backend | Nome da segunda subnet |
| subnet2Prefix | 10.0.2.0/24 | CIDR da segunda subnet |
| natGatewayName | nat-gateway-lab | Nome do NAT Gateway |
| publicIpName | pip-nat-gateway | Nome do Public IP do NAT Gateway |
| location | [resourceGroup().location] | Região do deployment |

### Virtual Machine

| Parâmetro | Valor Padrão | Descrição |
|-----------|--------------|-----------|
| vmName | vm-test-nat | Nome da VM de teste |
| vmSize | Standard_B2s | Tamanho da VM (2 vCPUs, 4 GB RAM) |
| adminUsername | azureuser | Nome do usuário administrador |
| adminPassword | **obrigatório** | Senha do admin (mínimo 12 caracteres) |
| osType | Windows | Sistema operacional (Windows ou Linux) |

## Instruções de Deployment

### Via Portal Azure

1. Clique no botão **Deploy to Azure** acima
2. Faça login no Azure Portal
3. Preencha os campos obrigatórios:
   - **Subscription**: Selecione sua subscription
   - **Resource Group**: Crie novo (ex: `rg-lab-natgateway`)
   - **Region**: Selecione `Brazil South`
   - **Admin Password**: Digite uma senha forte (ex: `Minimo123456!`)
4. Revise os demais parâmetros (valores padrão são recomendados)
5. Clique em **Review + create**
6. Clique em **Create**

**Tempo estimado**: 5-8 minutos

### Via Azure PowerShell

```powershell
# Conecte ao Azure
Connect-AzAccount

# Crie o Resource Group
$rgName = "rg-lab-natgateway"
$location = "brazilsouth"
New-AzResourceGroup -Name $rgName -Location $location

# Deploy do template
$templateUri = "https://raw.githubusercontent.com/v-60dapi/DeployToAzurePoC/refs/heads/main/azuredeploy.json"
$adminPassword = ConvertTo-SecureString "Minimo123456!" -AsPlainText -Force

New-AzResourceGroupDeployment `
    -ResourceGroupName $rgName `
    -TemplateUri $templateUri `
    -adminPassword $adminPassword `
    -osType "Windows" `
    -Verbose
