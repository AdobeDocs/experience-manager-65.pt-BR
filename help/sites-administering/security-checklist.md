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
source-git-commit: e44480535ea7058dc41fc747351446b670d03b7f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Lista de verificação de segurança {#security-checklist}

Esta seção trata de várias etapas que você deve tomar para garantir que sua instalação AEM seja segura quando implantada. A lista de verificação deve ser aplicada de cima para baixo.

>[!NOTE]
>
>Estão também disponíveis informações adicionais sobre as ameaças de segurança mais perigosas, publicadas por [Abrir Projeto de Segurança de Aplicativo Web (OWASP)](https://owasp.org/www-project-top-ten/).

>[!NOTE]
>
>Há alguns [considerações de segurança](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations) aplicável na fase de desenvolvimento.

## Principais medidas de segurança {#main-security-measures}

### Executar AEM no modo Pronto para produção {#run-aem-in-production-ready-mode}

Para obter mais informações, consulte [Executando AEM no modo Pronto para produção](/help/sites-administering/production-ready.md).

### Ativar HTTPS para segurança da camada de transporte {#enable-https-for-transport-layer-security}

Habilitar a camada de transporte HTTPS nas instâncias de autor e publicação é obrigatório para ter uma instância segura.

>[!NOTE]
>
>Consulte a [Habilitar HTTP por SSL](/help/sites-administering/ssl-by-default.md) para obter mais informações.

### Instalar hotfixes de segurança {#install-security-hotfixes}

Certifique-se de ter instalado a versão mais recente [Hotfixes de segurança fornecidos pelo Adobe](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=pt-BR).

### Alterar senhas padrão para contas de administração do console AEM e OSGi {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

O Adobe recomenda, após a instalação, que você altere a senha dos privilegiados [**AEM** `admin` contas](#changing-the-aem-admin-password) (em todas as instâncias).

Essas contas incluem:

* O AEM `admin` account

   Depois de alterar a senha da conta de administrador AEM, use a nova senha ao acessar o CRX.

* O `admin` senha para o console da Web OSGi

   Essa alteração também é aplicada à conta de administrador usada para acessar o console da Web, portanto, use a mesma senha ao acessar essa.

Essas duas contas usam credenciais separadas e ter uma senha forte e distinta para cada é essencial para uma implantação segura.

#### Alterar a senha do administrador AEM {#changing-the-aem-admin-password}

A senha da conta de administrador do AEM pode ser alterada por meio do [Operações do Granite - Usuários](/help/sites-administering/granite-user-group-admin.md) console.

Aqui você pode editar o `admin` e [alterar a senha](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user).

>[!NOTE]
>
>Alterar a conta de administrador também altera a conta do console da Web OSGi. Depois de alterar a conta de administrador, você deve alterar a conta OSGi para algo diferente.

#### Importância de alterar a senha do console da Web OSGi {#importance-of-changing-the-osgi-web-console-password}

Além do AEM `admin` , a não alteração da senha padrão do console da Web OSGi pode levar a:

* Exposição do servidor com uma senha padrão durante a inicialização e o desligamento (que pode levar minutos para grandes servidores);
* Exposição do servidor quando o repositório está inativo/reiniciando o pacote - e OSGI está em execução.

Para obter mais informações sobre como alterar a senha do console da Web, consulte [Alteração da senha do administrador do console da Web OSGi](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) abaixo.

#### Alteração da senha do administrador do console da Web OSGi {#changing-the-osgi-web-console-admin-password}

Altere a senha usada para acessar o console da Web. Use um [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) para atualizar as seguintes propriedades do **Console de Gerenciamento do Apache Felix OSGi**:

* **Nome do usuário** e **Senha**, as credenciais para acessar o próprio Apache Felix Web Management Console.
A senha deve ser alterada *after* a instalação inicial para garantir a segurança da sua instância.

>[!NOTE]
>
>Consulte [Configuração OSGI](/help/sites-deploying/configuring-osgi.md) para obter detalhes completos sobre a configuração das configurações do OSGi.

**Para alterar a senha do administrador do console da Web OSGi**:

1. Usar o **Ferramentas**, **Operações** abra o **Console da Web** e navegue até o **Configuração** seção.
Por exemplo, em `<server>:<port>/system/console/configMgr`.
1. Navegue até a entrada e abra-a para **Console de Gerenciamento do Apache Felix OSGi**.
1. Altere o **nome do usuário** e **senha**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. Selecione **Salvar**.

### Implementar o Manipulador de Erros Personalizado {#implement-custom-error-handler}

O Adobe recomenda definir páginas personalizadas do manipulador de erros, especialmente para os códigos de resposta HTTP 404 e 500, para evitar a divulgação de informações.

>[!NOTE]
>
>Consulte [Como posso criar scripts personalizados ou manipuladores de erros](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) para obter mais detalhes.

### Lista de verificação de segurança completa do Dispatcher {#complete-dispatcher-security-checklist}

AEM Dispatcher é uma parte essencial de sua infraestrutura. O Adobe recomenda que você conclua a [Lista de verificação de segurança do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>Usando o Dispatcher, você deve desativar o seletor &quot;.form&quot;.

## Etapas de verificação {#verification-steps}

### Configurar usuários de replicação e transporte {#configure-replication-and-transport-users}

Uma instalação padrão de AEM especifica `admin` como usuário para credenciais de transporte no padrão [agentes de replicação](/help/sites-deploying/replication.md). Além disso, o usuário administrador é usado para originar a replicação no sistema de criação.

Por questões de segurança, ambas devem ser alteradas de forma a refletirem o caso de uso específico em questão, tendo em conta os dois aspectos seguintes:

* O **utilizador de transportes** não deve ser o usuário administrador. Em vez disso, configure um usuário no sistema de publicação que tenha somente direitos de acesso às partes relevantes do sistema de publicação e use as credenciais desse usuário para o transporte.

   Você pode começar com o usuário receptor de replicação empacotado e configurar os direitos de acesso deste usuário para corresponder à sua situação

* O **usuário de replicação** ou **ID de usuário do agente** também não deve ser o usuário administrador, mas um usuário que só pode ver o conteúdo que é replicado. O usuário de replicação é usado para coletar o conteúdo a ser replicado no sistema de autor antes de ser enviado ao editor.

### Verifique as verificações de integridade de segurança do painel de operações {#check-the-operations-dashboard-security-health-checks}

O AEM 6 apresenta o novo Painel de Operações, destinado a ajudar os operadores do sistema a solucionar problemas e monitorar a integridade de uma instância.

O painel também vem com uma coleção de verificações de integridade de segurança. É recomendável verificar o status de todas as verificações de integridade de segurança antes de entrar em vigor com a instância de produção. Para obter mais informações, consulte o [Documentação do Painel de operações](/help/sites-administering/operations-dashboard.md).

### Verifique se o conteúdo de exemplo está presente {#check-if-example-content-is-present}

Todo o conteúdo de exemplo e os usuários (por exemplo, o projeto do Geometrixx e seus componentes) devem ser desinstalados e excluídos completamente em um sistema produtivo antes de torná-lo acessível ao público.

>[!NOTE]
>
>A amostra `We.Retail` os aplicativos são removidos se esta instância estiver em execução no [Modo Pronto para produção](/help/sites-administering/production-ready.md). Se esse cenário não for o caso, é possível desinstalar o conteúdo de amostra indo até o Gerenciador de pacotes, procurando e desinstalando todos os `We.Retail` pacotes.

Consulte [Trabalhar com pacotes](package-manager.md).

### Verifique se os pacotes de desenvolvimento do CRX estão presentes {#check-if-the-crx-development-bundles-are-present}

Esses pacotes OSGi de desenvolvimento devem ser desinstalados nos sistemas produtivos de criação e publicação antes de torná-los acessíveis.

* Suporte a Adobe CRXDE (com.adobe.granite.crxde-support)
* Adobe Granite CRX Explorer (com.adobe.granite.crx-explorer)
* Adobe Granite CRXDE Lite (com.adobe.granite.crxde-lite)

### Verifique se o pacote de desenvolvimento do Sling está presente {#check-if-the-sling-development-bundle-is-present}

O [Ferramentas do desenvolvedor do AEM](/help/sites-developing/aem-eclipse.md) implante a instalação do suporte a ferramentas do Apache Sling (org.apache.sling.tooling.support.install).

Este pacote OSGi deve ser desinstalado nos sistemas produtivos de autor e publicação antes de torná-los acessíveis.

### Protect contra falsificação de solicitação entre sites {#protect-against-cross-site-request-forgery}

#### Quadro de proteção do QREF {#the-csrf-protection-framework}

O AEM 6.1 acompanha um mecanismo que ajuda a proteger contra ataques de falsificação de solicitação entre sites, chamado de **Estrutura de proteção do CSRF**. Para obter mais informações sobre como usá-lo, consulte o [documentação](/help/sites-developing/csrf-protection.md).

#### O filtro do referenciador do Sling {#the-sling-referrer-filter}

Para solucionar problemas de segurança conhecidos com a falsificação de solicitação entre sites (CSRF) no CRX WebDAV e no Apache Sling, adicione configurações para o filtro Referenciador usá-lo.

O serviço de filtro do referenciador é um serviço OSGi que permite configurar o seguinte:

* quais métodos http devem ser filtrados
* se um cabeçalho de referenciador vazio é permitido
* e uma lista de servidores a serem permitidos além do host do servidor.

   Por padrão, todas as variações de localhost e os nomes de host atuais aos quais o servidor está vinculado estão na lista.

Para configurar o serviço de filtro do referenciador:

1. Abra o console do Apache Felix (**Configurações**) em:

   `https://<server>:<port_number>/system/console/configMgr`

1. Efetuar logon como `admin`.
1. No **Configurações** selecione:

   `Apache Sling Referrer Filter`

1. No `Allow Hosts` , insira todos os hosts permitidos como referenciador. Cada entrada deve ser do formulário

   &lt;protocol>://&lt;server>:&lt;port>

   Por exemplo:

   * `https://allowed.server:80` permite todas as solicitações deste servidor com a porta especificada.
   * Se também quiser permitir solicitações https, é necessário inserir uma segunda linha.
   * Se você permitir todas as portas desse servidor, poderá usar `0` como o número da porta.

1. Verifique a `Allow Empty` , se desejar permitir cabeçalhos de referenciador vazios/ausentes.

   >[!CAUTION]
   >
   >O Adobe recomenda que você forneça um referenciador ao usar ferramentas de linha de comando como `cURL` em vez de permitir um valor vazio, pois pode expor seu sistema a ataques de CSRF.

1. Edite os métodos que esse filtro usa para verificações com o `Filter Methods` campo.

1. Clique em **Salvar** para salvar as alterações.

### Configurações OSGI {#osgi-settings}

Algumas configurações OSGI são definidas por padrão para permitir uma depuração mais fácil do aplicativo. Altere essas configurações em suas instâncias produtivas de publicação e criação para evitar o vazamento de informações internas para o público.

>[!NOTE]
>
>Todas as configurações abaixo, exceto por **O filtro de depuração Day CQ WCM** são automaticamente cobertos pela variável [Modo Pronto para produção](/help/sites-administering/production-ready.md). Dessa forma, o Adobe recomenda que você analise todas as configurações antes de implantar sua instância em um ambiente produtivo.

Para cada um dos seguintes serviços, as configurações especificadas devem ser alteradas:

* [Gerenciador de biblioteca de HTML do Adobe Granite](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * habilitar **Minimizar** (para remover caracteres CRLF e espaço em branco).
   * habilitar **Gzip** (para permitir que os arquivos sejam compactados e acessados com uma solicitação).
   * disable **Depurar**
   * disable **Tempo**

* [Filtro de depuração do Day CQ WCM](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter):

   * desmarcar **Habilitar**

* [Filtro Day CQ WCM](/help/sites-deploying/osgi-configuration-settings.md):

   * somente ao publicar, definir **Modo WCM** para &quot;desativado&quot;

* [Manipulador de JavaScript do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * disable **Gerar informações de depuração**

* [Manipulador de script JSP do Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler):

   * disable **Gerar informações de depuração**
   * disable **Conteúdo mapeado**

Consulte [Configurações do OSGi](/help/sites-deploying/osgi-configuration-settings.md).

Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

## Outras Leituras {#further-readings}

### Reduza os ataques de negação de serviço (DoS) {#mitigate-denial-of-service-dos-attacks}

Um ataque de negação de serviço (DoS) é uma tentativa de tornar um recurso de computador indisponível para os usuários desejados. Este ataque é frequentemente feito sobrecarregando o recurso; por exemplo:

* Um fluxo de solicitações de uma fonte externa.
* Uma solicitação para obter mais informações do que o sistema pode fornecer com sucesso.

   Por exemplo, uma representação JSON de todo o repositório.

* Ao solicitar uma página de conteúdo com um número ilimitado de URLs, o URL pode incluir um identificador, alguns seletores, uma extensão e um sufixo, qualquer um dos quais pode ser modificado.

   Por exemplo, `.../en.html` também pode ser solicitada como:

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   Todas as variações válidas (por exemplo, retornam um `200` e são configurados para serem armazenados em cache) são armazenados em cache pelo Dispatcher, resultando em um sistema de arquivos completo e nenhum serviço para solicitações adicionais.

Há muitos pontos de configuração para prevenir tais ataques, mas apenas os que se relacionam com AEM são discutidos aqui.

**Configurar o Sling para evitar DoS**

O Sling é *centrado no conteúdo*. O processamento é focado no conteúdo, já que cada solicitação (HTTP) é mapeada no conteúdo na forma de um recurso JCR (um nó de repositório):

* O primeiro target é o recurso (nó JCR) que contém o conteúdo.
* Segundo, o renderizador ou script está localizado nas propriedades do recurso com determinadas partes da solicitação (por exemplo, seletores e/ou extensão).

Consulte [Processamento de solicitação Sling](/help/sites-developing/the-basics.md#sling-request-processing) para obter mais informações.

Essa abordagem torna o Sling poderoso e flexível, mas, como sempre, é a flexibilidade que deve ser gerenciada com cuidado.

Para ajudar a evitar o uso indevido de DoS, você pode fazer o seguinte:

1. Incorpore controles no nível do aplicativo. Devido ao número de variações possíveis, uma configuração padrão não é viável.

   No seu aplicativo, você deve:

   * Controle os seletores em seu aplicativo, para que você *only* forneça os seletores explícitos necessários e retorne `404` para todos os outros.
   * Impeça a saída de um número ilimitado de nós de conteúdo.

1. Verifique a configuração dos renderizadores padrão, que pode ser uma área problemática.

   * Em particular, o renderizador JSON atravessa a estrutura em árvore em vários níveis.

      Por exemplo, a solicitação:

      `http://localhost:4502/.json`

      O pode despejar todo o repositório em uma representação JSON, o que pode causar problemas significativos no servidor. Por esse motivo, o Sling define um limite no número máximo de resultados. Para limitar a profundidade da renderização JSON, defina o valor para o seguinte:

      **Máximo de resultados JSON** ( `json.maximumresults`)

      na configuração do [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet). Quando esse limite é excedido, a renderização é recolhida. O valor padrão para Sling em AEM é `1000`.

   * Como medida preventiva, você deve desativar os outros renderizadores padrão (HTML, texto sem formatação, XML). Novamente, configurando o [Servlet de GET Apache Sling](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >Não desative o renderizador JSON porque ele é necessário para a operação normal de AEM.

1. Use um firewall para filtrar o acesso à sua instância.

   * O uso de um firewall no nível do sistema operacional é necessário para filtrar o acesso aos pontos da instância que podem levar a ataques de negação de serviço se eles ficarem desprotegidos.

**Mitigar contra ações causadas pelo uso de seletores de formulário**

>[!NOTE]
>
>Essa atenuação deve ser executada somente em ambientes AEM que não estejam usando o Forms.

Como o AEM não fornece índices prontos para uso para a variável `FormChooserServlet`, o uso de seletores de formulário em queries pode acionar uma dispendiosa travessia do repositório, geralmente paralisando a instância de AEM. Os seletores de formulários podem ser detectados pela presença do **&amp;ast;.form.&amp;ast;** em queries.

Para atenuar esse problema, você pode executar as seguintes etapas:

1. Vá para o Console da Web apontando seu navegador para *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*

1. Procurar por **Servlet do Seletor de Formulário Day CQ WCM**
1. Depois de clicar na entrada, desative o **Necessidade de pesquisa avançada** na janela a seguir.

1. Clique em **Salvar**.

**Mitigar contra ações causadas pelo servlet de download de ativos**

O servlet de download de ativos padrão permite que usuários autenticados emitam solicitações arbitrariamente grandes, simultâneas e de download para criar arquivos ZIP de ativos. Criar arquivos ZIP grandes pode sobrecarregar o servidor e a rede. Para mitigar um risco potencial de Negação de Serviço (DoS) causado por esse comportamento, `AssetDownloadServlet` O componente OSGi é desativado por padrão em [!DNL Experience Manager] instância de publicação. Está ativado em [!DNL Experience Manager] instância do autor por padrão.

Se não precisar do recurso de download, desative o servlet nas implantações de criação e publicação. Se a configuração exigir que o recurso de download de ativos esteja ativado, consulte [este artigo](/help/assets/download-assets-from-aem.md) para obter mais informações. Além disso, é possível definir um limite máximo de download que sua implantação possa suportar.

### Desativar WebDAV {#disable-webdav}

Desative o WebDAV nos ambientes de autor e publicação, interrompendo os pacotes OSGi apropriados.

1. Conecte-se ao **Console de Gerenciamento Felix** em execução:

   `https://<*host*>:<*port*>/system/console`

   Por exemplo, `http://localhost:4503/system/console/bundles`.

1. Na lista de pacotes, encontre o pacote chamado:

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. Para interromper esse pacote, na coluna Actions , clique no botão stop .

1. Novamente, na lista de pacotes, encontre o pacote chamado:

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. Para interromper esse pacote, clique no botão stop .

   >[!NOTE]
   >
   >Não é necessário reiniciar o AEM.

### Verifique Se Você Não Está Exibindo Informações Pessoalmente Identificáveis No Caminho Inicial Dos Usuários {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

É importante proteger seus usuários, certificando-se de que você não exponha informações pessoalmente identificáveis no caminho inicial dos usuários do repositório.

Desde o AEM 6.1, a maneira como os nomes de nó da ID do usuário (também conhecida como autorizável) são armazenados é alterada com uma nova implementação do `AuthorizableNodeName` interface. A nova interface não expõe mais a ID de usuário no nome do nó, mas gera um nome aleatório.

Nenhuma configuração deve ser executada para habilitá-la, pois agora é a maneira padrão de gerar IDs autorizáveis no AEM.

Embora não seja recomendado, você pode desativá-lo caso precise da implementação antiga para ter compatibilidade com os aplicativos existentes. Para fazer isso, você deve fazer o seguinte:

1. Vá para o Console da Web e remova a entrada** org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** da propriedade **requiredServicePids** em **Apache Jackrabbit Oak SecurityProvider**.

   Você também pode encontrar o Provedor de segurança Oak procurando pela variável **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID nas configurações do OSGi.

1. Exclua o **Nome de nó autorizado aleatório do Apache Jackrabbit Oak** Configuração do OSGi no Console da Web.

   Para uma pesquisa mais fácil, o PID para esta configuração é **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>Para obter mais informações, consulte a documentação do Oak em [Geração de Nome de Nó Autorizável](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

**Pacote Anônimo de Otimização de Permissões**

Por padrão, o AEM armazena metadados do sistema, como `jcr:createdBy` ou `jcr:lastModifiedBy` como propriedades do nó, ao lado do conteúdo regular, no repositório. Dependendo da configuração e da configuração do controle de acesso, em alguns casos isso pode levar à exposição de informações de identificação pessoal (PII), por exemplo, quando esses nós são renderizados como JSON bruto ou XML.

Como todos os dados do repositório, essas propriedades são mediadas pela pilha de autorização do Oak. O seu acesso deve ser restringido de acordo com o princípio do menor privilégio.

Para dar suporte a isso, o Adobe fornece um pacote de proteção de permissão como base para os clientes se desenvolverem. Funciona instalando uma entrada de controle de acesso &quot;negar&quot; na raiz do repositório, restringindo o acesso anônimo às propriedades do sistema comumente usadas. O pacote está disponível para download [here](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) e pode ser instalado em todas as versões compatíveis do AEM. Consulte as notas de versão para obter mais informações.

### Prevenção contra clickjacking {#prevent-clickjacking}

Para evitar o clickjacking, o Adobe recomenda que você configure seu servidor da Web para fornecer a variável `X-FRAME-OPTIONS` Cabeçalho HTTP definido como `SAMEORIGIN`.

Para obter mais informações sobre clickjacking, consulte o [Site OWASP](https://www.owasp.org/index.php/Clickjacking).

### Certifique-Se De Replicar Corretamente As Chaves De Criptografia Quando Necessário {#make-sure-you-properly-replicate-encryption-keys-when-needed}

Determinados recursos de AEM e esquemas de autenticação exigem a replicação das chaves de criptografia em todas as instâncias de AEM.

Antes de fazer isso, a replicação de chaves é feita de forma diferente entre as versões, pois a maneira como as chaves são armazenadas é diferente entre a 6.3 e as versões mais antigas.

Consulte abaixo para obter mais informações.

#### Replicação de chaves para o AEM 6.3 {#replicating-keys-for-aem}

Enquanto em versões mais antigas as chaves de replicação eram armazenadas no repositório, a partir da AEM 6.3, elas são armazenadas no sistema de arquivos.

Portanto, para replicar suas chaves em instâncias, copie-as da instância de origem para o local das instâncias de destino no sistema de arquivos.

Mais especificamente, você deve fazer o seguinte:

1. Acesse a instância de AEM - normalmente uma instância de autor - que contém o material principal a ser copiado;
1. Localize o pacote com.adobe.granite.crypto.file no sistema de arquivos local. Por exemplo, neste caminho:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   O `bundle.info` dentro de cada pasta identifica o nome do pacote.

1. Navegue até a pasta de dados. Por exemplo:

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Copie o HMAC e os arquivos principais.
1. Em seguida, vá para a instância de destino para a qual deseja duplicar a chave HMAC e navegue até a pasta de dados. Por exemplo:

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. Cole os dois arquivos copiados anteriormente.
1. [Atualizar o pacote de criptografia](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle) se a instância de destino já estiver em execução.
1. Repita as etapas acima para todas as instâncias para as quais deseja replicar a chave.

>[!NOTE]
>
>Você pode reverter para o método pré-6.3 de armazenamento de chaves adicionando o parâmetro abaixo ao instalar o AEM pela primeira vez:
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### Replicação de chaves para AEM 6.2 e versões anteriores {#replicating-keys-for-aem-and-older-versions}

No AEM 6.2 e versões mais antigas, as chaves são armazenadas no repositório no `/etc/key` nó .

A maneira recomendada para replicar com segurança as chaves em suas instâncias é replicar apenas esse nó. Você pode replicar nós seletivamente via CRXDE Lite:

1. Abra o CRXDE Lite indo para *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`*
1. Selecione o `/etc/key` nó .
1. Vá para o **Replicação** guia .
1. Pressione a tecla **Replicação** botão.

### Realização de teste de penetração {#perform-a-penetration-test}

O Adobe recomenda que você realize um teste de penetração de sua infraestrutura de AEM antes de continuar a produção.

### Práticas recomendadas de desenvolvimento {#development-best-practices}

É fundamental que os novos desenvolvimentos sigam a [Práticas recomendadas de segurança](/help/sites-developing/security.md) para garantir que seu ambiente AEM permaneça seguro.
