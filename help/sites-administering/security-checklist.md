---
title: Lista de verificação de segurança
seo-title: Security Checklist
description: Saiba mais sobre as várias considerações de segurança ao configurar e implantar AEM.
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: f60d3049b10a8ec500dd0cd4b1b5d4efbe415d84
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 3%

---

# Lista de verificação de segurança {#security-checklist}

Esta seção trata de várias etapas que você deve tomar para garantir que sua instalação AEM seja segura quando implantada. A lista de verificação deve ser aplicada de cima para baixo.

>[!NOTE]
>
>Informações adicionais também estão disponíveis sobre as ameaças de segurança mais perigosas, conforme publicado pelo [Open Web Application Security Project (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Há algumas considerações adicionais [de segurança](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aplicáveis na fase de desenvolvimento.

## Principais medidas de segurança {#main-security-measures}

### Executar AEM no modo Pronto para produção {#run-aem-in-production-ready-mode}

Para obter mais informações, consulte [Execução de AEM no Modo de Pronto para Produção](/help/sites-administering/production-ready.md).

### Ativar HTTPS para segurança da camada de transporte {#enable-https-for-transport-layer-security}

Habilitar a camada de transporte HTTPS nas instâncias de autor e publicação é obrigatório para ter uma instância segura.

>[!NOTE]
>
>Consulte a seção [Ativando HTTP sobre SSL](/help/sites-administering/ssl-by-default.md) para obter mais informações.

### Instalar hotfixes de segurança {#install-security-hotfixes}

Certifique-se de ter instalado os [Hotfixes de segurança mais recentes fornecidos pelo Adobe](https://helpx.adobe.com/br/experience-manager/kb/aem63-available-hotfixes.html).

### Alterar senhas padrão para contas de administração do console AEM e OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

O Adobe recomenda que, após a instalação, você altere a senha das contas privilegiadas [**AEM** `admin`](#changing-the-aem-admin-password) (em todas as instâncias).

Essas contas incluem:

* A conta AEM `admin`

   Depois de alterar a senha da conta de administrador AEM, será necessário usar a nova senha ao acessar o CRX.

* A senha `admin` do console OSGi da Web

   Essa alteração também será aplicada à conta de administrador usada para acessar o console da Web; portanto, você precisará usar a mesma senha ao acessar essa senha.

Essas duas contas usam credenciais separadas e ter uma senha forte e distinta para cada é essencial para uma implantação segura.

#### Alterar a senha do administrador AEM {#changing-the-aem-admin-password}

A senha da conta de administrador AEM pode ser alterada por meio do console [Granite Operations - Users](/help/sites-administering/granite-user-group-admin.md).

Aqui você pode editar a conta `admin` e [alterar a senha](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Alterar a conta de administrador também altera a conta do console da Web OSGi. Depois de alterar a conta de administrador, você deve alterar a conta OSGi para algo diferente.

#### Importância de alterar a senha do console da Web OSGi {#importance-of-changing-the-osgi-web-console-password}

Além da conta AEM `admin`, a falha na alteração da senha padrão do console da Web OSGi pode levar a:

* Exposição do servidor com uma senha padrão durante a inicialização e o desligamento (que pode levar minutos para grandes servidores);
* Exposição do servidor quando o repositório está inativo/reiniciando o pacote - e OSGI está em execução.

Para obter mais informações sobre como alterar a senha do console da Web, consulte [Alteração da senha do administrador do console da Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) abaixo.

#### Alteração da senha do administrador do console da Web OSGi {#changing-the-osgi-web-console-admin-password}

Você também deve alterar a senha usada para acessar o console da Web. Isso é feito configurando as seguintes propriedades do [Console de Gerenciamento OSGi do Apache Felix](/help/sites-deploying/osgi-configuration-settings.md):

**Nome** de usuário e  **senha**, as credenciais para acessar o próprio Apache Felix Web Management Console.
A senha deve ser alterada após a instalação inicial para garantir a segurança da sua instância.

Para fazer isso:

1. Navegue até o console da Web em `<server>:<port>/system/console/configMgr`.
1. Navegue até **Apache Felix OSGi Management Console** e altere o **nome de usuário** e **senha**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Clique em **Salvar**.

### Implementar o Manipulador de Erros Personalizado {#implement-custom-error-handler}

O Adobe recomenda definir páginas personalizadas do manipulador de erros, especialmente para os códigos de resposta HTTP 404 e 500, a fim de evitar a divulgação de informações.

>[!NOTE]
>
>Consulte [Como posso criar scripts personalizados ou manipuladores de erro](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) artigo da base de conhecimento para obter mais detalhes.

### Lista de verificação de segurança completa do Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher é uma parte essencial de sua infraestrutura. Adobe é altamente recomendável concluir a [lista de verificação de segurança do dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=pt-BR#getting-started).

>[!CAUTION]
>
>Usando o Dispatcher, você deve desativar o seletor &quot;.form&quot;.

## Etapas de verificação {#verification-steps}

### Configurar usuários de replicação e transporte {#configure-replication-and-transport-users}

Uma instalação padrão de AEM especifica `admin` como usuário para credenciais de transporte no [agentes de replicação](/help/sites-deploying/replication.md) padrão. Além disso, o usuário administrador é usado para originar a replicação no sistema de criação.

Por questões de segurança, ambas devem ser alteradas de forma a refletirem o caso de uso específico em questão, tendo em conta os dois aspectos seguintes:

* O **usuário de transporte** não deve ser o usuário administrador. Em vez disso, configure um usuário no sistema de publicação que tenha somente direitos de acesso às partes relevantes do sistema de publicação e use as credenciais desse usuário para o transporte.

   Você pode começar com o usuário receptor de replicação empacotado e configurar os direitos de acesso deste usuário para corresponder à sua situação

* O **usuário de replicação** ou **Agent User Id** também não deve ser o usuário administrador, mas um usuário que só pode ver o conteúdo que deve ser replicado. O usuário de replicação é usado para coletar o conteúdo a ser replicado no sistema de autor antes de ser enviado ao editor.

### Verifique as verificações de integridade de segurança do painel de operações {#check-the-operations-dashboard-security-health-checks}

O AEM 6 apresenta o novo Painel de Operações, destinado a ajudar os operadores do sistema a solucionar problemas e monitorar a integridade de uma instância.

O painel também vem com uma coleção de verificações de integridade de segurança. É recomendável verificar o status de todas as verificações de integridade de segurança antes de entrar em vigor com a instância de produção. Para obter mais informações, consulte a [documentação do Painel de Operações](/help/sites-administering/operations-dashboard.md).

### Verifique se o conteúdo de exemplo está presente {#check-if-example-content-is-present}

Todo o conteúdo de exemplo e os usuários (por exemplo, o projeto do Geometrixx e seus componentes) devem ser desinstalados e excluídos completamente em um sistema produtivo antes de torná-lo acessível ao público.

>[!NOTE]
>
>As amostras de aplicativos We.Retail são removidas se esta instância estiver em execução em [Modo de Pronto para Produção](/help/sites-administering/production-ready.md). Se, por qualquer motivo, esse não for o caso, é possível desinstalar o conteúdo de amostra acessando o Gerenciador de pacotes e, em seguida, procurando e desinstalando todos os pacotes We.Retail. Para obter mais informações, consulte [Trabalhar com pacotes](package-manager.md).

### Verifique se os pacotes de desenvolvimento do CRX estão presentes {#check-if-the-crx-development-bundles-are-present}

Esses pacotes OSGi de desenvolvimento devem ser desinstalados nos sistemas produtivos de criação e publicação antes de torná-los acessíveis.

* Suporte a Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Verifique se o pacote de desenvolvimento do Sling está presente {#check-if-the-sling-development-bundle-is-present}

As [Ferramentas do Desenvolvedor AEM para Eclipse](/help/sites-developing/aem-eclipse.md) implantam a instalação do suporte de ferramentas do Apache Sling (org.apache.sling.tooling.support.install).

Este pacote OSGi deve ser desinstalado nos sistemas produtivos de autor e publicação antes de torná-los acessíveis.

### Protect contra falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery}

#### Quadro de proteção do QREF {#the-csrf-protection-framework}

O AEM 6.1 vem com um mecanismo que ajuda a proteger contra ataques de falsificação de solicitação entre sites, chamado de **CSRF Protection Framework**. Para obter mais informações sobre como usá-lo, consulte a [documentação](/help/sites-developing/csrf-protection.md).

#### O filtro do referenciador do Sling {#the-sling-referrer-filter}

Para solucionar problemas de segurança conhecidos com a falsificação de solicitação entre sites (CSRF) no CRX WebDAV e no Apache Sling, é necessário adicionar configurações para o filtro Referenciador para usá-lo.

O serviço de filtro do referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores a serem permitidos além do host do servidor.

   Por padrão, todas as variações de localhost e os nomes de host atuais aos quais o servidor está vinculado estão na lista.

Para configurar o serviço de filtro do referenciador:

1. Abra o console do Apache Felix (**Configurations**) em:

   `https://<server>:<port_number>/system/console/configMgr`

1. Faça logon como `admin`.
1. No menu **Configurações**, selecione:

   `Apache Sling Referrer Filter`

1. No campo `Allow Hosts` , insira todos os hosts permitidos como referenciador. Cada entrada precisa estar no formulário

   &lt;protocol>://&lt;server>:&lt;port>

   Por exemplo:

   * `https://allowed.server:80` permite todas as solicitações deste servidor com a porta especificada.
   * Se também quiser permitir solicitações https, é necessário inserir uma segunda linha.
   * Se você permitir todas as portas desse servidor, poderá usar `0` como o número da porta.

1. Marque o campo `Allow Empty` , se desejar permitir cabeçalhos de referenciador vazios/ausentes.

   >[!CAUTION]
   >
   >É recomendável fornecer um referenciador ao usar ferramentas de linha de comando, como `cURL`, em vez de permitir um valor vazio, pois pode expor seu sistema a ataques de CSRF.

1. Edite os métodos que esse filtro deve usar para verificações com o campo `Filter Methods`.

1. Clique em **Salvar** para salvar as alterações.

### Configurações OSGI {#osgi-settings}

Algumas configurações OSGI são definidas por padrão para permitir uma depuração mais fácil do aplicativo. Eles precisam ser alterados em instâncias produtivas de publicação e criação para evitar o vazamento de informações internas para o público.

>[!NOTE]
>
>Todas as configurações abaixo, com exceção de **The Day CQ WCM Debug Filter**, são automaticamente cobertas pelo [Production Ready Mode](/help/sites-administering/production-ready.md). Por causa disso, recomendamos revisar todas as configurações antes de implantar sua instância em um ambiente produtivo.

Para cada um dos seguintes serviços, as configurações especificadas precisam ser alteradas:

* [Gerenciador](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager) da biblioteca HTML do Adobe Granite:

   * habilite **Minify** (para remover caracteres CRLF e espaço em branco).
   * habilite **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * desativar **Depurar**
   * desativar **Tempo**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter) de depuração do WCM CQ do dia:

   * desmarque **Ativar**

* [Filtro](/help/sites-deploying/osgi-configuration-settings.md) Day CQ WCM:

   * somente ao publicar, defina **Modo WCM** como &quot;desabilitado&quot;

* [Manipulador](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler) de script Java do Apache Sling:

   * desativar **Gerar Informações de Depuração**

* [Manipulador](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler) de script JSP do Apache Sling:

   * desativar **Gerar Informações de Depuração**
   * desativar **Conteúdo Mapeado**

Para obter mais detalhes, consulte [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Outras Leituras {#further-readings}

### Reduza os ataques de negação de serviço (DoS) {#mitigate-denial-of-service-dos-attacks}

Um ataque de negação de serviço (DoS) é uma tentativa de tornar um recurso de computador indisponível para os usuários desejados. Isso é feito com frequência sobrecarregando o recurso; por exemplo:

* Com uma enxurrada de solicitações de uma fonte externa.
* Com uma solicitação para obter mais informações do que o sistema pode fornecer com sucesso.

   Por exemplo, uma representação JSON de todo o repositório.

* Ao solicitar uma página de conteúdo com um número ilimitado de URLs, o URL pode incluir um identificador, alguns seletores, uma extensão e um sufixo, qualquer um dos quais pode ser modificado.

   Por exemplo, `.../en.html` também pode ser solicitado como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas as variações válidas (por exemplo, retornar uma resposta `200` e são configuradas para serem armazenadas em cache) serão armazenadas em cache pelo dispatcher, resultando em um sistema de arquivos completo e nenhum serviço para solicitações adicionais.

Há muitos pontos de configuração para prevenir tais ataques, aqui só discutimos aqueles diretamente relacionados com a AEM.

**Configurar o Sling para evitar DoS**

O Sling é *centrado no conteúdo*. Isso significa que o processamento está focado no conteúdo, já que cada solicitação (HTTP) é mapeada no conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro target é o recurso (nó JCR) que contém o conteúdo.
* Em segundo lugar, o renderizador, ou script, está localizado nas propriedades do recurso em combinação com determinadas partes da solicitação (por exemplo, seletores e/ou extensão).

>[!NOTE]
>
>Isso é abordado com mais detalhes em [Processamento de solicitação do Sling](/help/sites-developing/the-basics.md#sling-request-processing).

Essa abordagem torna o Sling muito poderoso e flexível, mas, como sempre, é a flexibilidade que precisa ser gerenciada com cuidado.

Para ajudar a evitar o uso indevido de DoS, você pode:

1. Incorporar controlos ao nível da aplicação; devido ao número de variações possíveis, uma configuração padrão não é viável.

   No seu aplicativo, você deve:

   * Controle os seletores em seu aplicativo, para que *only* sirva os seletores explícitos necessários e retorne `404` para todos os outros.
   * Impeça a saída de um número ilimitado de nós de conteúdo.

1. Verifique a configuração dos renderizadores padrão, que pode ser uma área problemática.

   * Particularmente o renderizador JSON, que pode inverter a estrutura da árvore em vários níveis.

      Por exemplo, a solicitação:

      `http://localhost:4502/.json`

      pode despejar todo o repositório em uma representação JSON. Isso causaria problemas significativos no servidor. Por esse motivo, o Sling define um limite no número máximo de resultados. Para limitar a profundidade da renderização JSON, é possível definir o valor para:

      **Máximo de resultados JSON**  (  `json.maximumresults`)

      na configuração do [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando esse limite for excedido, a renderização será recolhida. O valor padrão para Sling em AEM é `1000`.

   * Como medida preventiva, desative os outros renderizadores padrão (HTML, texto sem formatação, XML). Novamente, configurando o [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Não desative o renderizador JSON, isso é necessário para a operação normal de AEM.

1. Use um firewall para filtrar o acesso à sua instância.

   * O uso de um firewall no nível do sistema operacional é necessário para filtrar o acesso a pontos da instância que podem levar a ataques de negação de serviço se não estiverem protegidos.

**Mitigar contra ações causadas pelo uso de seletores de formulário**

>[!NOTE]
>
>Essa atenuação deve ser executada somente em ambientes AEM que não estejam usando o Forms.

Como o AEM não fornece índices prontos para uso para o `FormChooserServlet`, usar seletores de formulário em consultas acionará uma dispendiosa travessia do repositório, normalmente travando a instância AEM. Os seletores de formulário podem ser detectados pela presença do **&amp;ast;.form.&amp;ast;** sequência em consultas.

Para mitigar isso, siga as etapas abaixo:

1. Vá para o Console da Web apontando seu navegador para *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Procure por **Day CQ WCM Form Chooser Servlet**
1. Depois de clicar na entrada, desative o **Advanced Search Require** na janela a seguir.

1. Clique em **Salvar**.

**Mitigar contra ações causadas pelo servlet de download de ativos**

O servlet de download de ativos padrão permite que usuários autenticados emitam solicitações de download simultâneas e arbitrariamente grandes para criar arquivos ZIP de ativos. Criar arquivos ZIP grandes pode sobrecarregar o servidor e a rede. Para mitigar um potencial risco de Negação de Serviço (DoS) causado por esse comportamento, `AssetDownloadServlet` o componente OSGi é desabilitado por padrão na instância de publicação [!DNL Experience Manager]. Está ativado na instância do autor [!DNL Experience Manager] por padrão.

Se você não precisar do recurso de download, desative o servlet nas implantações de criação e publicação. Se a configuração exigir que o recurso de download de ativos esteja ativado, consulte [este artigo](/help/assets/download-assets-from-aem.md) para obter mais informações. Além disso, é possível definir um limite máximo de download que sua implantação possa suportar.

### Desativar WebDAV {#disable-webdav}

O WebDAV deve ser desativado nos ambientes de autor e publicação. Isso pode ser feito parando os pacotes OSGi apropriados.

1. Conecte-se ao **Felix Management Console** em execução em:

   `https://<*host*>:<*port*>/system/console`

   Por exemplo `http://localhost:4503/system/console/bundles`.

1. Na lista de pacotes, encontre o pacote chamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Clique no botão stop (na coluna Actions ) para interromper esse pacote.

1. Novamente na lista de pacotes, encontre o pacote chamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Clique no botão stop para interromper esse pacote.

   >[!NOTE]
   >
   >Não é necessário reiniciar o AEM.

### Verifique Se Você Não Está Exibindo Informações Pessoalmente Identificáveis No Caminho Inicial Dos Usuários {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

É importante proteger seus usuários, certificando-se de não expor nenhuma informação pessoal identificável no caminho inicial dos usuários do repositório.

Desde o AEM 6.1, a maneira como os nomes de nó da ID do usuário (também conhecidos como autorizados) são armazenados é alterada com uma nova implementação da interface `AuthorizableNodeName`. A nova interface não exporá mais a ID do usuário no nome do nó, mas gerará um nome aleatório.

Nenhuma configuração precisa ser executada para habilitá-la, pois essa é agora a maneira padrão de gerar IDs autorizáveis no AEM.

Embora não seja recomendado, você pode desativá-lo caso precise da implementação antiga para ter compatibilidade com os aplicativos existentes. Para fazer isso, é necessário:

1. Vá para o Console da Web e remova a entrada ** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** da propriedade **requiredServicePids** em **Apache Jackrabbit Oak SecurityProvider**.

   Você também pode encontrar o Provedor de segurança do Oak procurando pelo PID **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** nas configurações do OSGi.

1. Exclua a configuração **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi do Console da Web.

   Para obter mais informações, observe que o PID dessa configuração é **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obter mais informações, consulte a documentação do Oak em [Geração de Nome de Nó Autorizável](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Prevenção contra clickjacking {#prevent-clickjacking}

Para evitar clickjacking, recomendamos que você configure seu servidor Web para fornecer o cabeçalho HTTP `X-FRAME-OPTIONS` definido como `SAMEORIGIN`.

Para obter mais [informações sobre clickjacking, consulte o site OWASP](https://www.owasp.org/index.php/Clickjacking).

### Certifique-Se De Replicar Corretamente As Chaves De Criptografia Quando Necessário {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Determinados recursos de AEM e esquemas de autenticação exigem a replicação das chaves de criptografia em todas as instâncias de AEM.

Antes de fazer isso, observe que a replicação de chaves é feita de forma diferente entre as versões, pois a maneira como as chaves são armazenadas é diferente entre a 6.3 e as versões mais antigas.

Consulte abaixo para obter mais informações.

#### Replicação de chaves para o AEM 6.3 {#replicating-keys-for-aem}

Enquanto em versões mais antigas as chaves de replicação eram armazenadas no repositório, a partir da AEM 6.3, elas são armazenadas no sistema de arquivos.

Portanto, para replicar suas chaves em instâncias, é necessário copiá-las da instância de origem para o local das instâncias de destino no sistema de arquivos.

Mais especificamente, é necessário:

1. Acesse a instância AEM, normalmente uma instância de autor, que contém o material principal a ser copiado;
1. Localize o pacote com.adobe.granite.crypto.file no sistema de arquivos local. Por exemplo, neste caminho:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   O arquivo `bundle.info` dentro de cada pasta identificará o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie o HMAC e os arquivos principais.
1. Em seguida, vá para a instância de destino para a qual deseja duplicar a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualize o ](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) pacote Crypto, se a instância de destino já estiver em execução.
1. Repita as etapas acima para todas as instâncias para as quais deseja replicar a chave.

>[!NOTE]
>
>Você pode reverter para o método pré-6.3 de armazenamento de chaves adicionando o parâmetro abaixo ao instalar o AEM pela primeira vez:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replicação de chaves para AEM 6.2 e versões anteriores {#replicating-keys-for-aem-and-older-versions}

Em AEM 6.2 e versões mais antigas, as chaves são armazenadas no repositório no nó `/etc/key` .

A maneira recomendada para replicar com segurança as chaves em suas instâncias é replicar apenas esse nó. Você pode replicar nós seletivamente via CRXDE Lite:

1. Abra o CRXDE Lite acessando *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Selecione o nó `/etc/key`.
1. Vá para a guia **Replication** .
1. Pressione o botão **Replication**.

### Realização de teste de penetração {#perform-a-penetration-test}

A Adobe recomenda realizar um teste de penetração na infraestrutura do seu AEM antes de continuar a produção.

### Práticas recomendadas de desenvolvimento {#development-best-practices}

É importante que o novo desenvolvimento esteja seguindo as [Práticas recomendadas de segurança](/help/sites-developing/security.md) para garantir que seu ambiente AEM permaneça seguro.
