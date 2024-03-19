# Atualiza-es-autom-ticas-de-seguran-a-do-ubuntu
Atualizações automáticas de segurança do ubuntu

# Como automatizar updates de segurança em um servidor Ubuntu
Antes de prosseguir, certifique-se de que a máquina está atualizada
<pre class="notranslate"><code class="notranslate">sudo apt update && apt upgrade</code></pre>
**COMANDOS**

**1. Certifique-se de que o Unattended-Upgrades está instalado. Geralmenete esse pacote é padrão do Ubuntu Server:
<pre class="notranslate"><code class="notranslate">apt-get install unattended-upgrades apt-listchanges</code></pre>
**2. Configure para que os pacotes sejam baixados e instalados no sistema:
Acesse o arquivo de configuração:
<pre class="notranslate"><code class="notranslate">nano /etc/apt/apt.conf.d/10periodic</code></pre>
Edite as linhas:
<pre class="notranslate"><code class="notranslate">APT::Periodic::Update-Package-Lists "1";APT::Periodic::Download-Upgradeable-Packages "1";APT::Periodic::AutocleanInterval "0";</code></pre>
**NOTA DO AUTOR: TALVEZ SEJA NECESSÁRIO ATIVAR O AUTOCLEANINTERVAL CASO O SERVIDOR COMEÇE A LOTAR DE LOGS DO APT** 

**3. Configure a frequência com que as atualizações serão instaladas. Nesse caso, será configurada como default para 1 dia:
Acesse o arquivo de configuração:
<pre class="notranslate"><code class="notranslate">nano /etc/apt/apt.conf.d/20auto-upgrades</code></pre>
Edite as linhas:
<pre class="notranslate"><code class="notranslate">APT::Periodic::Update-Package-Lists "1";APT::Periodic::Unattended-Upgrade "1";</code></pre>
**4. Para verificar os logs do Unattended-Upgrades, execute o comando:
<pre class="notranslate"><code class="notranslate">cat /var/log/unattended-upgrades/unattended-upgrades.log</code></pre>
Caso configurado corretamente, o retorno deve ser similar a esse:

**EXEMPLO DE RETORNO CASO HAJA PACOTES PARA ATUALIZAR:
<pre>2023-10-31 06:24:21,949 INFO Starting unattended upgrades script2023-10-31 06:24:21,950 INFO Allowed origins are: o=Ubuntu,a=jammy, o=Ubuntu,a=jammy-security, o=UbuntuESMApps,a=jammy-apps-security, o=UbuntuESM,a=jammy-infra-security2023-10-31 06:24:21,951 INFO Initial blacklist:2023-10-31 06:24:21,951 INFO Initial whitelist (not strict):2023-10-31 06:24:33,442 INFO Packages that will be upgraded: libmysqlclient21 linux-generic linux-headers-generic linux-image-generic linux-libc-dev mysql-client-8.0 mysql-client-core-8.0 mysql-server mysql-server-8.0 mysql-server-core-8.02023-10-31 06:24:33,443 INFO Writing dpkg log to /var/log/unattended-upgrades/unattended-upgrades-dpkg.log2023-10-31 06:39:27,915 INFO All upgrades installed2023-10-31 06:41:08,222 INFO Packages that were successfully auto-removed: linux-headers-5.15.0-83 linux-headers-5.15.0-83-generic linux-image-5.15.0-83-generic linux-modules-5.15.0-83-generic linux-modules-extra-5.15.0-83-generic/pre>
**EXEMPLO DE RETORNO CASO NÃO HAJA PACOTES PARA ATUALIZAR:
<pre style="white-space: pre-wrap; overflow: auto;">2023-10-30 06:39:59,784 INFO Starting unattended upgrades script2023-10-30 06:39:59,786 INFO Allowed origins are: o=Ubuntu,a=jammy, o=Ubuntu,a=jammy-security, o=UbuntuESMApps,a=jammy-apps-security, o=UbuntuESM,a=jammy-infra-security2023-10-30 06:39:59,786 INFO Initial blacklist:2023-10-30 06:39:59,786 INFO Initial whitelist (not strict):2023-10-30 06:40:05,283 INFO No packages found that can be upgraded unattended and no pending auto-removals</pre>

