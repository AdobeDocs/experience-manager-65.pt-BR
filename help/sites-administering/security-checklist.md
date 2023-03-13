---
title: Lista de verificação de segurança
seo-title: Security Checklist
description: Saiba mais sobre as várias considerações de segurança ao configurar e implantar o AEM.
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
source-git-commit: 7efe4a011d831c34f6aafd877654e8b41fec96e0
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 3%

---

# Lista de verificação de segurança {#security-checklist}

Esta seção trata de várias etapas necessárias para garantir que a instalação do AEM esteja segura quando implantada. A lista de verificação deve ser aplicada de cima para baixo.

>[!NOTE]
>
>Estão também disponíveis informações adicionais sobre as ameaças à segurança mais perigosas publicadas pela [Open Web Application Security Project (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Há alguns [considerações de segurança](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aplicável na fase de desenvolvimento.

## Principais medidas de segurança {#main-security-measures}

### Execute o AEM no modo de produção pronta {#run-aem-in-production-ready-mode}

Para obter mais informações, consulte [Execução do AEM no modo de produção pronta](/help/sites-administering/production-ready.md).

### Ativar HTTPS para segurança da camada de transporte {#enable-https-for-transport-layer-security}

Habilitar a camada de transporte HTTPS em instâncias de autor e publicação é obrigatório para ter uma instância segura.

>[!NOTE]
>
>Consulte a [Habilitar HTTP por SSL](/help/sites-administering/ssl-by-default.md) para obter mais informações.

### Instalar Hotfixes de Segurança {#install-security-hotfixes}

Verifique se você instalou o mais recente [Hotfixes de segurança fornecidos pelo Adobe](https://helpx.adobe.com/br/experience-manager/kb/aem63-available-hotfixes.html).

### Alterar senhas padrão para as contas de administrador do console do AEM e OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

A Adobe recomenda que, após a instalação, você altere a senha do [**AEM** `admin` contas](#changing-the-aem-admin-password) (em todas as instâncias).

Essas contas incluem:

* O AEM `admin` account

   Depois de alterar a senha da conta de administrador AEM, será necessário usar a nova senha ao acessar o CRX.

* A variável `admin` senha para o console OSGi da Web

   Essa alteração também será aplicada à conta de administrador usada para acessar o console da Web, portanto, você precisará usar a mesma senha ao acessá-la.

Essas duas contas usam credenciais separadas e ter uma senha forte e distinta para cada uma é essencial para uma implantação segura.

#### Alteração da senha do administrador do AEM {#changing-the-aem-admin-password}

A senha da conta de administrador do AEM pode ser alterada por meio da [Operações do Granite - Usuários](/help/sites-administering/granite-user-group-admin.md) console.

Aqui é possível editar a variável `admin` conta e [alterar a senha](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Alterar a conta de administrador também altera a conta do console da Web OSGi. Depois de alterar a conta de administrador, você deve alterar a conta OSGi para algo diferente.

#### Importância de alterar a senha do console da Web OSGi {#importance-of-changing-the-osgi-web-console-password}

Além do AEM `admin` conta, a falha na alteração da senha padrão para a senha do console da Web OSGi pode levar a:

* Exposição do servidor com uma senha padrão durante a inicialização e o encerramento (que pode levar minutos para servidores grandes);
* Exposição do servidor quando o repositório está inativo/reiniciando o pacote - e OSGI está em execução.

Para obter mais informações sobre como alterar a senha do console da Web, consulte [Alteração da senha do administrador do console da Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) abaixo.

#### Alteração da senha do administrador do console da Web OSGi {#changing-the-osgi-web-console-admin-password}

Você também deve alterar a senha usada para acessar o console da Web. Isso é feito com um [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) para atualizar as seguintes propriedades do **Console de gerenciamento do Apache Felix OSGi**:

* **Nome do usuário** e **Senha**, as credenciais para acessar o próprio Console de gerenciamento da Web Apache Felix.
A senha deve ser alterada *após* a instalação inicial para garantir a segurança da sua instância.

Para fazer isso:

>[!NOTE]
>
>Consulte [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos sobre a definição das configurações do OSGi.

1. Usar o **Ferramentas**, **Operações** , abra o **Console da Web** e navegue até o **Configuração** seção.
Por exemplo, em `<server>:<port>/system/console/configMgr`.
1. Navegue até a entrada para **Console de gerenciamento do Apache Felix OSGi**.
1. Altere o **nome de usuário** e **senha**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Selecione **Salvar**.

### Implementar manipulador de erros personalizado {#implement-custom-error-handler}

A Adobe recomenda definir páginas de manipulador de erros personalizadas, especialmente para códigos de resposta HTTP 404 e 500, a fim de evitar a divulgação de informações.

>[!NOTE]
>
>Consulte [Como posso criar scripts personalizados ou manipuladores de erros](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html) artigo da knowledge base para obter mais detalhes.

### Lista de verificação de segurança completa do Dispatcher {#complete-dispatcher-security-checklist}

O AEM Dispatcher é uma parte essencial de sua infraestrutura. Adobe é altamente recomendável que você conclua o [lista de verificação de segurança do dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=pt-BR#getting-started).

>[!CAUTION]
>
>Usando o Dispatcher, você deve desativar o seletor &quot;.form&quot;.

## Etapas de verificação {#verification-steps}

### Configurar usuários de replicação e transporte {#configure-replication-and-transport-users}

Uma instalação padrão de AEM especifica `admin` como usuário para credenciais de transporte no padrão [agentes de replicação](/help/sites-deploying/replication.md). Além disso, o usuário administrador é usado para originar a replicação no sistema do autor.

Por questões de segurança, ambos devem ser alterados para refletir o caso de uso específico em questão, tendo em mente os dois aspectos a seguir:

* A variável **usuário de transporte** não deve ser o usuário administrador. Em vez disso, configure um usuário no sistema de publicação que tenha direitos de acesso somente às partes relevantes do sistema de publicação e use as credenciais desse usuário para o transporte.

   Você pode começar com o usuário receptor de replicação agrupada e configurar os direitos de acesso desse usuário para corresponder à sua situação

* A variável **usuário de replicação** ou **ID de usuário agente** Também não deve ser o usuário administrador, mas um usuário que pode ver somente o conteúdo que deve ser replicado. O usuário de replicação é usado para coletar o conteúdo a ser replicado no sistema do autor antes de ser enviado ao publicador.

### Verifique as verificações de integridade da segurança do painel de operações {#check-the-operations-dashboard-security-health-checks}

O AEM 6 apresenta o novo Painel de operações, destinado a ajudar os operadores de sistema a solucionar problemas e monitorar a integridade de uma instância.

O painel também vem com uma coleção de verificações de integridade de segurança. É recomendável verificar o status de todas as verificações de integridade de segurança antes de entrar em atividade com a instância de produção. Para obter mais informações, consulte o [Documentação do Painel de operações](/help/sites-administering/operations-dashboard.md).

### Verifique se o conteúdo de exemplo está presente {#check-if-example-content-is-present}

Todos os exemplos de conteúdo e usuários (por exemplo, o projeto do Geometrixx e seus componentes) devem ser desinstalados e excluídos completamente em um sistema produtivo antes de torná-lo acessível publicamente.

>[!NOTE]
>
>Os aplicativos We.Retail de exemplo serão removidos se esta instância estiver em execução no [Modo de produção pronto](/help/sites-administering/production-ready.md). Se, por qualquer motivo, esse não for o caso, você poderá desinstalar o conteúdo de amostra acessando o Gerenciador de pacotes e procurando e desinstalando todos os pacotes We.Retail. Para obter mais informações, consulte [Trabalhar com pacotes](package-manager.md).

### Verifique se os pacotes de desenvolvimento de CRX estão presentes {#check-if-the-crx-development-bundles-are-present}

Esses pacotes OSGi de desenvolvimento devem ser desinstalados nos sistemas produtivos do autor e da publicação antes de torná-los acessíveis.

* Suporte ao CRXDE do Adobe (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* CRXDE Lite do Adobe Granite (com.adobe.granite.crxde-lite)

### Verifique se o pacote de desenvolvimento do Sling está presente {#check-if-the-sling-development-bundle-is-present}

A variável [Ferramentas de desenvolvedor de AEM para Eclipse](/help/sites-developing/aem-eclipse.md) implanta a Instalação do suporte ao Apache Sling Tooling (org.apache.sling.tooling.support.install).

Esse pacote OSGi deve ser desinstalado nos sistemas produtivos do autor e da publicação antes de torná-los acessíveis.

### Protect contra falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery}

#### A estrutura de proteção CSRF {#the-csrf-protection-framework}

O AEM 6.1 é enviado com um mecanismo que ajuda a proteger contra ataques de falsificação de solicitação entre sites, chamado de **Estrutura de proteção CSRF**. Para obter mais informações sobre como usá-lo, consulte o [documentação](/help/sites-developing/csrf-protection.md).

#### O filtro referenciador do Sling {#the-sling-referrer-filter}

Para resolver problemas de segurança conhecidos com a falsificação de solicitação entre sites (CSRF) no CRX WebDAV e no Apache Sling, é necessário adicionar configurações para o filtro Referenciador para usá-lo.

O serviço de filtro referenciador é um serviço OSGi que permite configurar:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores permitidos além do host do servidor.

   Por padrão, todas as variações do host local e os nomes de host atuais aos quais o servidor está vinculado estão na lista.

Para configurar o serviço de filtro de referenciador:

1. Abra o console Apache Felix (**Configurações**) em:

   `https://<server>:<port_number>/system/console/configMgr`

1. Fazer logon como `admin`.
1. No **Configurações** selecione:

   `Apache Sling Referrer Filter`

1. No `Allow Hosts` insira todos os hosts permitidos como referenciador. Cada entrada precisa estar no formato

   &lt;protocol>://&lt;server>:&lt;port>

   Por exemplo:

   * `https://allowed.server:80` permite todas as solicitações deste servidor com a porta especificada.
   * Se também quiser permitir solicitações https, insira uma segunda linha.
   * Se você permitir todas as portas desse servidor, poderá usar `0` como o número da porta.

1. Verifique a `Allow Empty` , se quiser permitir cabeçalhos de referenciador vazios/ausentes.

   >[!CAUTION]
   >
   >É recomendável fornecer um referenciador ao usar ferramentas de linha de comando, como `cURL` em vez de permitir um valor vazio, pois ele pode expor seu sistema a ataques CSRF.

1. Editar os métodos que este filtro deve usar para verificações com o `Filter Methods` campo.

1. Clique em **Salvar** para salvar as alterações.

### Configurações OSGI {#osgi-settings}

Algumas configurações de OSGI são definidas por padrão para facilitar a depuração do aplicativo. Eles precisam ser alterados nas instâncias produtivas de publicação e criação para evitar que informações internas vazem para o público.

>[!NOTE]
>
>Todas as configurações abaixo, com exceção de **O filtro de depuração Day CQ WCM** são automaticamente cobertas pelo [Modo de produção pronto](/help/sites-administering/production-ready.md). Por causa disso, recomendamos revisar todas as configurações antes de implantar sua instância em um ambiente produtivo.

Para cada um dos seguintes serviços, as configurações especificadas precisam ser alteradas:

* [Gerenciador de biblioteca de HTML do Adobe Granite](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * habilitar **Minify** (para remover CRLF e caracteres de espaço em branco).
   * habilitar **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * disable **Depurar**
   * disable **Tempo**

* [Filtro de depuração WCM CQ diário](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * desmarcar **Ativar**

* [Filtro WCM CQ do dia](/help/sites-deploying/osgi-configuration-settings.md):

   * somente na publicação, defina **Modo WCM** para &quot;desativado&quot;

* [Manipulador de script Java do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Gerar informações de depuração**

* [Manipulador de script JSP do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Gerar informações de depuração**
   * disable **Conteúdo mapeado**

Para obter mais detalhes, consulte [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Outras leituras {#further-readings}

### Atenuar ataques de negação de serviço (DoS) {#mitigate-denial-of-service-dos-attacks}

Um ataque de negação de serviço (DoS) é uma tentativa de tornar um recurso de computador indisponível para os usuários desejados. Isso geralmente é feito sobrecarregando o recurso; por exemplo:

* Com uma enxurrada de solicitações de uma fonte externa.
* Com uma solicitação de mais informações do que o sistema pode fornecer com êxito.

   Por exemplo, uma representação em JSON de todo o repositório.

* Ao solicitar uma página de conteúdo com um número ilimitado de URLs, o URL pode incluir um identificador, alguns seletores, uma extensão e um sufixo. Qualquer um deles pode ser modificado.

   Por exemplo, `.../en.html` também pode ser solicitado como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas as variações válidas (por exemplo, retornar um `200` e são configurados para serem armazenados em cache) serão armazenados em cache pelo Dispatcher, eventualmente levando a um sistema de arquivos completo e sem serviço para outras solicitações.

Existem muitos pontos de configuração para evitar tais ataques, aqui só discutimos aqueles diretamente relacionados ao AEM.

**Configuração do Sling para impedir o DoS**

O Sling está *centrado no conteúdo*. Isso significa que o processamento está focado no conteúdo conforme cada solicitação (HTTP) é mapeada no conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro destino é o recurso (nó JCR) que contém o conteúdo.
* Em segundo lugar, o renderizador, ou script, está localizado nas propriedades de recurso em combinação com determinadas partes da solicitação (por exemplo, seletores e/ou a extensão).

>[!NOTE]
>
>Este aspecto é abordado mais pormenorizadamente no [Processamento de solicitação do Sling](/help/sites-developing/the-basics.md#sling-request-processing).

Essa abordagem torna o Sling muito eficiente e flexível, mas, como sempre, é a flexibilidade que precisa ser gerenciada com cuidado.

Para ajudar a evitar o uso incorreto de DoS, você pode:

1. Incorpora controles no nível do aplicativo; devido ao número de variações possíveis, uma configuração padrão não é viável.

   No aplicativo, você deve:

   * Controle os seletores em seu aplicativo para que você *somente* atendem aos seletores explícitos necessários e retornam `404` para todos os outros.
   * Evite a saída de um número ilimitado de nós de conteúdo.

1. Verifique a configuração dos renderizadores padrão, que pode ser uma área com problemas.

   * Em particular, o renderizador JSON, que pode atravessar a estrutura da árvore em vários níveis.

      Por exemplo, a solicitação:

      `http://localhost:4502/.json`

      O poderia despejar todo o repositório em uma representação JSON. Isso causaria problemas significativos no servidor. Por essa razão, o Sling define um limite no número de resultados máximos. Para limitar a profundidade da renderização JSON, é possível definir o valor de:

      **Máximo de resultados JSON** ( `json.maximumresults`)

      na configuração do para o [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando esse limite for excedido, a renderização será recolhida. O valor padrão para o Sling dentro do AEM é `1000`.

   * Como medida preventiva, desative os outros renderizadores padrão (HTML, texto simples, XML). Novamente, configurando o [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Não desative o renderizador JSON, pois isso é necessário para a operação normal do AEM.

1. Use um firewall para filtrar o acesso à sua instância.

   * O uso de um firewall de nível de sistema operacional é necessário para filtrar o acesso a pontos da sua instância que podem levar a ataques de negação de serviço, se deixados desprotegidos.

**Mitigar Contra DoS Causado pelo Uso de Seletores de Formulário**

>[!NOTE]
>
>Essa mitigação deve ser executada somente em ambientes AEM que não estejam usando o Forms.

Como o AEM não fornece índices prontos para uso para o `FormChooserServlet`No entanto, o uso de seletores de formulário em consultas acionará uma travessia de repositório dispendiosa, normalmente imobilizando a instância do AEM. Os seletores de formulário podem ser detectados pela presença do **&amp;ast;.form.&amp;ast;** sequência de caracteres em consultas.

Para atenuar isso, siga as etapas abaixo:

1. Vá para o Console da Web apontando seu navegador para *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Pesquisar por **Servlet do seletor de formulários WCM CQ do dia**
1. Depois de clicar na entrada, desative a variável **Pesquisa Avançada Requerida** na janela a seguir.

1. Clique em **Salvar**.

**Mitigar Contra DoS Causado pelo Servlet de download de ativo**

O servlet de download de ativos padrão permite que usuários autenticados emitam solicitações de download simultâneas grandes arbitrariamente para criar arquivos ZIP de ativos. A criação de arquivos ZIP grandes pode sobrecarregar o servidor e a rede. Para atenuar um possível risco de Negação de serviço (DoS) causado por esse comportamento, `AssetDownloadServlet` O componente OSGi é desativado por padrão em [!DNL Experience Manager] instância de publicação. Está ativado em [!DNL Experience Manager] instância do autor por padrão.

Se você não precisar do recurso de download, desative o servlet nas implantações de autor e publicação. Se a configuração exigir que o recurso de download de ativos esteja ativado, consulte [este artigo](/help/assets/download-assets-from-aem.md) para obter mais informações. Além disso, é possível definir um limite máximo de download que sua implantação possa suportar.

### Desabilitar WebDAV {#disable-webdav}

O WebDAV deve ser desativado nos ambientes do autor e de publicação. Isso pode ser feito interrompendo os pacotes OSGi apropriados.

1. Conecte-se à **Felix Management Console** em execução em:

   `https://<*host*>:<*port*>/system/console`

   Por exemplo, `http://localhost:4503/system/console/bundles`.

1. Na lista de pacotes, localize o pacote chamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Clique no botão Stop (na coluna Actions) para interromper esse pacote.

1. Novamente na lista de pacotes, localize o pacote chamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Clique no botão stop para interromper esse pacote.

   >[!NOTE]
   >
   >Não é necessário reiniciar o AEM.

### Verifique se você não está revelando informações de identificação pessoal no caminho da página inicial dos usuários {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

É importante proteger seus usuários, certificando-se de não expor nenhuma informação de identificação pessoal no caminho inicial dos usuários do repositório.

Desde o AEM 6.1, a forma como os nomes de nó da ID de usuário (também conhecida como autorizável) são armazenados é alterada com uma nova implementação do `AuthorizableNodeName` interface. A nova interface não exibirá mais a ID de usuário no nome do nó, mas gerará um nome aleatório.

Nenhuma configuração precisa ser executada para ativá-la, pois essa agora é a maneira padrão de gerar IDs autorizáveis no AEM.

Embora não seja recomendado, você pode desativá-la caso precise da implementação antiga para ter compatibilidade com versões anteriores de seus aplicativos existentes. Para fazer isso, é necessário:

1. Vá para o Console da Web e remova a entrada** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** da propriedade **requiredServicePids** in **Apache Jackrabbit Oak SecurityProvider**.

   Você também pode encontrar o Provedor de segurança do Oak procurando pelo **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID nas configurações do OSGi.

1. Exclua o **Nome do nó autorizado aleatório Apache Jackrabbit Oak** Configuração OSGi no console da Web.

   Para facilitar a pesquisa, observe que o PID dessa configuração é **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obter mais informações, consulte a documentação do Oak em [Geração do nome do nó autorizada](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### Prevenção contra clickjacking {#prevent-clickjacking}

Para evitar clickjacking, recomendamos que você configure seu servidor Web para fornecer o cabeçalho HTTP `X-FRAME-OPTIONS` definido como `SAMEORIGIN`.

Para obter mais [informações sobre clickjacking, consulte o site OWASP](https://www.owasp.org/index.php/Clickjacking).

### Certifique-Se De Replicar Corretamente As Chaves De Criptografia Quando Necessário {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Certos recursos e esquemas de autenticação do AEM exigem a replicação das chaves de criptografia em todas as instâncias do AEM.

Antes de fazer isso, observe que a replicação de chaves é feita de forma diferente entre as versões, pois a maneira como as chaves são armazenadas é diferente entre as versões 6.3 e mais antigas.

Consulte mais informações abaixo.

#### Replicação de chaves para AEM 6.3 {#replicating-keys-for-aem}

Enquanto em versões mais antigas, as chaves de replicação eram armazenadas no repositório, a partir do AEM 6.3 elas são armazenadas no sistema de arquivos.

Portanto, para replicar suas chaves entre instâncias, é necessário copiá-las da instância de origem para o local das instâncias de destino no sistema de arquivos.

Mais especificamente, é necessário:

1. Acesse a instância do AEM, normalmente uma instância de autor, que contém o material principal a ser copiado;
1. Localize o conjunto com.adobe.granite.crypto.file no sistema de arquivos local. Por exemplo, neste caminho:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   A variável `bundle.info` arquivo dentro de cada pasta identificará o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie os arquivos HMAC e principais.
1. Em seguida, vá para a instância de destino para a qual deseja duplicar a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualizar o pacote de criptografia](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se a instância de destino já estiver em execução.
1. Repita as etapas acima para todas as instâncias para as quais deseja replicar a chave.

>[!NOTE]
>
>É possível reverter para o método pré 6.3 de armazenamento de chaves ao adicionar o parâmetro abaixo quando você instala o AEM pela primeira vez:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replicação de chaves para AEM 6.2 e versões anteriores {#replicating-keys-for-aem-and-older-versions}

No AEM 6.2 e versões anteriores, as chaves são armazenadas no repositório do `/etc/key` nó.

A maneira recomendada de replicar com segurança as chaves em suas instâncias é replicar somente esse nó. Você pode replicar nós seletivamente via CRXDE Lite:

1. Abra o CRXDE Lite acessando *https://&lt;serveraddress>:4502/crx/de/index.jsp*
1. Selecione o `/etc/key` nó.
1. Vá para a **Replicação** guia.
1. Pressione a **Replicação** botão.

### Realização de teste de penetração {#perform-a-penetration-test}

A Adobe recomenda realizar um teste de penetração na infraestrutura do seu AEM antes de continuar a produção.

### Práticas recomendadas de desenvolvimento {#development-best-practices}

É fundamental que os novos desenvolvimentos [Práticas recomendadas de segurança](/help/sites-developing/security.md) para garantir que seu ambiente AEM permaneça seguro.
