---
title: Configuração da estrutura de integração de tradução
seo-title: Configuring the Translation Integration Framework
description: Saiba como configurar a Estrutura de integração de tradução.
seo-description: Learn how to configure the Translation Integration Framework.
uuid: 5ecfe154-732f-4a13-96f8-92f55023c54d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: 200f51ab-f9bf-4989-91af-c3904fc673e5
feature: Language Copy
exl-id: 7562754b-d9fd-441b-8ae5-c7eebe458cef
source-git-commit: e5bdf1218d3b747e2317481a67ae74e7855cda0b
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 2%

---

# Configuração da estrutura de integração de tradução{#configuring-the-translation-integration-framework}

A Estrutura de integração de tradução integra-se aos serviços de tradução de terceiros para orquestrar a tradução de conteúdo AEM.

* Conecte-se ao seu provedor de serviços de tradução.
* Crie uma configuração da Estrutura de integração de tradução.
* Associe as configurações de nuvem com suas páginas.

Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md).

## Conexão com um provedor de serviços de tradução {#connecting-to-a-translation-service-provider}

Crie uma configuração de nuvem que se conecta AEM seu provedor de serviços de tradução. AEM inclui a capacidade de se conectar ao Microsoft Translator por padrão.
Os fornecedores de tradução a seguir fornecem uma implementação da nova API para os Projetos de tradução. Links para saber mais sobre a integração:

* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (Adobe Exchange Premier Partner)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memória](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Palavras-chave](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [Cloud XTM](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)
* [Altlang](https://exchange.adobe.com/experiencecloud.details.90222.altlang.html)
* Microsoft (o Microsoft Translator é pré-instalado no AEM)

>[!NOTE]
>
>Para encontrar a lista mais recente de provedores de tradução automática e humana, consulte estas páginas:
>
>
>* [AEM Tradução Humana](https://www.adobe.com/go/aem-human-translation-connectors)
>* [Tradução AEM Máquina](https://www.adobe.com/go/aem-machine-translation-connectors)
>


Depois de instalar um pacote de conectores, você pode criar uma configuração de nuvem para o conector. Normalmente, você precisa fornecer suas credenciais para autenticação com o serviço de tradução. Para obter informações sobre como adicionar uma configuração de nuvem para o conector do Microsoft Translator, consulte [Integração com o Microsoft Translator](/help/sites-administering/tc-msconf.md).

Você pode criar várias configurações de nuvem para o mesmo conector, se necessário. Por exemplo, crie uma configuração para cada conta ou projeto que você tem com o mesmo fornecedor.

Após configurar uma conexão, você pode criar a configuração da estrutura de integração de tradução que a usa.

## Criar uma configuração de integração de tradução {#creating-a-translation-integration-configuration}

Crie uma configuração de estrutura de integração de tradução para especificar como traduzir o conteúdo. A configuração inclui as seguintes informações:

* Qual provedor de serviços de tradução usar.
* Se a tradução humana ou de máquina deve ser realizada.
* Traduzir outro conteúdo associado a uma página ou ativo, como tags.

Após criar uma configuração de estrutura, associe a configuração de nuvem às páginas que deseja traduzir de acordo com a configuração. Quando o processo de tradução é iniciado, o fluxo de trabalho de tradução continua de acordo com a configuração de estrutura associada.

Quando diferentes seções do seu site tiverem diferentes requisitos de tradução, crie várias configurações de estrutura de acordo. Por exemplo, um site multilíngue inclui cópias em inglês, espanhol e japonês. O proprietário do site usa dois provedores de serviços de tradução diferentes para traduções em espanhol e japonês. Portanto, duas configurações da estrutura são configuradas. Cada configuração usa um provedor de serviço de tradução diferente.

Após configurar uma estrutura de integração de tradução, é possível [associá-lo às páginas](/help/sites-administering/tc-prep.md) que o usem.

**Observação:** Para obter uma visão geral dos recursos de tradução de conteúdo no AEM, consulte [Tradução de conteúdo para sites multilíngues](/help/sites-administering/translation.md).

Uma única configuração da estrutura controla como traduzir o conteúdo da página, o conteúdo da comunidade e os ativos.
![chlimage_1-386](assets/translation-config-65.jpg)

### Propriedades de configuração de sites {#sites-configuration-properties}

As propriedades do Sites controlam como a tradução do conteúdo da página é executada.

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Fluxo de trabalho da conversão</td>
   <td><p>Selecione o método de tradução que a estrutura executa para o conteúdo do site:</p>
    <ul>
     <li>Tradução Automática: O provedor de tradução executa a tradução usando a tradução automática em tempo real.</li>
     <li>Tradução Humana: O conteúdo é enviado ao provedor de tradução para ser traduzido por tradutores. </li>
     <li>Não Traduzir: O conteúdo não é enviado para tradução. Isso é para ignorar determinadas ramificações de conteúdo que não seriam traduzidas, mas poderiam ser atualizadas com o conteúdo mais recente.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provedor de tradução</td>
   <td>Selecione o provedor de tradução para executar a tradução. Um provedor é exibido na lista quando o conector correspondente é instalado.</td>
  </tr>
  <tr>
   <td>Categoria de conteúdo</td>
   <td>(Somente tradução automática) Uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da expressão na tradução do conteúdo.</td>
  </tr>
  <tr>
   <td>Traduzir tags</td>
   <td>Selecione para traduzir tags associadas à página.</td>
  </tr>
  <tr>
   <td>Traduzir ativos da página</td>
   <td><p>Selecione como traduzir ativos que são adicionados aos componentes do sistema de arquivos ou referenciados do Assets:</p>
    <ul>
     <li>Não traduzir: Os ativos da página não são traduzidos.</li>
     <li>Usando o fluxo de trabalho de tradução de Sites : Os ativos são manipulados de acordo com as propriedades de configuração na guia Sites .</li>
     <li>Uso do fluxo de trabalho de tradução de Ativos : Os ativos são manipulados de acordo com a configuração das propriedades na guia Ativos .</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Executar tradução automaticamente</td>
   <td>Selecione para executar tarefas de tradução automaticamente após a criação de projetos de tradução. Você não tem uma oportunidade de revisar e escoar o trabalho de tradução ao selecionar essa opção.</td>
  </tr>
 </tbody>
</table>

### Propriedades de configuração do Communities {#communities-configuration-properties}

As propriedades das comunidades controlam como a tradução do conteúdo gerado pelo usuário é executada. A tradução de conteúdo gerado pelo usuário sempre usa a tradução automática. Para obter mais informações, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).

| Propriedade | Descrição |
|---|---|
| Provedor de tradução | Selecione o provedor de tradução para executar a tradução. O provedor para o qual as configurações de nuvem são criadas aparece na lista. |
| Categoria de conteúdo | Uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da expressão na tradução do conteúdo. |
| Escolha Uma Localidade A Ser Usada Como Loja De Compartilhamento Global | (Opcional) Ao selecionar um local para armazenar o UGC, as publicações de todas as cópias de idioma serão exibidas em uma conversa global. Por convenção, escolha a localidade para [idioma base](/help/communities/sites-console.md#translation) para o site. Escolher Nenhum Armazenamento Comum desativará a tradução global. Por padrão, a tradução global está desativada. |

### Propriedades de configuração de ativos {#assets-configuration-properties}

As propriedades de ativos controlam como configurar ativos. Para obter mais informações sobre a tradução de ativos, consulte [Criação de cópias de idioma para ativos](/help/assets/translation-projects.md).

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>Fluxo de trabalho da conversão</td>
   <td><p>Selecione o tipo de tradução que a estrutura executa para os ativos:</p>
    <ul>
     <li>Tradução Automática: O provedor de tradução executa a tradução imediatamente usando a tradução automática.</li>
     <li>Tradução Humana: O conteúdo é enviado automaticamente para o provedor de tradução para ser traduzido manualmente. </li>
     <li>Não Traduzir: Os ativos não são enviados para tradução.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Provedor de tradução</td>
   <td>Selecione o provedor de tradução para executar a tradução. Um provedor é exibido na lista quando o conector correspondente é instalado.</td>
  </tr>
  <tr>
   <td>Categoria de conteúdo</td>
   <td>(Somente tradução automática) Uma categoria que descreve o conteúdo que você está traduzindo. A categoria pode afetar a escolha da terminologia e da expressão na tradução do conteúdo.</td>
  </tr>
  <tr>
   <td>Converter ativos</td>
   <td>Selecione para incluir ativos no projeto de tradução. </td>
  </tr>
  <tr>
   <td>Traduzir metadados</td>
   <td>Selecione para traduzir metadados de ativos.</td>
  </tr>
  <tr>
   <td>Traduzir tags</td>
   <td>Selecione para traduzir tags associadas ao ativo.</td>
  </tr>
  <tr>
   <td>Executar tradução automaticamente</td>
   <td>Selecione para executar tarefas de tradução automaticamente após a criação de projetos de tradução. Você não tem uma oportunidade de revisar ou escoar o trabalho de tradução ao selecionar essa opção.</td>
  </tr>
 </tbody>
</table>

1. Na barra lateral, clique ou toque em Ferramentas > Operações > Nuvem > Cloud Services.
1. Na área Integração de tradução, se alguma configuração foi criada, determina qual link aparece:

   * Se nenhuma configuração tiver sido criada, clique ou toque em Configurar agora.
   * Se as configurações já existirem, clique ou toque em Mostrar configurações e, em seguida, clique ou toque no link + exibido ao lado de Configurações disponíveis.

1. Digite um nome para a configuração e clique ou toque em Criar.
1. Configure as propriedades na guia Sites, Comunidades e Ativos e clique ou toque em OK.

## Configuração de páginas para tradução {#configuring-pages-for-translation}

Para configurar a tradução das páginas de origem em outros idiomas, associe as páginas às seguintes configurações de nuvem:

* A configuração da nuvem que se conecta AEM seu provedor de tradução.
* A estrutura de integração de tradução que configura os detalhes da tradução.

Observe que a configuração da nuvem da estrutura de integração de tradução identifica a configuração da nuvem a ser usada para conexão com o provedor de serviços. Quando você associa uma página de origem a uma configuração da nuvem de estrutura, a página deve ser associada à configuração da nuvem do provedor de serviços que a configuração da nuvem de estrutura usa.

Quando você associa uma página com uma configuração de nuvem, os descendentes da página herdam a associação. Por exemplo, se você associar a página /content/geometrixx/en/products a uma Estrutura de integração de tradução, a página Produtos e todas as páginas abaixo dela serão traduzidas de acordo com a estrutura.

Quando necessário, é possível substituir a associação em uma página descendente. Por exemplo, o conteúdo de um site é principalmente sobre roupas. No entanto, um ramo de páginas descreve a empresa. A página raiz do site está associada a uma Estrutura de integração de tradução que especifica a tradução automática usando a categoria Vestuário. A ramificação que descreve a empresa usa uma estrutura que executa a tradução automática usando a categoria Geral .

Além disso, para qualquer comunidade [Componentes do SCF](/help/communities/scf.md) nas páginas, o conteúdo gerado pelo usuário (UGC) incluirá a capacidade dos usuários de traduzir conteúdo. Para obter mais informações, consulte [Tradução do conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).

### Associar uma página a um provedor de tradução {#associating-a-page-with-a-translation-provider}

Associe uma página ao provedor de tradução que você está usando para traduzir a página e as páginas descendentes.

1. No console Sites, selecione a página que será configurada e clique ou toque em Propriedades da exibição.
1. Clique ou toque em Editar e em ou toque na guia Cloud Services.
1. Clique ou toque em Adicionar configuração > Integração de tradução.
1. Selecione o provedor de tradução a ser usado e clique ou toque em Concluído.

### Associar páginas a uma estrutura de integração de tradução {#associating-pages-with-a-translation-integration-framework}

Associe uma página à Estrutura de integração de tradução que define como você deseja executar a tradução da página e das páginas descendentes.

1. No console Sites, selecione a página que será configurada e clique ou toque em Propriedades da exibição.
1. Clique ou toque em Editar e em ou toque na guia Cloud Services.
1. Clique ou toque em Adicionar configuração > Integração de tradução.
1. Selecione a estrutura de integração de tradução a ser usada e clique ou toque em Concluído.
