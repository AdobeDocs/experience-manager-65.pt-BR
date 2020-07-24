---
title: Práticas recomendadas de integração [!DNL Adobe Experience Manager] e da Adobe Creative Cloud.
description: Práticas recomendadas para [!DNL Adobe Experience Manager] with [!DNL Adobe Creative Cloud] integrar-se para dinamizar os workflows de transferência de ativos e alcançar alta velocidade de conteúdo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '3262'
ht-degree: 17%

---


# [!DNL Adobe Experience Manager] e as práticas recomendadas de [!DNL Creative Cloud] integração {#aem-and-creative-cloud-integration-best-practices}

[!DNL Adobe Experience Manager Assets] é uma solução de gerenciamento de ativos digitais (DAM) que pode ser integrada [!DNL Adobe Creative Cloud] para ajudar os usuários do DAM a trabalharem em conjunto com as equipes criativas, simplificando a colaboração no processo de criação de conteúdo.

[!DNL Adobe Creative Cloud] fornece às equipes criativas um ecossistema de soluções e serviços para ajudá-las a criar ativos digitais. Inclui aplicativos para desktop e dispositivos móveis, serviços em nuvem como armazenamento com sincronização de desktop ou experiência na Web, bem como mercados como [!DNL Adobe Stock]o.

Leia para saber quais integrações escolher entre desktop e DAM de nível corporativo com base no caso de uso e quais são as práticas recomendadas associadas para os workflows de conexão.

>[!NOTE]
>
>[!DNL Experience Manager] o compartilhamento de [!DNL Creative Cloud] pastas está obsoleto e não é mais abordado neste guia. A Adobe recomenda usar recursos mais recentes, como o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou o aplicativo [de desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html) Experience Manager, para fornecer ao usuário criativo acesso aos ativos gerenciados no [!DNL Experience Manager].

## Necessidades de colaboração de criativos, profissionais de marketing e usuários de DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superfícies envolvidas |
|---|---|---|
| Simplifique a experiência de profissionais de criação em desktop | Simplifique o acesso a ativos de um DAM ([!DNL Experience Manager Assets]) para profissionais criativos, ou, mais amplamente, para usuários de desktop que trabalham em aplicativos nativos de criação de ativos. Eles precisam de uma maneira fácil e direta de descobrir, usar (abrir), editar e salvar alterações em [!DNL Experience Manager]e fazer upload de novos arquivos. | Ambiente de trabalho Win ou Mac; [!DNL Creative Cloud] aplicativos |
| Fornecer ativos prontos para uso de alta qualidade de [!DNL Adobe Stock] | Os profissionais de marketing ajudam a acelerar o processo de criação de conteúdo auxiliando na seleção de fontes e na descoberta de ativos. Profissionais criativos usam os ativos aprovados diretamente de suas ferramentas criativas. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] mercado; campos de metadados |
| Distribuir e compartilhar ativos por organizações | Os departamentos internos/locais e parceiros externos, distribuidores e agências usam os ativos aprovados compartilhados pela organização-mãe. A organização deseja compartilhar com segurança e facilidade os ativos criados para uma reutilização mais ampla. | Portal de marcas, Commons de compartilhamento de ativos |

## Ofertas da Adobe para dar suporte à necessidade de colaboração {#adobe-offerings-to-support-the-collaboration-need}

| Proposta de valor para as pessoas envolvidas | Oferta da Adobe | Superfícies envolvidas |
|---|---|---|
| Os usuários da Creative Cloud descobrem ativos de [!DNL Experience Manager], abrem e usam, editam e carregam alterações para [!DNL Experience Manager]e também carregam novos arquivos [!DNL Experience Manager], sem sair dos [!DNL Creative Cloud] aplicativos. | [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) | [!DNL Adobe Photoshop], [!DNL Adobe Illustrator]e [!DNL Adobe InDesign]. |
| Os usuários empresariais simplificam a abertura e o uso de ativos, a edição e o upload de alterações para [!DNL Experience Manager]e o upload de novos arquivos para o ambiente [!DNL Experience Manager] de desktop. Eles usam uma integração genérica para abrir qualquer tipo de ativo no aplicativo de desktop nativo, incluindo os que não são da Adobe. | [aplicativo de desktop Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | [!DNL Experience Manager] aplicativo desktop no desktop Win e Mac |
| Os profissionais de marketing e os usuários empresariais descobrem, pré-visualizações, licenciam e salvam e gerenciam os [!DNL Adobe Stock] ativos de dentro [!DNL Experience Manager]. Os ativos licenciados e salvos fornecem metadados selecionados [!DNL Adobe Stock] para melhor governança. | [Integração com o Experience Manager e o Adobe Stock](aem-assets-adobe-stock.md) | [!DNL Experience Manager] interface da Web |

Este artigo foca principalmente nos dois primeiros aspectos das necessidades de colaboração. A distribuição e o fornecimento de ativos em escala são brevemente mencionadas como um caso de uso. Para essas necessidades, considere o Adobe Brand Portal ou o Asset Share Commons. Alternate solutions such as [Brand Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/home.html), solutions that can be built based on [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) components, [Link Share](/help/assets/link-sharing.md), using [Experience Manager Assets](/help/assets/managing-assets-touch-ui.md) should be reviewed based on specific requirement.

![Conexões da Creative Cloud para Experience Manager, decida qual recurso usar](assets/creative-connections-aem.png)

### Mapeamento de casos de uso e soluções da Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso de uso  | [!DNL Adobe Asset Link] | [!DNL Experience Manager] aplicativo para desktop | Observações / Outras soluções |
|---|---|---|---|
| Discover - procurar pastas DAM | Sim | [!DNL Experience Manager] Interface da Web e ações da área de trabalho |  |
| Discover - acessar coleções de DAM | Sim | [!DNL Experience Manager] Interface da Web e ações da área de trabalho |  |
| Discover - pesquisar ativos do DAM | Sim | [!DNL Experience Manager] Interface da Web e ações da área de trabalho |  |
| Usar - ativo aberto | Sim | Sim | [Abrir da interface](managing-assets-touch-ui.md#previewing-assets) da Web ou do Finder |
| Usar - colocar o ativo do DAM em um documento | Sim - incorporação | Sim - vinculação ou incorporação | [!DNL Experience Manager] o aplicativo desktop dá acesso aos ativos como arquivos no sistema de arquivos local. Esses links nos aplicativos nativos são representados por caminhos locais. |
| Editar - abrir para edição | Sim - Ação de check-out | Sim - ação de abertura (no compartilhamento de rede) | [O check-out no AAL](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) salva o ativo na conta do armazenamento da Creative Cloud do usuário (sincronizada pelo aplicativo da Creative Cloud) por padrão. |
| Editar - trabalho em andamento fora do DAM | Sim - Ativo disponível na conta do armazenamento da Creative Cloud do usuário sincronizada ao desktop. | Sim |  |
| Editar - carregar alterações | Sim - ação [de](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) check-in com comentário opcional | Sim |  |
| Carregar - único arquivo | Sim - carrega o documento ativo atual | Sim | [Fazer upload por meio da interface da Web](managing-assets-touch-ui.md#uploading-assets) |
| Carregar - vários arquivos / estruturas hierárquicas de pastas | Não | Sim | [Faça upload pela interface](managing-assets-touch-ui.md#uploading-assets) da Web ou por meio de scripts ou ferramentas personalizados. |
| Misc - usuário e login | O usuário da Creative Cloud conectado ao aplicativo de desktop da Creative Cloud é reconhecido (SSO) | [!DNL Experience Manager] usuário e credenciais | Os usuários de ambas as soluções contam para a cota de [!DNL Experience Manager] usuários. |
| Diversos - rede e acesso | Requer acesso da área de trabalho do usuário à [!DNL Experience Manager] implantação pela rede | Requer acesso da área de trabalho do usuário à [!DNL Experience Manager] implantação pela rede | [!DNL Adobe Asset Link] não compartilha o ambiente proxy de rede. |
| Diversos - Migrar um grande número de ativos | Não | Não | [Guia de migração de ativos](assets-migration-guide.md) |

Para suportar casos de uso de distribuição de ativos, outras soluções devem ser consideradas:

* [Portal](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/home.html) da marca para um complemento SaaS configurável para [!DNL Experience Manager Assets] publicar ativos.
* As soluções personalizadas são criadas com base na base de código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* [!DNL Experience Manager] [compartilhamento](/help/assets/link-sharing.md) de link para compartilhar ativos ad hoc usando links.
* [interface](/help/assets/managing-assets-touch-ui.md) da Web do Experience Manager Assets com áreas para terceiros externos protegidas pela configuração do [!DNL Experience Manager] controle de acesso e com os ajustes necessários de configuração de TI/rede, dando a esses usuários externos acesso [!DNL Experience Manager].

## Conceitos-chave e casos de uso {#key-concepts-and-use-cases}

### Glossário de termos comuns {#glossary-of-common-terms}

* **Trabalho em andamento ou trabalho criativo em andamento (WIP)**: uma fase no ciclo de vida do ativo em que um ativo sofre várias alterações e normalmente ainda não está pronto para ser compartilhado com equipes maiores.
* **Ativos prontos para criação:** [!DNL Assets] que estejam prontos para serem compartilhados com uma equipe mais ampla ou que tenham sido selecionados ou aprovados pela equipe criativa para compartilhamento com equipes de marketing ou LOB.
* **Aprovações de ativos**: o processo de aprovação que executa ativos já carregados no DAM, que normalmente inclui aprovações de marca, legais e assim por diante.
* **Ativo final**: um ativo que passou por todas as aprovações/marcações de metadados e está pronto para ser usado pela equipe maior. Esse ativo é armazenado no DAM e disponibilizado a todos os usuários (ou a todos os interessados). Ele pode ser usado em canais de marketing ou por equipes criativas para criar designs.
* **Atualização/alteração de ativos secundários:** uma pequena e rápida mudança em um ativo digital. Geralmente é feito em resposta a uma solicitação de retoque ou edição secundária, revisão de ativos ou aprovação (por exemplo, reposição, alteração do tamanho do texto, ajuste da saturação/brilho, cor e assim em diante).
* **Atualizações/alterações de ativos principais:** uma mudança em um ativo digital que requer trabalho considerável, e às vezes deve ser feita por um período mais longo. Normalmente, inclui várias alterações. O ativo deve ser salvo várias vezes durante a atualização. As atualizações de ativos principais normalmente fazem com que o ativo entre em um estágio WIP.
* **DAM:** Gerenciamento de ativos digitais. In this document, it is synonymous with [!DNL Experience Manager Assets], unless specifically mentioned otherwise.
* **Usuário criativo**: um profissional criativo, que cria ativos digitais usando aplicativos e serviços da Creative Cloud. Em alguns casos, um usuário criativo pode ser membro de uma equipe criativa que pode usar a Creative Cloud, mas não cria ativos digitais (como um diretor criativo ou gerente de equipe criativa).
* **Usuário do DAM:** um usuário típico de um sistema DAM. Dependendo da organização, um usuário do DAM pode ser um usuário de marketing ou não, por exemplo, um usuário de Linha de Negócios (LOB), um bibliotecário, um vendedor e assim por diante.

### Considerações ao usar [!DNL Experience Manager] e [!DNL Creative Cloud] integração {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulte Práticas recomendadas de aplicativos [para desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/troubleshoot.html#best-practices-to-prevent-troubles)
* Consulte Integração [do Adobe Stock](aem-assets-adobe-stock.md)
* Consulte Link de ativos [da Adobe](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)

Este é um breve resumo das práticas recomendadas para [!DNL Experience Manager] e [!DNL Creative Cloud] integração. Leia o resto deste documento para entender os detalhes.

* **Para usuários criativos, que trabalham no Photoshop, InDesign ou Illustrator:** o do Adobe Asset Link fornece a melhor experiência do usuário, incluindo a manipulação limpa do Trabalho em andamento em ativos tirados do [!DNL Experience Manager].
* **Para simplificar o acesso a ativos do desktop para qualquer formato de arquivo ou aplicativo genérico:** use o aplicativo [!DNL Experience Manager] para desktop.
* **Entenda por que e quando armazenar ativos no DAM:** atualizações a serem disponibilizadas para a equipe maior em sua organização.
* **Considere o volume de ativos compartilhados:** se o caso de uso for a distribuição de ativos, a governança e a segurança podem ser os aspectos mais importantes. Considere usar ferramentas criadas para fazer isso em escala, como o Brand Portal.
* **Entenda o ciclo de vida do ativo:** saiba como os ativos são manipulados em sua organização por equipes diferentes
* **Lidar com salvamentos frequentes em ativos com cuidado:** o Adobe Asset Link cuida disso para você com PS, AI, ID. Em outros aplicativos, não realize tarefas em andamento na pasta mapeada/compartilhada, a menos que precise de todas as alterações no DAM

### Acesso a [!DNL Adobe Stock] ativos de [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

[A integração](/help/assets/aem-assets-adobe-stock.md) do Experience Manager e do Adobe Stock fornece aos [!DNL Experience Manager] usuários a capacidade de pesquisar, pré-visualização, licenciar e salvar ativos de [!DNL Adobe Stock] dentro [!DNL Experience Manager]. Os ativos licenciados e salvos [!DNL Stock] têm [!DNL Stock] metadados selecionados, que podem ser usados para pesquisá-los com filtros extras.

Alguns pontos importantes sobre essa integração:

* Quando os ativos do Adobe Stock são salvos em [!DNL Experience Manager], eles se tornam regulares [!DNL Assets], com o binário salvo no [!DNL Experience Manager] repositório. Alguns metadados relacionados a [!DNL Adobe Stock] são salvos para o ativo em [!DNL Experience Manager], caso contrário, o processo de ingestão terá a mesma aparência de qualquer outro arquivo. Por exemplo, se as Tags inteligentes estiverem ativas, as tags serão adicionadas a esses ativos ao salvar.
* O ativo salvo [!DNL Experience Manager] é uma cópia, não um link de volta para [!DNL Adobe Stock].

**Trabalhar com ativos salvos de[!DNL Adobe Stock]em[!DNL Experience Manager]em[!DNL Creative Cloud]**. Essa integração é independente[!DNL Adobe Asset Link], mas[!DNL Adobe Asset Link]reconhece esses ativos salvos dessa[!DNL Stock]maneira, e exibe metadados adicionais e um[!DNL Adobe Stock]logotipo nesses ativos na[!DNL Adobe Asset Link]extensão da interface do usuário em[!DNL Photoshop],[!DNL Illustrator]ou[!DNL InDesign]. Os arquivos estão disponíveis para navegação, abertura e assim por diante - porque são ativos comuns quando salvos em[!DNL Experience Manager].
Os usuários criativos que trabalham em[!DNL Creative Cloud]aplicativos com[!DNL Adobe Asset Link]extensão presentes, além de terem acesso a ativos já licenciados[!DNL Adobe Stock]de dentro[!DNL Experience Manager], também podem usar o painel[!DNL Creative Cloud]Bibliotecas para pesquisar, pré-visualização e licenciar ativos[!DNL Adobe Stock].[!DNL Assets]de[!DNL Adobe Stock]licenciados e salvos em[!DNL Experience Manager]tornam-se disponíveis para as equipes mais amplas que acessam a[!DNL Experience Manager Assets]implantação, enquanto os ativos de licenciamento de criativos[!DNL Adobe Stock]por meio do painel[!DNL Creative Cloud]Bibliotecas os disponibilizam somente para elas próprias por padrão em suas[!DNL Creative Cloud]contas.

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Sobre o armazenamento de ativos em um DAM {#about-storing-assets-in-a-dam}

Para projetar um fluxo de trabalho eficiente entre equipes de criação e marketing/linha de negócios (LOB) e escolher os melhores recursos de suporte, é importante entender quando e por que os ativos são armazenados no DAM.

### Por que os ativos são armazenados no DAM {#why-assets-are-stored-in-dam}

Armazenar ativos no DAM os torna facilmente acessíveis e acessíveis. Ela garante que os ativos possam ser aproveitados por vários usuários em toda a organização ou ecossistema, o que inclui parceiros, clientes e assim por diante.

A maioria das organizações escolhe armazenar apenas ativos relevantes para os processos de marketing/LOB de downstream (publicação em canais como canal da Web por meio [!DNL Experience Manager Sites] ou outros canais fornecidos pela Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e medidos pela Analytics Cloud, fornecendo a usuários/parceiros e assim por diante). Além disso, as organizações armazenam ativos que podem estar sujeitos a um processo de revisão/aprovação no DAM. Dessa forma, o DAM armazena principalmente ativos que têm grandes chances de serem aproveitados e evita armazenar ativos ociosos.

Armazenar ativos também está sujeito a considerações técnicas e de utilização de recursos. O DAM fornece serviços adicionais sobre ativos armazenados, incluindo extração de metadados, controle de versão, geração de pré-visualizações/transcodificação, gerenciamento de referências e adição de informações de controle de acesso. Esses serviços consomem mais tempo e recursos de infraestrutura.

Geralmente, armazenar todos os ativos e atualizações não é desejável. Por exemplo, se as atualizações de ativos específicos forem de baixa qualidade e consumirem recursos excessivos, os ativos podem não ser armazenados no DAM.

#### Quando os ativos são armazenados no DAM {#when-assets-are-stored-in-dam}

Geralmente, as equipes criativas (e organizações) não estão interessadas em armazenar ativos em cada estágio do ciclo de vida do ativo. Por exemplo, eles evitam armazenar ativos nos seguintes casos:

* Ativos que ainda não foram finalizados ou estão sujeitos a experimentação.
* Os ativos que não passam no ciclo de análise da equipe interna/criativa.
* Em comparação com o ativo em questão, a equipe tem melhores candidatos para representar seu trabalho para equipes externas.

Normalmente, os seguintes ativos de classes são armazenados no DAM:

* Ativos que atingiram um determinado prazo de vencimento e que são considerados prontos para serem partilhados.
* Ativos pré-selecionados pela equipe criativa.
* Formatos de ativos específicos que são utilizáveis ou solicitados pelo marketing, dependendo de um contrato ou contrato específico (por exemplo, arquivos JPG convertidos de arquivos RAW, TIFFs/imagens de originais PSD).

#### Quando as atualizações de ativos são armazenadas no DAM {#when-updates-to-assets-are-stored-in-dam}

Como regra, somente as atualizações de ativos relevantes para o conjunto mais amplo de usuários do DAM devem ser armazenadas no DAM. Ela garante que os usuários (marketing e funções semelhantes) visualizem somente as versões relevantes na linha do tempo do ativo DAM.

Normalmente, as alterações estão relacionadas aos principais marcos no ciclo de vida do ativo. Por exemplo, o ativo pronto para marketing ou uma atualização oficial com base na solicitação/revisão fornecida pela equipe criativa deve ser armazenado e controle de versão no DAM.

A atualização da equipe criativa para revisão pela equipe de marketing após uma solicitação de alteração no ativo existente no DAM é um exemplo de uma atualização relevante. Ele deve ser armazenado e controle de versão no DAM para referência adicional ou para reverter para a versão anterior.

A seguir estão exemplos de atualizações que normalmente não são relevantes:

* Versões antecipadas de ativos carregados antes de estarem prontos para a revisão de marketing
* Alterações criativas frequentes no ativo na fase de trabalho em andamento antes que as equipes de criação e marketing decidam que o ativo está pronto

### Acesso do usuário ao DAM {#user-access-to-dam}

[!DNL Assets] oferece suporte a dois tipos de usuários com base em seu acesso à [!DNL Assets] implantação. Normalmente, os usuários dentro da rede corporativa (firewall) têm acesso direto ao DAM. Outros usuários fora da rede corporativa não teriam acesso direto. O tipo de usuário determina quais integrações podem ser usadas do ponto de vista técnico.

#### Usuários criativos com acesso direto ao DAM {#creative-users-with-direct-access-to-dam}

Geralmente, equipes de criação interna ou agências/profissionais de criação integrados à rede interna têm acesso à implantação do DAM, incluindo [!DNL Experience Manager] logon. [!DNL Experience Manager] e a infraestrutura de rede pode ser configurada para permitir o acesso direto a partes externas - normalmente organizações confiáveis, como agências que trabalham para um cliente - para ter acesso à rede, por exemplo via VPN ou lista de permissões IP. [!DNL Experience Manager]

Nesses casos, o Adobe Asset Link ou o aplicativo de desktop ajuda a fornecer acesso fácil aos ativos finais/aprovados e permite salvar ativos prontos para criação no DAM. [!DNL Experience Manager]

#### Usuários criativos sem acesso ao DAM {#creative-users-without-access-to-dam}

Agências externas e freelancers sem acesso direto à implantação do DAM podem exigir acesso a ativos aprovados ou podem adicionar seus novos designs ao DAM.

Use as seguintes estratégias para fornecer acesso aos ativos finais/aprovados:

* Use o aplicativo desktop se o Link de ativo não funcionar.
* Use o Portal [de marcas dos ativos](https://docs.adobe.com/content/help/br/experience-manager-brand-portal/using/home.html) Experience Manager para distribuir ativos com segurança a parceiros externos
* Usar uma implementação personalizada de um portal de distribuição e seleção de fornecedor com base no [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use a configuração de Controles de acesso em uma infraestrutura de rede [!DNL Experience Manager] necessária (por exemplo, VPN e lista de permissões IP) para dar a terceiros acesso a uma área de conteúdo dedicada no seu DAM. Eles podem usar a interface do usuário [!DNL Experience Manager] da Web para obter ativos e carregar novo conteúdo no DAM.

#### Trabalhos em andamento em ativos de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Conforme discutido neste documento, é recomendável realizar atualizações importantes em ativos, às vezes chamados de trabalhos em andamento, sem ter todas as edições salvas no arquivo local também carregadas [!DNL Experience Manager] como alterações. Isso acelera o trabalho de um usuário do desktop, limita a largura de banda da rede usada e mantém a linha do tempo dos ativos limpos e focados em atualizações importantes e controladas.

O Adobe Asset Link oferta um bom suporte para este caso de uso:

* Quando os usuários entram, [!DNL Photoshop]ou [!DNL InDesign][!DNL Illustrator] pretendem editar um arquivo, eles executam uma operação de Check-out no ativo em questão
* O ativo é baixado em segundo plano, colocado em uma conta da Creative Cloud de usuários sincronizada ao disco pelo aplicativo de desktop da Creative Cloud e o sinalizador de check-out é alternado [!DNL Experience Manager] no ativo para minimizar conflitos de edição
* A partir daí, o usuário trabalha em um arquivo armazenado localmente no local sincronizado e pode continuar trabalhando e salvando as alterações necessárias a qualquer frequência necessária
* Além disso, como o ativo está na conta da Creative Cloud, ele também está disponível em outros dispositivos que o usuário pode ter (por exemplo, pode ser aberto ou editado em um aplicativo dedicado da Creative Cloud para dispositivos móveis) e pode ser compartilhado com outros usuários da Creative Cloud para fins de colaboração.
* Quando o usuário criativo terminar com as alterações, ele poderá executar uma operação de Check-in no arquivo em seu aplicativo da Creative Cloud, com um comentário opcional. O ativo correspondente em [!DNL Experience Manager] é controlado e atualizado com o novo binário. [!DNL Experience Manager] usuários como profissionais de marketing ou LOB têm acesso às principais alterações de ativos, ou marcos, por meio da interface do usuário da linha do tempo [!DNL Experience Manager] do ativo.

[!DNL Experience Manager] o aplicativo desktop fornece um compartilhamento de rede para ativos abertos no aplicativo nativo. Por padrão, todas as alterações feitas localmente são carregadas para [!DNL Experience Manager] automaticamente após algum tempo. Com tal configuração, salvas frequentes durante a fase de trabalho em andamento seriam todos carregadas para a versão [!DNL Experience Manager] e controle de versão, criando muito tráfego de rede e possíveis desafios de escalabilidade - para não mencionar versões desnecessárias na [!DNL Experience Manager].

A abordagem recomendada aqui é usar uma opção no aplicativo para [!DNL Experience Manager] desktop para desativar atualizações automatizadas e fazer upload das alterações nos ativos [!DNL Experience Manager] manualmente, aproveitando a ação de upload de alterações na interface do usuário do Status do ativo do aplicativo.

#### Carregamento em massa para DAM {#bulk-upload-to-dam}

Você pode ter a necessidade de carregar simultaneamente um número maior de arquivos no DAM em alguns cenários, por exemplo:

* Carregar resultados de fotografias ou projetos maiores
* Fazer upload de ativos fornecidos por agências criativas
* Carregar ativos selecionados de um conjunto maior se a seleção for feita fora do DAM

A descrição refere-se ao upload de arquivos operacionalmente (por exemplo, toda semana ou com cada fotografia), como uma parte normal do fluxo de trabalho do usuário do desktop. As migrações de grandes ativos não são abordadas aqui.

Você pode aproveitar os seguintes recursos de upload:

* Para fazer upload de pastas grandes/hierárquicas em massa, use o aplicativo de área de trabalho [!DNL Experience Manager] que oferece a funcionalidade de upload [de](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#bulk-upload-assets) pastas. Você também pode carregar estruturas hierárquicas de pastas. [!DNL Assets] são carregados em segundo plano e, portanto, não estão vinculados a uma sessão do navegador da Web
* Para carregar alguns arquivos de uma única pasta, arraste os arquivos diretamente para a interface da Web ou use a opção Criar na interface da [!DNL Assets] Web.
* Dependendo dos requisitos de sua empresa, você também pode usar o carregador personalizado.

#### Gerenciar ativos digitais diretamente do desktop {#managing-digital-assets-directly-from-desktop}

Se você usar Compartilhamentos de arquivos de rede para gerenciar ativos digitais, o uso do compartilhamento de rede mapeado pelo aplicativo de [!DNL Experience Manager] desktop pode ser visto como um substituto conveniente. Ao fazer a transição dos compartilhamentos de arquivos de rede, a interface da Web fornece um conjunto avançado de recursos de Gerenciamento de ativos digitais que vão muito além do que é possível em um compartilhamento de rede (pesquisa, coleções, metadados, colaboração, pré-visualizações e assim por diante), e o aplicativo de desktop fornece um link útil para conectar o repositório DAM do lado do servidor ao trabalho no desktop. [!DNL Experience Manager] [!DNL Experience Manager]

Evite usar o aplicativo [!DNL Experience Manager] desktop para gerenciar ativos diretamente no compartilhamento de rede do [!DNL Assets]. Por exemplo, evite usar o aplicativo de [!DNL Experience Manager] desktop para mover/copiar vários arquivos. Em vez disso, use a [!DNL Assets] interface para arrastar pastas do Finder/Explorer para o compartilhamento de rede ou use o recurso de Upload de [!DNL Assets] pasta.

#### Migração de ativos {#asset-migration}

Para planejar e executar migrações de ativos do sistema existente para um novo sistema ou migração de um grande volume de ativos armazenados em servidores, consulte o Guia [de](/help/assets/assets-migration-guide.md)Migração. [!DNL Experience Manager] aplicativos de desktop e [!DNL Experience Manager] para [!DNL Creative Cloud] integrações não suportam essas migrações. Devido aos grandes volumes de ativos a serem ingeridos e aos requisitos adicionais em torno do mapeamento, transformação e ingestão de metadados, as migrações devem ser tratadas usando diferentes ferramentas e abordagens.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* [Práticas recomendadas de aplicativos para desktop Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/archive/best-practices-for-v1.html)
>* [Portal da marca Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/introduction/brand-portal.html)
>* [Integração com o Experience Manager e o Adobe Stock](aem-assets-adobe-stock.md)

