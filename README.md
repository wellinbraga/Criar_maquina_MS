# Guia para Criação de Máquina Virtual no Microsoft Azure

Este documento orienta como criar uma Máquina Virtual (VM) no Microsoft Azure, com foco em boas práticas, segurança e controle de custos.

---

## ☁️ Pré-requisitos

Antes de iniciar, certifique-se de ter:

- Uma conta Microsoft com acesso ao [Azure Portal](https://portal.azure.com/)
- Uma assinatura ativa do Azure (pode ser gratuita ou paga)
- Permissões adequadas para criar recursos (como Owner ou Contributor)

---

## 🚀 Passo a Passo para Criar uma Máquina Virtual

### 1. Acesse o Azure Portal
Vá para [https://portal.azure.com](https://portal.azure.com) e faça login com sua conta Microsoft.

### 2. Inicie a criação da VM
- No menu lateral, clique em **"Máquinas virtuais"**.
- Clique em **"+ Criar"** > **"Máquina virtual"**.

### 3. Configure as Informações Básicas
- **Assinatura**: Selecione sua assinatura ativa.
- **Grupo de Recursos**: Crie um novo ou use um existente.
- **Nome da VM**: Dê um nome significativo.
- **Região**: Escolha uma região próxima de você ou do seu público-alvo (ex: Brazil South).
- **Imagem**: Escolha o sistema operacional (ex: Ubuntu 22.04 LTS, Windows Server 2022).
- **Tamanho da VM**: Use uma instância de baixo custo para testes, como `B1s` ou `Standard_D2s_v3`.

> 💡 **Dica**: A série B é ideal para cargas leves e economiza custos em ambientes de desenvolvimento e testes.

### 4. Configurar autenticação
- Escolha entre **Chave SSH** (Linux) ou **Senha** (Windows).
- Para Linux, gere um par de chaves SSH se ainda não tiver:
  ```bash
  ssh-keygen -t rsa -b 2048

##### 5. Discos

- Use disco SSD padrão (Standard SSD) para balancear desempenho e custo  
- Habilite criptografia automática

##### 6. Rede

- Crie uma nova rede virtual (VNet) ou utilize uma existente  
- Habilite **grupo de segurança de rede (NSG)** com regras mínimas:
  - Permitir **porta 22** para SSH (Linux) ou **porta 3389** para RDP (Windows)  
  - Evite liberar portas públicas desnecessárias

##### 7. Monitoramento

- Habilite o monitoramento básico (Diagnostics) se desejar acompanhar o uso  
- Desmarque recursos adicionais como backup e auto-shutdown, a menos que necessário

##### 8. Revisar e Criar

- Revise as configurações finais  
- Clique em **"Criar"**

##### ✅ Boas Práticas

- **Nomeação Padronizada**: Use nomes consistentes (ex: `vm-dev-ubuntu-eastus`)  
- **Tags**: Utilize tags para organização e controle de custos (ex: `ambiente=dev`, `projeto=sitex`)  
- **Grupos de Recursos**: Agrupe recursos relacionados para facilitar o gerenciamento  
- **Backups**: Configure backup regular se estiver usando a VM para produção  
- **Atualizações**: Mantenha o sistema operacional e softwares atualizados  
- **Segurança**: Use firewalls, NSG e atualize chaves SSH periodicamente

##### 💸 Cuidados com Custos

- ⚠️ **Máquinas Virtuais em execução geram custos continuamente**  
- Use **auto-shutdown** para desligar VMs automaticamente fora do horário comercial  
- Monitore os custos no portal: **Custos e Cobrança > Visão Geral**  
- Use a **calculadora de preços do Azure**: https://azure.microsoft.com/pricing/calculator/  
- Para testes, prefira regiões com menor custo e instâncias mais baratas (`B1s`, `A0`, etc)  
- Avalie o uso de **Azure Spot VMs** para workloads temporários

##### 📎 Recursos Úteis

- [Documentação oficial do Azure](https://learn.microsoft.com/azure/virtual-machines/)  
- [Calculadora de preços](https://azure.microsoft.com/pricing/calculator/)  
- [CLI do Azure](https://learn.microsoft.com/cli/azure/install-azure-cli)  
- [Azure Free Tier](https://azure.microsoft.com/free/)

