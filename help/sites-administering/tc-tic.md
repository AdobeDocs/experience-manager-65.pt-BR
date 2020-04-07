---
title: Configuração da estrutura de integração de tradução
seo-title: Configuração da estrutura de integração de tradução
description: Saiba como configurar a estrutura de integração de tradução.
seo-description: Saiba como configurar a estrutura de integração de tradução.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
translation-type: tm+mt
source-git-commit: d01b36770ea1cc7f8d780c49bf8c2af70915c553

---


# Configuração da estrutura de integração de tradução{#configuring-the-translation-integration-framework}

A estrutura de integração de tradução integra-se a serviços de tradução de terceiros para orquestrar a tradução de conteúdo do AEM.

* Conecte-se ao seu provedor de serviço de tradução.
* Criar uma configuração de estrutura de integração de tradução.
* Associe as configurações de nuvem às suas páginas.

Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Traduzir conteúdo para sites multilíngues](/help/sites-administering/translation.md).

## Conexão a um Provedor de serviço de tradução {#connecting-to-a-translation-service-provider}

Crie uma configuração de nuvem que conecte o AEM ao seu provedor de serviço de tradução. O AEM inclui a capacidade de se conectar ao Microsoft Translator por padrão. Para outros provedores de tradução, baixe o pacote do conector do Compartilhamento de [pacotes](/help/sites-administering/package-manager.md#package-share).
Os seguintes fornecedores de tradução fornecem uma implementação da nova API para os Projetos de tradução. Links para saber mais sobre a integração e como fazer download do Compartilhamento de pacotes:

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (Adobe Exchange Premier Partner)
* [Clay Tablet Technologies](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/clay-tablet-translation-connector-for-aem.html) (não em PackageShare, entre em contato diretamente com o fornecedor)
* [Lionbridge](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lionbridge-for-adobe-experience-manager.html)
* [Palavras-nuvem](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/cloudwords-for-adobe-translations-connector.html)
* [CrossLang NV](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/crosslang-xtm-for-adobe-experience-manager.html)
* [Lingotek](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/lingotek-for-adobe-experience-manager.html)
* Microsoft (o Microsoft Translator está pré-instalado no AEM)
* [Inteligência](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/smartling-connector-for-adobe-experience-manager.html)
* [SDL WorldServer](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdlworldserver-connector.html)
* [TMS SDL](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/sdl-tms-translation-connector-for-adobe-experience-manager.html)
* [Systran](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/systran-for-adobe-experience-manager.html)
* [Altlang](https://marketing.adobe.com/resources/content/resources/en/exchange/marketplace/apps/Altlang.html)

>[!NOTE]
>
>Para encontrar a última lista de provedores de tradução automática e humana, visite estas páginas:
>
>
>* [Tradução do AEM Human](https://www.adobe.com/go/aem-human-translation-connectors)
>* [Tradução automática do AEM](https://www.adobe.com/go/aem-machine-translation-connectors)
>



Depois de instalar um pacote do conector, você pode criar uma configuração de nuvem para o conector. Geralmente, você precisa fornecer suas credenciais para autenticação com o serviço de tradução. Para obter informações sobre como adicionar uma configuração de nuvem para o conector do Microsoft Translator, consulte [Integração com o Microsoft Translator](/help/sites-administering/tc-msconf.md).

É possível criar várias configurações de nuvem para o mesmo conector, se necessário. Por exemplo, crie uma configuração para cada conta ou projeto que você tem com o mesmo fornecedor.

Depois de configurar uma conexão, você pode criar a configuração da estrutura de integração de tradução que a usa.

## Criando uma configuração de integração de tradução {#creating-a-translation-integration-configuration}

Crie uma configuração de estrutura de integração de tradução para especificar como traduzir seu conteúdo. A configuração inclui as seguintes informações:

* Que provedor de serviço de tradução usar.
* Se a tradução humana ou automática deve ser efetuada.
* Se você deve traduzir outro conteúdo associado a uma página ou ativo, como tags.

Depois de criar uma configuração de estrutura, associe a configuração da nuvem às páginas que deseja traduzir de acordo com a configuração. Quando o processo de tradução é iniciado, o fluxo de trabalho de tradução continua de acordo com a configuração de estrutura associada.

Quando diferentes seções do seu site tiverem diferentes requisitos de tradução, crie várias configurações de estrutura de acordo. Por exemplo, um site multilíngue inclui cópias em inglês, espanhol e japonês. O proprietário do site usa dois provedores de serviço de tradução diferentes para traduções em espanhol e japonês. Portanto, duas configurações da estrutura são configuradas. Cada configuração usa um provedor de serviço de tradução diferente.

Depois de configurar uma estrutura de integração de tradução, você pode [associá-la às páginas](/help/sites-administering/tc-prep.md) que a utilizam.

**Observação:** Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Traduzir conteúdo para sites multilíngues](/help/sites-administering/translation.md).

Uma única configuração da estrutura controla como traduzir o conteúdo da página, o conteúdo da comunidade e os ativos.
![chlimage_1-386](assets/translation-config-65.jpg)

### Propriedades de configuração de sites {#sites-configuration-properties}

As propriedades de Sites controlam como a tradução do conteúdo da página é realizada.

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Fluxo de trabalho da conversão</td>
   <td><p>Selecione o método de conversão que a estrutura executa para o conteúdo do site:</p>
    <ul>
     <li>Tradução automática: O provedor de tradução realiza a tradução usando tradução automática em tempo real.</li>
     <li>Tradução humana: O conteúdo é enviado ao provedor de tradução para ser traduzido pelos tradutores. </li>
     <li>Não Traduzir: O conteúdo não é enviado para tradução. Isso serve para ignorar certas ramificações de conteúdo que não seriam traduzidas, mas poderiam ser atualizadas com o conteúdo mais recente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provedor de tradução</td>
   <td>Selecione o provedor de tradução para executar a tradução. Um provedor é exibido na lista quando seu conector correspondente é instalado.</td>
  </tr>
  <tr>
   <td>Categoria de conteúdo</td>
   <td>(Somente tradução automática) Uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da formulação ao traduzir o conteúdo.</td>
  </tr>
  <tr>
   <td>Traduzir tags</td>
   <td>Selecione para traduzir as tags associadas à página.</td>
  </tr>
  <tr>
   <td>Traduzir ativos da página</td>
   <td><p>Selecione como traduzir ativos adicionados aos componentes do sistema de arquivos ou referenciados em Ativos:</p>
    <ul>
     <li>Não traduzir: Os ativos da página não são convertidos.</li>
     <li>Usando o fluxo de trabalho de tradução de Sites: Os ativos são tratados de acordo com as propriedades de configuração na guia Sites.</li>
     <li>Usando o fluxo de trabalho de tradução de Ativos: Os ativos são tratados de acordo com a configuração das propriedades na guia Ativos.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Executar tradução automaticamente</td>
   <td>Selecione para executar trabalhos de tradução automaticamente após a criação dos projetos de tradução. Você não tem uma oportunidade de revisar e definir o escopo do trabalho de tradução ao selecionar essa opção.</td>
  </tr>
 </tbody>
</table>

### Propriedades de configuração de comunidades {#communities-configuration-properties}

As propriedades das comunidades controlam como a tradução do conteúdo gerado pelo usuário é executada. A tradução de conteúdo gerado pelo usuário sempre usa tradução automática. Para obter mais informações, consulte [Traduzindo conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.

| Propriedade | Descrição |
|---|---|
| Provedor de tradução | Selecione o provedor de tradução para executar a tradução. O provedor para o qual as configurações de nuvem são criadas aparece na lista. |
| Categoria de conteúdo | Uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da formulação ao traduzir o conteúdo. |
| Escolha Uma Localidade Para Usar Como Armazenamento De Compartilhamento Global | (Opcional) Ao selecionar uma localidade para armazenar o UGC, as publicações de todas as cópias de idioma aparecerão em uma conversa global. Por convenção, escolha a localidade para o idioma [](/help/communities/sites-console.md#translation) base do site. Escolher Nenhum armazenamento comum desativará a tradução global. Por padrão, a tradução global está desativada. |

### Propriedades de configuração de ativos {#assets-configuration-properties}

As propriedades de ativos controlam como configurar ativos. Para obter mais informações sobre como traduzir ativos, consulte [Criar cópias de idioma para ativos](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Fluxo de trabalho da conversão</td>
   <td><p>Selecione o tipo de tradução que a estrutura executa para ativos:</p>
    <ul>
     <li>Tradução automática: O provedor de tradução executa a tradução imediatamente usando a tradução automática.</li>
     <li>Tradução humana: O conteúdo é enviado automaticamente para o provedor de tradução para ser traduzido manualmente. </li>
     <li>Não Traduzir: Os ativos não são enviados para conversão.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provedor de tradução</td>
   <td>Selecione o provedor de tradução para executar a tradução. Um provedor é exibido na lista quando seu conector correspondente é instalado.</td>
  </tr>
  <tr>
   <td>Categoria de conteúdo</td>
   <td>(Somente tradução automática) Uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da formulação ao traduzir o conteúdo.</td>
  </tr>
  <tr>
   <td>Converter ativos</td>
   <td>Selecione para incluir ativos no projeto de tradução. </td>
  </tr>
  <tr>
   <td>Traduzir metadados</td>
   <td>Selecione para traduzir os metadados do ativo.</td>
  </tr>
  <tr>
   <td>Traduzir tags</td>
   <td>Selecione para traduzir as tags associadas ao ativo.</td>
  </tr>
  <tr>
   <td>Executar tradução automaticamente</td>
   <td>Selecione para executar trabalhos de tradução automaticamente após a criação dos projetos de tradução. Você não tem uma oportunidade de revisar ou escoar o trabalho de tradução ao selecionar essa opção.</td>
  </tr>
 </tbody>
</table>

1. Na barra lateral, clique ou toque em Ferramentas > Operações > Nuvem > Serviços em nuvem.
1. Na área Integração de tradução, se alguma configuração foi criada, determina qual link será exibido:

   * Se nenhuma configuração tiver sido criada, clique ou toque em Configurar agora.
   * Se as configurações já existirem, clique ou toque em Mostrar configurações e, em seguida, clique ou toque no link + exibido ao lado de Configurações disponíveis.

1. Digite um nome para a configuração e clique ou toque em Criar.
1. Configure as propriedades na guia Sites, Communities e Assets e clique ou toque em OK.

## Configuração de páginas para tradução {#configuring-pages-for-translation}

Para configurar a tradução das páginas de origem para outros idiomas, associe as páginas às seguintes configurações de nuvem:

* A configuração da nuvem que conecta o AEM ao seu provedor de tradução.
* A estrutura de integração da tradução que configura os detalhes da tradução.

Observe que a configuração em nuvem da estrutura de integração de tradução identifica a configuração em nuvem a ser usada para conexão com o provedor de serviço. Quando você associa uma página de origem a uma configuração da estrutura cloud, a página deve ser associada à configuração da nuvem de provedores de serviço que a configuração da estrutura usa.

Quando você associa uma página a uma configuração em nuvem, os descendentes da página herdam a associação. Por exemplo, se você associar a página /content/geometrixx/en/products a uma estrutura de integração de tradução, a página Produtos e todas as páginas abaixo dela serão traduzidas de acordo com a estrutura.

Quando necessário, você pode substituir a associação em uma página descendente. Por exemplo, o conteúdo de um site é principalmente sobre roupas. No entanto, uma ramificação de páginas descreve a empresa. A página raiz do site está associada a uma Estrutura de Integração de Tradução que especifica a tradução automática usando a categoria de Vestuário. A ramificação que descreve a empresa usa uma estrutura que executa a tradução automática usando a categoria Geral.

Além disso, para quaisquer componentes [](/help/communities/scf.md) SCF de comunidades nas páginas, o conteúdo gerado pelo usuário (UGC) incluirá a capacidade de os usuários traduzirem conteúdo. Para obter mais informações, consulte [Tradução de conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.

### Associar uma página a um provedor de tradução {#associating-a-page-with-a-translation-provider}

Associe uma página ao provedor de tradução que você está usando para traduzir a página e as páginas descendentes.

1. No console Sites, selecione a página a ser configurada e clique ou toque em Propriedades da Visualização.
1. Clique ou toque em Editar e, em seguida, clique ou toque na guia Serviços em nuvem.
1. Clique ou toque em Adicionar configuração > Integração de tradução.
1. Selecione o provedor de tradução a ser usado e clique ou toque em Concluído.

### Associar páginas a uma estrutura de integração de tradução {#associating-pages-with-a-translation-integration-framework}

Associe uma página à Estrutura de integração de tradução que define como você deseja executar a tradução da página e das páginas descendentes.

1. No console Sites, selecione a página a ser configurada e clique ou toque em Propriedades da Visualização.
1. Clique ou toque em Editar e, em seguida, clique ou toque na guia Serviços em nuvem.
1. Clique ou toque em Adicionar configuração > Integração de tradução.
1. Selecione a estrutura de integração de tradução a ser usada e clique ou toque em Concluído.

