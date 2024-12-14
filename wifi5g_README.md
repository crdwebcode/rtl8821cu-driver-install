# Tutorial de Instalação do Driver Realtek RTL8821CU (802.11ac NIC) no Ubuntu

Este tutorial descreve como instalar o driver para o adaptador Wi-Fi 5G com ID `0bda:c811` (Realtek Semiconductor Corp. 802.11ac NIC) no Ubuntu via terminal.

---

## **Pré-requisitos**
Certifique-se de ter os seguintes itens antes de iniciar:

1. **Sistema Ubuntu atualizado** (versão 22.04 LTS ou superior).
2. **Acesso à internet** para baixar dependências e o driver.

---

## **Passos para a instalação**

### **1. Atualizar o sistema**
Antes de começar, atualize o sistema:

```bash
sudo apt update && sudo apt upgrade -y
```

### **2. Instalar dependências necessárias**
Certifique-se de que as ferramentas de compilação e os cabeçalhos do kernel estão instalados:

```bash
sudo apt install build-essential dkms git linux-headers-$(uname -r) -y
```

### **3. Clonar o repositório do driver**
Baixe o driver RTL8821CU mais confiável diretamente do GitHub:

```bash
git clone https://github.com/brektrou/rtl8821CU.git
```

### **4. Compilar e instalar o driver**
Entre no diretório do driver clonado e instale usando o `dkms`:

```bash
cd rtl8821CU
sudo ./dkms-install.sh
```

O script compilará e instalará automaticamente o driver no sistema.

### **5. Verificar a instalação**
Após a instalação, verifique se o driver foi carregado corretamente:

```bash
lsmod | grep 8821cu
```

Se aparecer na lista, o driver foi carregado com sucesso.

### **6. Listar redes disponíveis**
Reinicie o gerenciador de rede para garantir que o adaptador esteja funcionando:

```bash
sudo systemctl restart NetworkManager
```

Liste as redes Wi-Fi disponíveis:

```bash
nmcli device wifi list
```

### **7. Conectar à rede Wi-Fi**
Conecte-se à rede Wi-Fi desejada. Substitua `SSID` pelo nome da rede e `senha_da_rede` pela senha:

```bash
nmcli device wifi connect "SSID" password "senha_da_rede"
```

---

## **Diagnóstico de Problemas**
Se encontrar problemas, use os comandos abaixo para diagnóstico:

1. **Verificar dispositivos USB conectados:**
   ```bash
   lsusb
   ```

2. **Checar logs do kernel para erros do driver:**
   ```bash
   dmesg | grep 8821cu
   ```

3. **Certificar-se de que o adaptador está ativo:**
   ```bash
   iwconfig
   ```

---

## **Desinstalar o Driver**
Caso precise remover o driver, execute:

```bash
cd rtl8821CU
sudo ./dkms-remove.sh
```

---

## **Notas Finais**
Este tutorial foi testado no Ubuntu 22.04 LTS com o adaptador Wi-Fi Realtek RTL8821CU. Caso encontre problemas, consulte a documentação do repositório [brektrou/rtl8821CU](https://github.com/brektrou/rtl8821CU).
