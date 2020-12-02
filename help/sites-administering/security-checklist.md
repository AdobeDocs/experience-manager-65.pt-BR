---
title: Lista de verificação de segurança
seo-title: Lista de verificação de segurança
description: Saiba mais sobre as várias considerações de segurança ao configurar e implantar AEM.
seo-description: Saiba mais sobre as várias considerações de segurança ao configurar e implantar AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
translation-type: tm+mt
source-git-commit: 474fc122f557f32d34fddd9d35a113431f6ce491
workflow-type: tm+mt
source-wordcount: '2841'
ht-degree: 0%

---


# Lista de verificação de segurança {#security-checklist}

Esta seção trata de várias etapas que devem ser tomadas para garantir que sua instalação AEM esteja segura quando implantada. A lista de verificação deve ser aplicada de cima para baixo.

>[!NOTE]
>
>Informações adicionais [também estão disponíveis sobre as ameaças de segurança mais perigosas conforme publicadas pelo Open Aplicação web Security Project (OWASP)](https://www.owasp.org/index.php/OWASP_Top_Ten_Project).

>[!NOTE]
>
>Há algumas considerações de segurança adicionais [aplicáveis na fase de desenvolvimento.](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)

## Principais medidas de segurança {#main-security-measures}

### Executar AEM no modo Production Ready {#run-aem-in-production-ready-mode}

Para obter mais informações, consulte [Execução de AEM no modo de produção pronto](/help/sites-administering/production-ready.md).

### Habilitar HTTPS para segurança de camada de transporte {#enable-https-for-transport-layer-security}

Habilitar a camada de transporte HTTPS nas instâncias de autor e publicação é obrigatório para ter uma instância segura.

>[!NOTE]
>
>Consulte a seção [Ativando HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obter mais informações.

### Instalar Hotfixes de Segurança {#install-security-hotfixes}

Verifique se você instalou os hotfixes de segurança [mais recentes fornecidos por Adobe](https://helpx.adobe.com/br/experience-manager/kb/aem63-available-hotfixes.html).

### Alterar senhas padrão para contas de administração do console AEM e OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

O Adobe recomenda enfaticamente que, após a instalação, você altere a senha das contas [**AEM** `admin` privilegiadas](#changing-the-aem-admin-password) (em todas as instâncias).

Essas contas incluem:

* A conta AEM `admin`

   Depois de alterar a senha da conta de administrador AEM, você precisará usar a nova senha ao acessar o CRX.

* A senha `admin` para o console Web OSGi

   Essa alteração também será aplicada à conta de administrador usada para acessar o console da Web, portanto, você precisará usar a mesma senha ao acessar essa conta.

Essas duas contas usam credenciais separadas e ter uma senha forte e distinta para cada uma é vital para uma implantação segura.

#### Alteração da senha do administrador AEM {#changing-the-aem-admin-password}

A senha da conta de administrador AEM pode ser alterada pelo console [Operações Granite - Usuários](/help/sites-administering/granite-user-group-admin.md).

Aqui você pode editar a conta `admin` e [alterar a senha](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Alterar a conta do administrador também altera a conta do console da Web OSGi. Depois de alterar a conta de administrador, você deve alterar a conta OSGi para algo diferente.

#### Importância de alterar a senha do console da Web OSGi {#importance-of-changing-the-osgi-web-console-password}

Além da conta AEM `admin`, a falha ao alterar a senha padrão para a senha do console da Web OSGi pode levar a:

* Exposição do servidor com uma senha padrão durante a inicialização e o encerramento (que pode levar minutos para grandes servidores);
* Exposição do servidor quando o repositório está inativo/reiniciando o pacote - e o OSGI está em execução.

Para obter mais informações sobre como alterar a senha do console da Web, consulte [Alteração da senha de administrador do console da Web do OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) abaixo.

#### Alteração da senha de administrador do console da Web OSGi {#changing-the-osgi-web-console-admin-password}

Você também deve alterar a senha usada para acessar o console da Web. Isso é feito configurando as seguintes propriedades do [Console de gerenciamento do Apache Felix OSGi](/help/sites-deploying/osgi-configuration-settings.md):

**Nome** de usuário e  **senha**, as credenciais para acessar o Console de gerenciamento da Web do Apache Felix.
A senha deve ser alterada após a instalação inicial para garantir a segurança da sua instância.

Para fazer isso:

1. Navegue até o console da Web em `<server>:<port>/system/console/configMgr`.
1. Navegue até **Apache Felix OSGi Management Console** e altere **nome de usuário** e **senha**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Clique em **Salvar**.

### Implementar o Manipulador de Erros Personalizado {#implement-custom-error-handler}

O Adobe recomenda definir páginas personalizadas do manipulador de erros, especialmente para os códigos de resposta 404 e 500 HTTP, a fim de impedir a divulgação de informações.

>[!NOTE]
>
>Consulte [Como posso criar scripts personalizados ou manipuladores de erros](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) artigo da base de conhecimento para obter mais detalhes.

### Lista de verificação completa de segurança do Dispatcher {#complete-dispatcher-security-checklist}

AEM o Dispatcher é uma peça essencial da sua infraestrutura. É altamente recomendável que você conclua a lista de verificação de segurança [dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/security-checklist.html).

>[!CAUTION]
>
>Usando o Dispatcher, você deve desativar o seletor &quot;.form&quot;.

## Etapas de verificação {#verification-steps}

### Configurar usuários de replicação e transporte {#configure-replication-and-transport-users}

Uma instalação padrão de AEM especifica `admin` como o usuário para credenciais de transporte dentro dos [agentes de replicação](/help/sites-deploying/replication.md) padrão. Além disso, o usuário administrador é usado para gerar a replicação no sistema do autor.

Por razões de segurança, ambas devem ser alteradas de modo a refletir o caso de utilização específico em causa, tendo em conta os dois aspectos seguintes:

* O **usuário de transporte** não deve ser o usuário administrador. Em vez disso, configure um usuário no sistema de publicação que tenha somente direitos de acesso às partes relevantes do sistema de publicação e use as credenciais desse usuário para o transporte.

   Você pode start do usuário receptor de replicação agrupado e configurar os direitos de acesso desse usuário para corresponder à sua situação

* O **usuário de replicação** ou **ID de usuário do agente** também não deve ser o usuário administrador, mas um usuário que só pode ver o conteúdo que deve ser replicado. O usuário de replicação é usado para coletar o conteúdo a ser replicado no sistema do autor antes de ser enviado ao editor.

### Verifique as verificações de integridade de segurança do Operations Painel {#check-the-operations-dashboard-security-health-checks}

AEM 6 apresenta o novo Painel Operações, que tem como objetivo ajudar os operadores do sistema a solucionar problemas e monitorar a integridade de uma instância.

O painel também vem com uma coleção de verificações de segurança de saúde. É recomendável verificar o status de todas as verificações de integridade de segurança antes de entrar em operação com a instância de produção. Para obter mais informações, consulte a [documentação do Painel de Operações](/help/sites-administering/operations-dashboard.md).

### Verifique se o conteúdo de exemplo está presente {#check-if-example-content-is-present}

Todos os exemplos de conteúdo e usuários (por exemplo, o projeto do Geometrixx e seus componentes) devem ser desinstalados e excluídos completamente em um sistema produtivo antes de torná-lo acessível ao público.

>[!NOTE]
>
>A amostra de aplicativos We.Retail será removida se essa instância estiver sendo executada no [Modo Pronto para Produção](/help/sites-administering/production-ready.md). Se, por qualquer motivo, esse não for o caso, você poderá desinstalar o conteúdo de amostra indo para o Gerenciador de pacotes e, em seguida, pesquisando e desinstalando todos os pacotes We.Retail. Para obter mais informações, consulte [Trabalhar com pacotes](package-manager.md).

### Verifique se os pacotes de desenvolvimento do CRX estão presentes {#check-if-the-crx-development-bundles-are-present}

Esses pacotes OSGi de desenvolvimento devem ser desinstalados nos sistemas de produção do autor e publicação antes de torná-los acessíveis.

* Suporte a Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Verifique se o pacote de desenvolvimento Sling está presente {#check-if-the-sling-development-bundle-is-present}

As [Ferramentas do desenvolvedor AEM para Eclipse](/help/sites-developing/aem-eclipse.md) implementam a Instalação do suporte à ferramenta Apache Sling (org.apache.sling.tooling.support.install).

Esse pacote OSGi deve ser desinstalado no autor e publicar sistemas produtivos antes de torná-los acessíveis.

### Protect contra falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery}

#### A estrutura de proteção do CSRF {#the-csrf-protection-framework}

AEM 6.1 é fornecido com um mecanismo que ajuda a proteger contra ataques de falsificação de solicitação entre sites, chamado **CSRF Protection Framework**. Para obter mais informações sobre como usá-lo, consulte a [documentação](/help/sites-developing/csrf-protection.md).

#### O Filtro de Quem indicou Sling {#the-sling-referrer-filter}

Para resolver problemas de segurança conhecidos com o CSRF (Cross-Site Request Forgery) no CRX WebDAV e no Apache Sling, é necessário adicionar configurações para o filtro de Quem indicou para usá-lo.

O serviço de filtro de quem indicou é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de quem indicou vazio é permitido
* e uma lista de servidores a ser permitida além do host do servidor.

   Por padrão, todas as variações de localhost e os nomes de host atuais aos quais o servidor está vinculado estão na lista.

Para configurar o serviço de filtro de quem indicou:

1. Abra o console do Apache Felix (**Configurações**) em:

   `https://<server>:<port_number>/system/console/configMgr`

1. Faça logon como `admin`.
1. No menu **Configurações**, selecione:

   `Apache Sling Referrer Filter`

1. No campo `Allow Hosts`, insira todos os hosts permitidos como uma quem indicou. Cada entrada precisa ser do formulário

   &lt;protocol>://&lt;server>:&lt;port>

   Por exemplo:

   * `https://allowed.server:80` permite todas as solicitações deste servidor com a porta especificada.
   * Se você também quiser permitir solicitações https, é necessário inserir uma segunda linha.
   * Se você permitir todas as portas desse servidor, poderá usar `0` como o número da porta.

1. Marque o campo `Allow Empty`, se desejar permitir cabeçalhos de quem indicou vazios/ausentes.

   >[!CAUTION]
   >
   >É recomendável fornecer uma quem indicou ao usar ferramentas de linha de comando, como `cURL`, em vez de permitir um valor vazio, pois isso pode expor seu sistema a ataques de CSRF.

1. Edite os métodos que este filtro deve usar para verificações com o campo `Filter Methods`.

1. Clique em **Salvar** para salvar as alterações.

### Configurações de OSGI {#osgi-settings}

Algumas configurações de OSGI são definidas por padrão para permitir uma depuração mais fácil do aplicativo. Eles precisam ser alterados em suas instâncias produtivas de publicação e criação para evitar que informações internas vazem para o público.

>[!NOTE]
>
>Todas as configurações abaixo, com exceção de **O Filtro de Depuração do Day CQ WCM** são automaticamente cobertas pelo [Modo Pronto para Produção](/help/sites-administering/production-ready.md). Por isso, recomendamos a revisão de todas as configurações antes de implantar sua instância em um ambiente produtivo.

Para cada um dos seguintes serviços, as configurações especificadas precisam ser alteradas:

* [Gerenciador](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager) de biblioteca HTML do Adobe Granite:

   * habilite **Minify** (para remover caracteres CRLF e de espaço em branco).
   * habilite **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * desativar **Depurar**
   * desabilitar **Tempo**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) de Depuração do WCM do Day CQ:

   * desmarque **Ativar**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md) WCM CQ Dia:

   * apenas para publicação, defina **Modo WCM** como &quot;desativado&quot;

* [Manipulador](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler) Apache Sling Java Script:

   * desabilitar **Gerar Informações de Depuração**

* [Manipulador](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler) De Script JSP Do Apache Sling:

   * desabilitar **Gerar Informações de Depuração**
   * desabilitar **Conteúdo mapeado**

Para obter mais detalhes, consulte [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Ao trabalhar com AEM existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Leituras Adicionais {#further-readings}

### Atenuar ataques de negação de serviço (DoS) {#mitigate-denial-of-service-dos-attacks}

Um ataque de negação de serviço (DoS) é uma tentativa de tornar um recurso de computador indisponível para os usuários pretendidos. Isso é feito com frequência sobrecarregando o recurso; por exemplo:

* Com uma inundação de solicitações de uma fonte externa.
* Com uma solicitação para obter mais informações do que o sistema pode fornecer com êxito.

   Por exemplo, uma representação JSON de todo o repositório.

* Ao solicitar uma página de conteúdo com um número ilimitado de URLs, o URL pode incluir um identificador, alguns seletores, uma extensão e um sufixo - qualquer um dos quais pode ser modificado.

   Por exemplo, `.../en.html` também pode ser solicitado como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas as variações válidas (por exemplo, retornar uma resposta `200` e estiverem configuradas para serem armazenadas em cache) serão armazenadas em cache pelo dispatcher, resultando em um sistema de arquivos completo e nenhum serviço para solicitações adicionais.

Há muitos pontos de configuração para evitar tais ataques, aqui apenas discutimos os diretamente relacionados com a AEM.

**Configuração do Sling para impedir DoS**

O Sling é *centrado no conteúdo*. Isso significa que o processamento está focado no conteúdo, já que cada solicitação (HTTP) está mapeada para o conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro público alvo é o recurso (nó JCR) que contém o conteúdo.
* Em segundo lugar, o renderizador, ou script, está localizado nas propriedades do recurso em combinação com determinadas partes da solicitação (por exemplo, seletores e/ou extensão).

>[!NOTE]
>
>Isso é abordado com mais detalhes em [Processamento de solicitação Sling](/help/sites-developing/the-basics.md#sling-request-processing).

Esta abordagem torna o Sling muito poderoso e flexível, mas, como sempre, é a flexibilidade que precisa ser cuidadosamente gerenciada.

Para ajudar a impedir o uso indevido de DoS, você pode:

1. Incorporar controlos ao nível da aplicação; devido ao número de variações possíveis, uma configuração padrão não é viável.

   Em seu aplicativo, você deve:

   * Controle os seletores em seu aplicativo, para que você *only* sirva os seletores explícitos necessários e retorne `404` para todos os outros.
   * Impedir a saída de um número ilimitado de nós de conteúdo.

1. Verifique a configuração dos renderizadores padrão, que podem ser uma área problemática.

   * Em particular, o renderizador JSON que pode transverter a estrutura em árvore em vários níveis.

      Por exemplo, a solicitação:

      `http://localhost:4502/.json`

      poderia descarregar todo o repositório em uma representação JSON. Isso causaria problemas significativos no servidor. Por esse motivo, o Sling define um limite para o número máximo de resultados. Para limitar a profundidade da renderização JSON, é possível definir o valor para:

      **Resultados**  máx. JSON(  `json.maximumresults`)

      na configuração para o [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando esse limite for excedido, a renderização será recolhida. O valor padrão para Sling em AEM é `200`.

   * Como medida preventiva, desative os outros renderizadores padrão (HTML, texto sem formatação, XML). Novamente ao configurar o [Servlet de GET Sling do Apache](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Não desative o renderizador JSON, isso é necessário para a operação normal do AEM.

1. Use um firewall para filtrar o acesso à sua instância.

   * O uso de um firewall de nível de sistema operacional é necessário para filtrar o acesso a pontos de sua instância que podem levar a ataques de negação de serviço se deixados desprotegidos.

**Mitigar contra DoS causado pelo uso de seletores de formulário**

>[!NOTE]
>
>Essa mitigação deve ser realizada somente em ambientes AEM que não estejam usando o Forms.

Como o AEM não fornece índices prontos para o `FormChooserServlet`, usar seletores de formulário em query acionará uma dispendiosa travessia do repositório, geralmente paralisando a instância AEM. Os seletores de formulário podem ser detectados pela presença do **&amp;ast;.form.&amp;ast;** cadeia em query.

Para atenuar isso, siga as etapas abaixo:

1. Vá para o Console da Web apontando seu navegador para *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Procurar **Servlet do Seletor de Formulários do Day CQ WCM**
1. Depois de clicar na entrada, desative o **Pedido de pesquisa avançada** na seguinte janela.

1. Clique em **Salvar**.

**Mitigar contra DoS causado pelo Servlet de download de ativos**

O Servlet de download de ativos padrão no AEM permite que usuários autenticados emitam solicitações de download simultâneas e arbitrariamente grandes para criar arquivos ZIP de ativos visíveis para eles que podem sobrecarregar o servidor e/ou a rede.

Para atenuar os possíveis riscos de DoS causados por esse recurso, `AssetDownloadServlet` o componente OSGi está desabilitado por padrão para instâncias de publicação em versões mais recentes de AEM.

Se a configuração exigir que o Servidor de download de ativos esteja ativado, consulte [este artigo](/help/assets/download-assets-from-aem.md) para obter mais informações.

### Desativar WebDAV {#disable-webdav}

O WebDAV deve ser desativado nos ambientes de autor e publicação. Isso pode ser feito parando os pacotes OSGi apropriados.

1. Conecte-se ao **Console de gerenciamento Felix** em execução em:

   `https://<*host*>:<*port*>/system/console`

   Por exemplo `http://localhost:4503/system/console/bundles`.

1. Na lista dos pacotes, localize o conjunto chamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Clique no botão Parar (na coluna Ações) para parar este pacote.

1. Novamente na lista de pacotes, encontre o pacote chamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Clique no botão Parar para parar este pacote.

   >[!NOTE]
   >
   >Não é necessário reiniciar o AEM.

### Verifique se você não está exibindo informações pessoais identificáveis no Caminho inicial do usuário {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

É importante que você proteja seus usuários, certificando-se de não expor nenhuma informação pessoalmente identificável no caminho inicial dos usuários do repositório.

Desde AEM 6.1, a maneira como os nomes de nó de ID do usuário (também conhecidos como autorizados) são armazenados é alterada com uma nova implementação da interface `AuthorizableNodeName`. A nova interface não exporá mais a ID do usuário no nome do nó, mas gerará um nome aleatório.

Nenhuma configuração precisa ser executada para habilitá-la, já que essa é a forma padrão de gerar IDs autorizados no AEM.

Embora não seja recomendado, você pode desativá-lo caso precise da implementação antiga para ter compatibilidade com seus aplicativos existentes. Para fazer isso, é necessário:

1. Vá para o Console da Web e remova a entrada** org.apache.Jackrabbit.oak.security.user.RandomAuthorizableNodeName** da propriedade **requiredServicePids** em **Apache Jackrabbit Oak SecurityProvider**.

   Você também pode encontrar o Provedor de segurança Oak procurando pelo PID **org.apache.Jackrabbit.oak.security.internal.SecurityProviderRegistration** nas configurações do OSGi.

1. Exclua a configuração **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi do console da Web.

   Para facilitar a pesquisa, observe que o PID desta configuração é **org.apache.Jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obter mais informações, consulte a documentação do Oak em [Geração de Nome de Nó Autorizável](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Impedir que os cliques sejam ativados {#prevent-clickjacking}

Para evitar o clickjacking, recomendamos que você configure seu servidor Web para fornecer o cabeçalho HTTP `X-FRAME-OPTIONS` definido como `SAMEORIGIN`.

Para obter mais [informações sobre clickjacking, consulte o site da OWASP](https://www.owasp.org/index.php/Clickjacking).

### Certifique-se de replicar corretamente as chaves de criptografia quando necessário {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Determinados recursos AEM e esquemas de autenticação exigem que você replique suas chaves de criptografia em todas as instâncias AEM.

Antes de fazer isso, observe que a replicação principal é feita de forma diferente entre as versões, pois a maneira como as chaves são armazenadas é diferente entre as versões 6.3 e anteriores.

Consulte abaixo para obter mais informações.

#### Replicação de chaves para AEM 6.3 {#replicating-keys-for-aem}

Enquanto em versões mais antigas as chaves de replicação eram armazenadas no repositório, a partir da AEM 6.3, elas são armazenadas no sistema de arquivos.

Portanto, para replicar suas chaves em instâncias, é necessário copiá-las da instância de origem para o local das instâncias de público alvo no sistema de arquivos.

Mais especificamente, você precisa:

1. Acesse a instância AEM, normalmente uma instância do autor, que contém o material principal a ser copiado;
1. Localize o pacote com.adobe.granite.crypto.file no sistema de arquivos local. Por exemplo, neste caminho:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   O arquivo `bundle.info` dentro de cada pasta identificará o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie os arquivos HMAC e principais.
1. Em seguida, vá para a instância do público alvo para a qual deseja duplicado a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualize o ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) pacote Crypto se a instância do público alvo já estiver em execução.
1. Repita as etapas acima para todas as instâncias às quais deseja replicar a chave.

>[!NOTE]
>
>Você pode reverter para o método pre 6.3 de armazenamento de chaves adicionando o parâmetro abaixo ao instalar o AEM pela primeira vez:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replicação de chaves para AEM 6.2 e versões anteriores {#replicating-keys-for-aem-and-older-versions}

Em AEM 6.2 e versões anteriores, as chaves são armazenadas no repositório no nó `/etc/key`.

A maneira recomendada de replicar com segurança as chaves em todas as instâncias é apenas replicar esse nó. É possível replicar nós seletivamente por meio do CRXDE Lite:

1. Abra o CRXDE Lite indo para *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Selecione o nó `/etc/key`.
1. Vá para a guia **Replicação**.
1. Pressione o botão **Replication**.

### Execute um teste de penetração {#perform-a-penetration-test}

A Adobe recomenda que você realize um teste de penetração de sua infraestrutura AEM antes de entrar na produção.

### Práticas recomendadas de desenvolvimento {#development-best-practices}

É importante que o novo desenvolvimento siga as [Práticas recomendadas de segurança](/help/sites-developing/security.md) para garantir que seu ambiente AEM permaneça seguro.
