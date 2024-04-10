---
title: Uso do cURL com AEM
description: Saiba como usar cURL para tarefas comuns do Adobe Experience Manager.
contentOwner: Silviu Raiman
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: e3f018e6-563e-456f-99d5-d232f1a4aa55
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---

# Uso do cURL com AEM{#using-curl-with-aem}

Os administradores geralmente precisam automatizar ou simplificar tarefas comuns em qualquer sistema. No AEM, por exemplo, gerenciar usuários, instalar pacotes e gerenciar pacotes OSGi são tarefas que geralmente devem ser realizadas.

Devido à natureza RESTful da estrutura do Sling no qual o AEM é criado, a maioria das tarefas pode ser feita com uma chamada de URL. O cURL pode ser usado para executar essas chamadas de URL e pode ser uma ferramenta útil para administradores de AEM.

## O que é cURL {#what-is-curl}

cURL é uma ferramenta de linha de comando de código aberto usada para executar manipulações de URL. Ele suporta uma ampla gama de protocolos de internet, incluindo HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP e RTSP.

O cURL é uma ferramenta bem estabelecida e amplamente usada para obter ou enviar dados usando a sintaxe de URL e foi lançado originalmente em 1997. O nome cURL originalmente significava &quot;ver URL&quot;.

Devido à natureza RESTful da estrutura do Sling no qual o AEM é criado, a maioria das tarefas pode ser reduzida a uma chamada de URL, que pode ser executada com cURL. [Tarefas de manipulação de conteúdo](/help/sites-administering/curl.md#common-content-manipulation-aem-curl-commands) como ativar páginas e iniciar workflows e [tarefas operacionais](/help/sites-administering/curl.md#common-operational-aem-curl-commands) como gerenciamento de pacotes e gerenciamento de usuários podem ser automatizados usando cURL. Além disso, você pode [criar seu próprio cURL](/help/sites-administering/curl.md#building-a-curl-ready-aem-command) para a maioria das tarefas no AEM.

>[!NOTE]
>
>Qualquer comando AEM executado por meio de cURL deve ser autorizado da mesma forma que qualquer usuário para AEM. Todas as ACLs e direitos de acesso são respeitados ao usar cURL para executar um comando AEM.

## Baixando cURL {#downloading-curl}

O cURL é uma parte padrão do macOS e de algumas distribuições Linux. No entanto, ele está disponível para a maioria dos sistemas operacionais. Os downloads mais recentes podem ser encontrados em [https://curl.haxx.se/download.html](https://curl.haxx.se/download.html).

O repositório de origem do cURL também pode ser encontrado no GitHub.

## Criação de um comando AEM cURL-Ready {#building-a-curl-ready-aem-command}

Os comandos cURL podem ser criados para a maioria das operações no AEM, como acionar workflows, verificar configurações OSGi, acionar comandos JMX, criar agentes de replicação e muito mais.

Para localizar o comando exato necessário para sua operação específica, é necessário usar as ferramentas do desenvolvedor em seu navegador para capturar a chamada de POST para o servidor quando você executa o comando AEM.

As etapas a seguir descrevem como fazer isso usando a criação de uma nova página no navegador Chrome como exemplo.

1. Prepare a ação que deseja chamar no AEM. Neste caso, prosseguimos até ao final do **Criar página** assistente, mas ainda não clicaram **Criar**.

   ![chlimage_1-66](assets/chlimage_1-66a.png)

1. Inicie as ferramentas do desenvolvedor e selecione a variável **Rede** guia. Clique em **Preservar log** antes de limpar o console.

   ![chlimage_1-67](assets/chlimage_1-67a.png)

1. Clique em **Criar** no **Criar página** assistente para realmente criar o fluxo de trabalho.
1. Clique com o botão direito do mouse na ação de POST resultante e selecione **Copiar** > **Copiar como cURL**.

   ![chlimage_1-68](assets/chlimage_1-68a.png)

1. Copie o comando cURL para um editor de texto e remova todos os cabeçalhos do comando, que começam com `-H` (destacado em azul na imagem abaixo) e adicione o parâmetro de autenticação adequado, como `-u <user>:<password>`.

   ![chlimage_1-69](assets/chlimage_1-69a.png)

1. Execute o comando cURL pela linha de comando e exiba a resposta.

   ![chlimage_1-70](assets/chlimage_1-70a.png)

## Comandos comuns do AEM cURL operacional {#common-operational-aem-curl-commands}

Esta é uma lista de comandos cURL do AEM para tarefas administrativas e operacionais comuns.

>[!NOTE]
>
>Os exemplos a seguir pressupõem que o AEM esteja em execução `localhost` na porta `4502` e usa o usuário `admin` com senha `admin`. Espaços reservados para comandos adicionais são definidos entre colchetes.

### Gerenciamento de pacotes {#package-management}

#### Listar todos os pacotes instalados

```shell
curl -u <user>:<password> http://<host>:<port>/crx/packmgr/service.jsp?cmd=ls
```

#### Criar um pacote {#create-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=create -d packageName=<name> -d groupName=<name>
```

#### Visualizar um pacote {#preview-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=preview
```

#### Listar conteúdo do pacote {#list-package-content}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/console.html/etc/packages/mycontent.zip?cmd=contents
```

#### Criar um pacote {#build-a-package}

```shell
curl -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=build
```

#### Reajustar um pacote {#rewrap-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/mycontent.zip?cmd=rewrap
```

#### Renomear um pacote {#rename-a-package}

```shell
curl -u <user>:<password> -X POST -Fname=<New Name> http://localhost:4502/etc/packages/<Group Name>/<Package Name>.zip/jcr:content/vlt:definition
```

#### Carregar um pacote {#upload-a-package}

```shell
curl -u <user>:<password> -F cmd=upload -F force=true -F package=@test.zip http://localhost:4502/crx/packmgr/service/.json
```

#### Instalar um pacote {#install-a-package}

```shell
curl -u <user>:<password> -F cmd=install http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Desinstalar um pacote {#uninstall-a-package}

```shell
curl -u <user>:<password> -F cmd=uninstall http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Excluir um pacote {#delete-a-package}

```shell
curl -u <user>:<password> -F cmd=delete http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip
```

#### Baixar um pacote {#download-a-package}

```shell
curl -u <user>:<password> http://localhost:4502/etc/packages/my_packages/test.zip
```

#### Replicar um pacote {#replicate-a-package}

```shell
curl -u <user>:<password> -X POST http://localhost:4502/crx/packmgr/service/.json/etc/packages/my_packages/test.zip?cmd=replicate
```

### Gerenciamento de usuários {#user-management}

#### Criar um novo usuário {#create-a-new-user}

```shell
curl -u <user>:<password> -FcreateUser= -FauthorizableId=hashim -Frep:password=hashim http://localhost:4502/libs/granite/security/post/authorizables
```

#### Criar um novo grupo {#create-a-new-group}

```shell
curl -u <user>:<password> -FcreateGroup=group1 -FauthorizableId=testGroup1 http://localhost:4502/libs/granite/security/post/authorizables
```

#### Adicionar uma propriedade a um usuário existente {#add-a-property-to-an-existing-user}

```shell
curl -u <user>:<password> -Fprofile/age=25 http://localhost:4502/home/users/h/hashim.rw.html
```

#### Criar um usuário com um perfil {#create-a-user-with-a-profile}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=hashimkhan -Frep:password=hashimkhan -Fprofile/gender=male http://localhost:4502/libs/granite/security/post/authorizables
```

#### Criar um novo usuário como membro de um grupo {#create-a-new-user-as-a-member-of-a-group}

```shell
curl -u <user>:<password> -FcreateUser=testuser -FauthorizableId=testuser -Frep:password=abc123 -Fmembership=contributor http://localhost:4502/libs/granite/security/post/authorizables
```

#### Adicionar um usuário a um grupo {#add-a-user-to-a-group}

```shell
curl -u <user>:<password> -FaddMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Remover um usuário de um grupo {#remove-a-user-from-a-group}

```shell
curl -u <user>:<password> -FremoveMembers=testuser1 http://localhost:4502/home/groups/t/testGroup.rw.html
```

#### Definir a associação de grupo de um usuário {#set-a-user-s-group-membership}

```shell
curl -u <user>:<password> -Fmembership=contributor -Fmembership=testgroup http://localhost:4502/home/users/t/testuser.rw.html
```

#### Excluir um usuário {#delete-a-user}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/users/t/testuser
```

#### Excluir um grupo {#delete-a-group}

```shell
curl -u <user>:<password> -FdeleteAuthorizable= http://localhost:4502/home/groups/t/testGroup
```

### Backup {#backup}

Consulte [Backup e restauração](/help/sites-administering/backup-and-restore.md#automating-aem-online-backup) para obter detalhes.

### OSGi {#osgi}

#### Iniciar um pacote {#starting-a-bundle}

```shell
curl -u <user>:<password> -Faction=start http://localhost:4502/system/console/bundles/<bundle-name>
```

#### Interrupção de um pacote {#stopping-a-bundle}

```shell
curl -u <user>:<password> -Faction=stop http://localhost:4502/system/console/bundles/<bundle-name>
```

### Dispatcher {#dispatcher}

#### Invalidar o cache {#invalidate-the-cache}

```shell
curl -H "CQ-Action: Activate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

#### Remover o cache {#evict-the-cache}

```shell
curl -H "CQ-Action: Deactivate" -H "CQ-Handle: /content/test-site/" -H "CQ-Path: /content/test-site/" -H "Content-Length: 0" -H "Content-Type: application/octet-stream" http://localhost:4502/dispatcher/invalidate.cache
```

### Agente de replicação {#replication-agent}

#### Verificar o status de um agente {#check-the-status-of-an-agent}

```shell
curl -u <user>:<password> "http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish"
http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json?agent=publish
```

#### Excluir um agente {#delete-an-agent}

```shell
curl -X DELETE http://localhost:4502/etc/replication/agents.author/replication99 -u <user>:<password>
```

#### Criar um agente {#create-an-agent}

```shell
curl -u <user>:<password> -F "jcr:primaryType=cq:Page" -F "jcr:content/jcr:title=new-replication" -F "jcr:content/sling:resourceType=/libs/cq/replication/components/agent" -F "jcr:content/template=/libs/cq/replication/templates/agent" -F "jcr:content/transportUri=http://localhost:4503/bin/receive?sling:authRequestLogin=1" -F "jcr:content/transportUser=admin" -F "jcr:content/transportPassword={DES}8aadb625ced91ac483390ebc10640cdf"http://localhost:4502/etc/replication/agents.author/replication99
```

#### Pausar um agente {#pause-an-agent}

```shell
curl -u <user>:<password> -F "cmd=pause" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

#### Limpar uma fila de agente {#clear-an-agent-queue}

```shell
curl -u <user>:<password> -F "cmd=clear" -F "name=publish"  http://localhost:4502/etc/replication/agents.author/publish/jcr:content.queue.json
```

### Communities {#communities}

#### Atribuir e revogar selos {#assign-and-revoke-badges}

Consulte [Pontuação e medalhas das comunidades](/help/communities/implementing-scoring.md#assign-and-revoke-badges) para obter detalhes.

Consulte [Fundamentos de pontuação e medalhas](/help/communities/configure-scoring.md#example-setup) para obter detalhes.

#### Reindexação MSRP {#msrp-reindexing}

Consulte [MSRP - Provedor de Recurso de Armazenamento MongoDB](/help/communities/msrp.md#running-msrp-reindex-tool-using-curl-command) para obter detalhes.

### Segurança {#security}

#### Ativando e desativando o CRX DE Lite {#enabling-and-disabling-crx-de-lite}

Consulte [CRXDE Lite no AEM](/help/sites-administering/enabling-crxde-lite.md) para obter detalhes.

### Coleta de lixo do armazenamento de dados {#data-store-garbage-collection}

Consulte [Coleta de lixo do armazenamento de dados](/help/sites-administering/data-store-garbage-collection.md#automating-data-store-garbage-collection) para obter detalhes.

### Integração do Analytics e do Target {#analytics-and-target-integration}

Consulte [Ativação do Adobe Analytics e do Adobe Target](/help/sites-administering/opt-in.md#configuring-the-setup-and-provisioning-via-script) para obter detalhes.

### Logon único {#single-sign-on}

#### Enviar cabeçalho de teste {#send-test-header}

Consulte [Logon único](/help/sites-deploying/single-sign-on.md) para obter detalhes.

## Comandos cURL do AEM para manipulação de conteúdo comum {#common-content-manipulation-aem-curl-commands}

Aqui está uma lista de comandos AEM cURL para manipulação de conteúdo.

>[!NOTE]
>
>Os exemplos a seguir pressupõem que o AEM esteja em execução `localhost` na porta `4502` e usa o usuário `admin` com senha `admin`. Espaços reservados para comandos adicionais são definidos entre colchetes.

### Gerenciamento de página {#page-management}

#### Ativação de página {#page-activation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="activate" http://localhost:4502/bin/replicate.json
```

#### Desativação de página {#page-deactivation}

```shell
curl -u <user>:<password> -X POST -F path="/content/path/to/page" -F cmd="deactivate" http://localhost:4502/bin/replicate.json
```

#### Ativação em árvore {#tree-activation}

```shell
curl -u <user>:<password> -F cmd=activate -F ignoredeactivated=true -F onlymodified=true -F path=/content/geometrixx http://localhost:4502/etc/replication/treeactivation.html
```

#### Bloquear página {#lock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="lockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Desbloquear Página {#unlock-page}

```shell
curl -u <user>:<password> -X POST -F cmd="unlockPage" -F path="/content/path/to/page" -F "_charset_"="utf-8" http://localhost:4502/bin/wcmcommand
```

#### Página de cópia {#copy-page}

```shell
curl -u <user>:<password> -F cmd=copyPage -F destParentPath=/path/to/destination/parent -F srcPath=/path/to/source/location http://localhost:4502/bin/wcmcommand
```

### Fluxos de trabalhos {#workflows}

Consulte [Interação programática com fluxos de trabalho](/help/sites-developing/workflows-program-interaction.md) para obter detalhes.

### Conteúdo do Sling {#sling-content}

#### Criar uma pasta {#create-a-folder}

```shell
curl -u <user>:<password> -F jcr:primaryType=sling:Folder http://localhost:4502/etc/test
```

#### Excluir um nó {#delete-a-node}

```shell
curl -u <user>:<password> -F :operation=delete http://localhost:4502/etc/test/test.properties
```

#### Mover um nó {#move-a-node}

```shell
curl -u <user>:<password> -F":operation=move" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Copiar um nó {#copy-a-node}

```shell
curl -u <user>:<password> -F":operation=copy" -F":applyTo=/sourceurl"  -F":dest=/target/parenturl/" https://localhost:4502/content
```

#### Fazer upload de arquivos usando o Sling PostServlet {#upload-files-using-sling-postservlet}

```shell
curl -u <user>:<password> -F"*=@test.properties"  http://localhost:4502/etc/test
```

#### Fazer upload de arquivos usando o Sling PostServlet e especificando o nome do nó {#upload-files-using-sling-postservlet-and-specifying-node-name}

```shell
curl -u <user>:<password> -F"test2.properties=@test.properties"  http://localhost:4502/etc/test
```

#### Fazer upload de arquivos especificando um tipo de conteúdo {#upload-files-specifying-a-content-type}

```shell
curl -u <user>:<password> -F "*=@test.properties;type=text/plain" http://localhost:4502/etc/test
```

### Manipulação de ativos {#asset-manipulation}

Consulte [API HTTP de ativos](/help/assets/mac-api-assets.md) para obter detalhes.
