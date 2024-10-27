# Configuração de Rede Local Básica no Ubuntu 22.04 com Samba

Este projeto configura uma rede local básica no Ubuntu 22.04, utilizando o Samba para compartilhar pastas e permitir acesso a partir de outros dispositivos na rede, incluindo sistemas Windows.

## Pré-requisitos

- Ubuntu 22.04 instalado e atualizado
- Conexão com a rede local (LAN)
- Acesso root ou permissões sudo

## Passo a Passo

### 1. Instalar o Samba

1. Atualize o sistema e instale o Samba com o seguinte comando:
   ```bash
   sudo apt update
   sudo apt install samba

2. Verifique se o Samba foi instalado corretamente:
   ```bash
   sudo systemctl status smbd
### 2. Configurar uma Pasta para Compartilhamento
1. Escolha ou crie a pasta que deseja compartilhar. Exemplo:
   ```bash
   mkdir ~/compartilhado

2. Defina as permissões corretas para a pasta:
   ```bash
   sudo chmod 777 ~/compartilhado
3. Edite o arquivo de configuração do Samba:
   ```bash
   sudo nano /etc/samba/smb.conf
4. Adicione a seguinte configuração ao final do arquivo:
   ```bash
   [compartilhado]
    path = /home/seu_usuario/compartilhado
    browsable = yes
    writable = yes
    guest ok = yes
    read only = no
  Nota: Substitua /home/seu_usuario/compartilhado pelo caminho completo da pasta que deseja compartilhar.

5. Salve e feche o arquivo (CTRL + O para salvar e CTRL + X para sair).
6. Reinicie o serviço Samba para aplicar as mudanças:
   ```bash
   sudo systemctl restart smbd
### 3. Configurar o Firewall
     Caso o firewall esteja ativo no Ubuntu, permita o tráfego do Samba com o comando:
     ```bash
    sudo ufw allow samba
### 4. Acessar a Pasta Compartilhada de Outro Dispositivo
Agora, a pasta compartilhada estará acessível para outros dispositivos na mesma rede.
1. No Windows:
   - Abra o Explorador de Arquivos e vá até Rede para ver o computador Ubuntu.
   - Ou acesse diretamente pelo IP do Ubuntu no Explorador:
     ```bash
     \\IP_do_Ubuntu\compartilhado
2. No Linux:
   - Abra o Gerenciador de Arquivos e acesse a rede para visualizar a pasta compartilhada.
   - Ou utilize o comando smbclient no terminal para acessar diretamente.

### Solução de Problemas
  - Erro de permissão: Verifique se as permissões da pasta estão definidas corretamente (chmod 777).
  - Firewall: Verifique se o firewall está configurado para permitir o tráfego do Samba (sudo ufw allow samba).
  - Reiniciar o Samba: Após mudanças no arquivo de configuração, sempre reinicie o Samba.

### Autor
  Este projeto foi desenvolvido como um guia para configurar redes locais no Ubuntu 22.04 usando o Samba.

### Licença
  Este projeto está licenciado sob a licença MIT - veja o arquivo LICENSE para mais detalhes.
  ```bash

Essa documentação explica cada etapa para configurar a rede, incluindo detalhes importantes para garantir a funcionalidade da configuração.
