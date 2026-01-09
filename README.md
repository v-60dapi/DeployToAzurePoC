## Parâmetros Configuráveis

### Rede
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

### Virtual Machine
| Parâmetro | Valor Padrão | Descrição |
|-----------|--------------|-----------|
| vmName | vm-test-nat | Nome da VM de teste |
| vmSize | Standard_B2s | Tamanho da VM |
| adminUsername | azureuser | Nome do usuário admin |
| adminPassword | *obrigatório* | Senha do admin (mín. 12 caracteres) |
| osType | Windows | Sistema operacional (Windows/Linux) |
