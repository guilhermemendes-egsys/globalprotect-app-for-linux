# Instalação do Cliente GlobalProtect VPN no Linux



A plataforma de segurança de rede para endpoints GlobalProtect™, um tipo de rede privada virtual (VPN). Permite proteger a força de trabalho móvel das organizações ao garantir o acesso seguro a todos os colaboradores, independentemente do dispositivo ou da localização, com a utilização dos recursos do firewall da empresa Palo Alto Networks. Que provê conexão criptografada entre o equipamento móvel e a organização, além de assegurar recursos de prevenção de ameaças para proteger contra tráfego evasivo de aplicativos, phishing, roubo de credenciais e muito mais.

> Como os administradores do GlobalProtect determinam quais versões do aplicativo são necessárias em suas próprias organizações, o link de download está disponível apenas no portal do GlobalProtect, geralmente para os sistemas operacionais Windows e Mac 32/64. Não há link para download do aplicativo no site da Palo Alto Networks.

## Demonstrarei a instalação da versão 6.0 do GlobalProtect via interface de linha de comando (CLI).

### 1 Instalação

1.1 Para iniciar o processo de instalação será necessário baixar o aplicativo do repositório git a seguir.
Abra o terminal pressionando em simultâneo, as teclas “Ctrl + Alt + T” e execute os comandos abaixo para entrar na pasta  downloads e baixar o aplicativo para Linux:
```
cd ~/Downloads
```
```
wget https://github.com/aljes96/globalprotect-app-for-linux/raw/main/PanGPLinux-6.0.0-c18.tgz
```

1.2 Descompacte o arquivo TGZ baixado com o comando a seguir:
```
tar -xvzf PanGPLinux-6.0.0-c18.tgz
```

1.3 Iniciando a instalação
Logo após descompactar o arquivo, execute o comando abaixo conforme sua distro, para proceder à instalação:
Se utiliza uma distribuição baseada em **Debian/Ubuntu**.
```
sudo dpkg -i GlobalProtect_deb-6.0.0.1-44.deb
```

Se utiliza uma distribuição baseada em **Red Hat/CentOS/Fedora**.
```
sudo rpm -i GlobalProtect_rpm-6.0.0.1-44.rpm
```

Uma vez instalado, você pode visualizar os comandos disponíveis com `globalprotect help`
```
Usage: globalprotect [COMMAND] [OPTIONS] [args...]

COMMAND: Specifies the action to perform. It can be one of the following:
collect-log            -- collect log information
connect                -- connect to server
disconnect             -- disconnect
disable                -- disable connection
import-certificate     -- import client certificate file
quit                   -- quit from prompt mode
rediscover-network     -- network rediscovery
remove-user            -- clear credential
resubmit-hip           -- resubmit HIP information
set-log                -- set debug level
show                   -- show information

OPTIONS: Specifies options for the selected command.
Input a command and then press tab to get options for the selected command.
Read more details in man globalprotect.

EXAMPLES:
Connect to portal with user id:
>> connect -p gp.acme.com -u test

Show current status:
>> show --status
```

### 2 Estabelecendo a conexão VPN
Para conectar execute a linha abaixo, substituindo “vpn.organizacao.com” pelo endereço de VPN fornecido para acesso.
```
globalprotect connect --portal vpn.empresa.com.br
```
Exemplo: 
```
globalprotect connect --portal vpn2.tjro.jus.br
```

Em seguida informe o "usuário" e "senha" de acesso.
> Só é necessário na primeira utilização.
```
username: usuário do domínio
Password: senha do usuário
Discovering network...                                                 
Connecting...                                                          
Connected
```
A Partir desse momento você já estará conectado na VPN, o que significa que você estará acessando todos os recursos que lhes fora garantido no momento da sua concessão de acesso à rede, como se estivesse nas dependências da organização.

Após a configuração e sempre que pretender iniciar a VPN, deverá e executar o seguinte comando no terminal:
```
globalprotect connect
```

Verifique se a conexão ao serviço de VPN está funcionando corretamente:
```
globalprotect show --status && globalprotect show --details
```

Desconectando da VPN:
```
globalprotect disconnect
```

Pode-se criar alias, por exemplo nos arquivos .bashrc ou .zshrc, para não precisar digitar toda a linha de comando.
```
cat >>~/.zshrc <<-'EOF'
# GlobalProtect
alias vpnc="globalprotect connect"
alias vpns="globalprotect show --status && globalprotect show --details"
alias vpnd="globalprotect disconnect"
EOF
```
```
source ~/.zshrc
```


Nota: Procedimento testado com sucesso na(s) seguinte(s) Distro(s):
- Ubuntu: 20.04

### Precisa de mais ajuda?
[Nova mensagem](https://github.com/aljes96/globalprotect-app-for-linux/issues/new/choose)


### Referências
[GlobalProtect App for Linux](https://docs.paloaltonetworks.com/globalprotect/6-0/globalprotect-app-user-guide/globalprotect-app-for-linux)

Publicado em [https://dev.to/aljes96](https://dev.to/aljes96/instalacao-do-cliente-globalprotect-vpn-no-linux-47m0)
