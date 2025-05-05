---
title: Integração com as práticas recomendadas da Adobe Creative Cloud
description: Práticas recomendadas para integrar [!DNL Adobe Experience Manager] com [!DNL Adobe Creative Cloud] a fim de simplificar os fluxos de trabalho de transferência de ativos e alcançar alta velocidade de conteúdo.
contentOwner: AG
mini-toc-levels: 1
role: User, Admin
feature: Collaboration,Adobe Asset Link,Desktop App
exl-id: c7d589a3-1c5f-4ff0-879e-15e1c556f6dc
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: a144f7cc75b1a5cdb45d2aaf90e87013ac68a431
workflow-type: tm+mt
source-wordcount: '3173'
ht-degree: 11%

---

# Práticas recomendadas de integração do [!DNL Adobe Experience Manager] e do [!DNL Creative Cloud] {#aem-and-creative-cloud-integration-best-practices}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/manage/aem-cc-integration-best-practices) |
| AEM 6.5 | Este artigo |

O [!DNL Adobe Experience Manager Assets] é uma solução de gerenciamento de ativos digitais (DAM) que pode ser integrada ao [!DNL Adobe Creative Cloud] para ajudar os usuários do DAM a trabalhar em conjunto com equipes criativas, simplificando a colaboração no processo de criação de conteúdo.

O [!DNL Adobe Creative Cloud] fornece às equipes criativas um ecossistema de soluções e serviços para ajudá-las a criar ativos digitais. Inclui aplicativos móveis e de desktop, serviços em nuvem, como armazenamento com sincronização de área de trabalho ou experiência da Web, e mercados como o [!DNL Adobe Stock].

Leia para saber quais integrações escolher entre o desktop e o DAM de nível empresarial com base no seu caso de uso e quais são as práticas recomendadas associadas para os fluxos de trabalho de conexão.

>[!NOTE]
>
>O compartilhamento de pastas de [!DNL Experience Manager] para [!DNL Creative Cloud] foi descontinuado e não é mais abordado neste guia. A Adobe recomenda o uso de recursos mais novos, como o [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou o [Experience Manager desktop app](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=pt-BR), para fornecer ao usuário criativo acesso aos ativos gerenciados no [!DNL Experience Manager].

## Necessidades do Collaboration para usuários criativos, profissionais de marketing e DAM {#collaboration-needs-of-creatives-marketers-and-dam-users}

| Requisitos | Caso de uso | Superfícies envolvidas |
|---|---|---|
| Simplifique a experiência para profissionais criativos no desktop | Simplifique o acesso ao ativo a partir de um DAM ([!DNL Experience Manager Assets]) para profissionais de criação ou, de modo mais amplo, usuários no desktop que trabalham em aplicativos nativos de criação de ativos. Eles precisam de uma maneira fácil e direta de descobrir, usar (abrir), editar e salvar alterações no [!DNL Experience Manager] e carregar novos arquivos. | Área de trabalho do Win ou Mac; [!DNL Creative Cloud] aplicativos |
| Forneça ativos prontos para uso de alta qualidade do [!DNL Adobe Stock] | Os profissionais de marketing ajudam a acelerar o processo de criação de conteúdo, auxiliando na origem e descoberta de ativos. Os profissionais criativos usam os ativos aprovados diretamente de suas ferramentas criativas. | [!DNL Experience Manager Assets]; [!DNL Adobe Stock] marketplace; campos de metadados |
| Distribuir e compartilhar ativos por organizações | Departamentos internos/filiais locais e parceiros externos, distribuidores e agências usam os ativos aprovados compartilhados pela organização principal. A organização deseja compartilhar com segurança e perfeição os ativos criados para reutilização mais ampla. | Brand Portal, Asset Share Commons |

## ofertas de Adobe para dar suporte à necessidade de colaboração {#adobe-offerings-to-support-the-collaboration-need}

| Proposta de valor para os perfis envolvidos | oferta de Adobe | Superfícies envolvidas |
|---|---|---|
| Os usuários criativos descobrem ativos de [!DNL Experience Manager], abrem e os usam, editam e carregam alterações em [!DNL Experience Manager] e carregam novos arquivos em [!DNL Experience Manager], sem sair de aplicativos [!DNL Creative Cloud]. | [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) | .[!DNL Adobe Photoshop], [!DNL Adobe Illustrator], e [!DNL Adobe InDesign]. |
| Usuários empresariais simplificam a abertura e o uso de ativos, a edição e o carregamento de alterações no [!DNL Experience Manager] e o carregamento de novos arquivos no [!DNL Experience Manager] a partir do ambiente de desktop. Eles usam uma integração genérica para abrir qualquer tipo de ativo no aplicativo de desktop nativo, incluindo aqueles não-Adobe. | [aplicativo de desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR) | Aplicativo de desktop do [!DNL Experience Manager] nas áreas de trabalho do Win e Mac |
| Profissionais de marketing e usuários empresariais descobrem, visualizam, licenciam e salvam, além de gerenciarem os ativos do [!DNL Adobe Stock] no [!DNL Experience Manager]. Os ativos licenciados e salvos fornecem metadados [!DNL Adobe Stock] selecionados para melhor governança. | [integração com o Experience Manager e o Adobe Stock](aem-assets-adobe-stock.md) | Interface Web do [!DNL Experience Manager] |

Este artigo foca principalmente nos dois primeiros aspectos das necessidades de colaboração. A distribuição e o fornecimento de ativos em escala são brevemente mencionadas como um caso de uso. Para essas necessidades, considere o Adobe Brand Portal ou o Asset Share Commons. Soluções alternativas como [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=pt-BR), soluções que podem ser criadas com base nos componentes [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/), [Link Share](/help/assets/link-sharing.md), usando o [Experience Manager Assets](/help/assets/manage-assets.md) devem ser revisadas com base em requisitos específicos.

![conexões Creative Cloud para Experience Manager, decida qual recurso usar](assets/creative-connections-aem.png)

### Mapeamento de casos de uso e soluções Adobe {#mapping-of-use-cases-and-adobe-solutions}

<!-- TBD: Add some info about XD integration and possibly info about DA v2.0.
-->

| Caso de uso | [!DNL Adobe Asset Link] | Aplicativo de desktop do [!DNL Experience Manager] | Observações/Outras soluções |
|---|---|---|---|
| Descobrir - procurar pastas DAM | Sim | [!DNL Experience Manager] ações de interface da Web e área de trabalho | |
| Descobrir - acessar coleções do DAM | Sim | [!DNL Experience Manager] ações de interface da Web e área de trabalho | |
| Discover — pesquisar ativos no DAM | Sim | [!DNL Experience Manager] ações de interface da Web e área de trabalho | |
| Usar - abrir ativo | Sim | Sim | [Abrir da interface da Web](manage-assets.md#previewing-assets) ou do Localizador |
| Usar - colocar ativo do DAM em um documento | Sim - incorporação | Sim - vinculação ou incorporação | O aplicativo de desktop [!DNL Experience Manager] dá acesso aos ativos como arquivos no sistema de arquivos local. Esses links nos aplicativos nativos são representados por caminhos locais. |
| Editar - abrir para edição | Sim - Ação de check-out | Sim - Abrir ação (no compartilhamento de rede) | O [Check-out no AAL](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) salva o ativo na conta de armazenamento da creative cloud do usuário (sincronizada pelo aplicativo Creative Cloud) por padrão. |
| Editar - trabalho em andamento fora do DAM | Sim - ativo disponível na conta de armazenamento Creative Cloud do usuário sincronizado com o desktop. | Sim | |
| Editar - fazer upload de alterações | Sim - [Ação de check-in](https://helpx.adobe.com/br/enterprise/using/manage-assets-using-adobe-asset-link.html) com comentário opcional | Sim | |
| Upload - único arquivo | Sim - carrega o documento ativo atual | Sim | [Carregar via interface da Web](manage-assets.md#uploading-assets) |
| Upload - vários arquivos/estruturas de pastas hierárquicas | Não | Sim | [Carregar via interface da Web](manage-assets.md#uploading-assets) ou via ferramenta ou script personalizado. |
| Diversos - usuário e logon | O usuário do Creative Cloud conectado ao aplicativo de desktop do Creative Cloud é reconhecido (SSO) | [!DNL Experience Manager] usuário e credenciais | Os usuários de ambas as soluções contam para a cota de usuários [!DNL Experience Manager]. |
| Diversos - rede e acesso | Requer acesso da área de trabalho do usuário à implantação do [!DNL Experience Manager] pela rede | Requer acesso da área de trabalho do usuário à implantação do [!DNL Experience Manager] pela rede | [!DNL Adobe Asset Link] não compartilha o ambiente de proxy de rede. |
| Diversos - Migrar um grande número de ativos | Não | Não | [guia de migração do Assets](assets-migration-guide.md) |

Para dar suporte a casos de uso de distribuição de ativos, outras soluções devem ser consideradas:

* [Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=pt-BR) para obter um complemento SaaS configurável para [!DNL Experience Manager Assets] para publicar ativos.
* As soluções personalizadas são criadas com base no código [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/).
* [!DNL Experience Manager] [compartilhamento de links](/help/assets/link-sharing.md) para compartilhar ativos sob demanda usando links.
* [Interface Web do Experience Manager Assets](/help/assets/manage-assets.md) com áreas para participantes externos protegidas pela configuração de controle de acesso do [!DNL Experience Manager] e com os ajustes necessários de configuração de TI/rede, dando a esses usuários externos acesso ao [!DNL Experience Manager].

## Principais conceitos e casos de uso {#key-concepts-and-use-cases}

### Glossário de termos comuns {#glossary-of-common-terms}

* **Trabalho em andamento ou trabalho criativo em andamento (WIP)**: uma fase no ciclo de vida do ativo em que um ativo sofre várias alterações e normalmente ainda não está pronto para ser compartilhado com equipes maiores.
* **Ativos prontos para criação:** [!DNL Assets] que estão prontos para serem compartilhados com uma equipe maior ou que foram selecionados ou aprovados pela equipe criativa para compartilhamento com equipes de marketing ou LOB.
* **Aprovações de ativos**: o processo de aprovação que executa ativos já carregados no DAM, que normalmente inclui aprovações de marca, legais e assim por diante.
* **Ativo final:** um ativo que passou por todas as aprovações/marcações de metadados e está pronto para ser usado pela equipe maior. Esse ativo é armazenado no DAM e disponibilizado a todos os usuários (ou a todos os interessados). Ele pode ser usado em canais de marketing ou por equipes criativas para criar designs.
* **Atualização/alteração de ativos secundários:** uma pequena e rápida alteração em um ativo digital. Geralmente é feito em resposta a uma solicitação de retoque ou edição secundária, revisão de ativos ou aprovação (por exemplo, reposição, alteração do tamanho do texto, ajuste da saturação/brilho, cor e assim em diante).
* **Atualização/alteração de ativos principais:** uma alteração em um ativo digital que requer trabalho considerável, e às vezes deve ser feita por um período mais longo. Normalmente, inclui várias alterações. O ativo deve ser salvo várias vezes durante a atualização. As atualizações de ativos principais normalmente fazem com que o ativo entre em um estágio WIP.
* **DAM:** Gerenciamento de ativos digitais. Neste documento, ele é sinônimo de [!DNL Experience Manager Assets], a menos que especificamente mencionado o contrário.
* **Usuário criativo**: um profissional criativo, que cria ativos digitais usando aplicativos e serviços da Creative Cloud. Em alguns casos, um usuário criativo pode ser membro de uma equipe criativa que pode usar a Creative Cloud, mas não cria ativos digitais (como um diretor criativo ou gerente de equipe criativa).
* **Usuário do DAM:** um usuário típico de um sistema DAM. Dependendo da organização, um usuário do DAM pode ser um usuário de marketing ou não, por exemplo, um usuário de Linha de Negócios (LOB), um bibliotecário, um vendedor e assim por diante.

### Considerações ao usar a integração [!DNL Experience Manager] e [!DNL Creative Cloud] {#considerations-when-using-aem-and-creative-cloud-integration}

* Consulte as [práticas recomendadas para aplicativos de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/troubleshoot.html?lang=pt-BR#best-practices-to-prevent-troubles)
* Consulte [integração com o Adobe Stock](aem-assets-adobe-stock.md)
* Consulte [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)

Este é um breve resumo das práticas recomendadas para a integração do [!DNL Experience Manager] e do [!DNL Creative Cloud]. Leia o restante deste documento para obter a compreensão detalhada desses itens.

* **Para usuários criativos, que trabalham no Photoshop, no InDesign ou no Illustrator:** O Adobe Asset Link fornece a melhor experiência do usuário, incluindo a manipulação limpa do Trabalho em andamento em ativos tirados do [!DNL Experience Manager].
* **Para simplificar o acesso a ativos do desktop para qualquer formato de arquivo ou aplicativo genérico:** use o aplicativo de desktop [!DNL Experience Manager].
* **Entenda por que e quando armazenar ativos no DAM:** Atualizações a serem disponibilizadas para a equipe maior em sua organização.
* **Considere o volume de ativos compartilhados:** se o caso de uso for a distribuição de ativos, a governança e a segurança podem ser os aspectos mais importantes. Considere usar ferramentas criadas para fazer isso em escala, como o Brand Portal.
* **Entenda o ciclo de vida do ativo:** saiba como os ativos são manipulados em sua organização por equipes diferentes
* **Lidar com salvamentos frequentes em ativos com cuidado:** o Adobe Asset Link cuida disso para você com PS, AI, ID. Para outros aplicativos, não realize tarefas em andamento na pasta mapeada/compartilhada, a menos que precise de todas as alterações no DAM

### Acesso a [!DNL Adobe Stock] ativos a partir de [!DNL Assets] {#access-to-adobe-stock-assets-from-aem-assets}

A [integração com o Experience Manager e o Adobe Stock](/help/assets/aem-assets-adobe-stock.md) fornece aos usuários do [!DNL Experience Manager] a capacidade de pesquisar, visualizar, licenciar e salvar ativos do [!DNL Adobe Stock] para o [!DNL Experience Manager]. [!DNL Stock] ativos licenciados e salvos selecionaram [!DNL Stock] metadados, que podem ser usados para pesquisá-los com filtros extras.

Alguns pontos importantes sobre essa integração:

* Quando os ativos do estoque Adobe são salvos em [!DNL Experience Manager], eles se tornam um [!DNL Assets] normal, com o binário salvo no repositório [!DNL Experience Manager]. Alguns metadados relacionados a [!DNL Adobe Stock] são salvos para o ativo em [!DNL Experience Manager], caso contrário, o processo de assimilação será o mesmo de qualquer outro arquivo. Por exemplo, se as Tags inteligentes estiverem ativas, as tags serão adicionadas a esses ativos ao salvar.
* O ativo salvo em [!DNL Experience Manager] é uma cópia, não um link para [!DNL Adobe Stock].

**Trabalhando com ativos salvos de [!DNL Adobe Stock] em [!DNL Experience Manager] em[!DNL Creative Cloud]**. Essa integração independe do [!DNL Adobe Asset Link], mas o [!DNL Adobe Asset Link] reconhece esses ativos salvos do [!DNL Stock] dessa forma e exibe metadados adicionais e um logotipo do [!DNL Adobe Stock] nesses ativos na interface do usuário da extensão [!DNL Adobe Asset Link] no [!DNL Photoshop], [!DNL Illustrator] ou [!DNL InDesign]. Os arquivos estão disponíveis para navegação, abertura etc., pois eles são ativos comuns quando salvos em [!DNL Experience Manager].
Os usuários criativos que trabalham em aplicativos [!DNL Creative Cloud] com extensão [!DNL Adobe Asset Link] presentes, além de terem acesso a ativos já licenciados do [!DNL Adobe Stock] para o [!DNL Experience Manager], também podem usar o painel Bibliotecas do [!DNL Creative Cloud] para pesquisar, visualizar e licenciar ativos do [!DNL Adobe Stock].
[!DNL Assets] de [!DNL Adobe Stock] licenciados e salvos em [!DNL Experience Manager] ficam disponíveis para as equipes mais amplas que acessam a implantação do [!DNL Experience Manager Assets], enquanto os ativos de licenciamento de criação do [!DNL Adobe Stock] por meio do painel Bibliotecas do [!DNL Creative Cloud] os tornam disponíveis para si mesmos somente por padrão em suas contas do [!DNL Creative Cloud].

<!-- 
TBD: A condensed version of the below content is better placed in the Adobe DAM introduction article.
-->

## Sobre o armazenamento de ativos em um DAM {#about-storing-assets-in-a-dam}

Para projetar um fluxo de trabalho eficiente entre as equipes de criação e marketing/linha de negócios (LOB) e escolher os melhores recursos de suporte, é importante entender quando e por que os ativos são armazenados no DAM.

### Por que os ativos são armazenados no DAM {#why-assets-are-stored-in-dam}

Armazenar ativos no DAM facilita o acesso e a localização. Ele garante que os ativos possam ser usados por vários usuários em toda a organização ou ecossistema, o que inclui parceiros, clientes e assim por diante.

A maioria das organizações opta por armazenar somente ativos que sejam relevantes para os processos de marketing/LOB de downstream (publicação em canais como o canal da Web via [!DNL Experience Manager Sites] ou outros canais atendidos pela Adobe Experience Cloud - Marketing Cloud, Advertising Cloud e medidos pela Analytics Cloud, fornecimento para usuários/parceiros e assim por diante). Além disso, as organizações armazenam ativos que podem estar sujeitos a um processo de revisão/aprovação no DAM. Dessa forma, o DAM armazena principalmente ativos que têm altas chances de serem usados e evita o armazenamento de ativos ociosos.

O armazenamento de ativos também está sujeito a considerações técnicas e de utilização de recursos. O DAM fornece serviços adicionais sobre ativos armazenados, incluindo extração de metadados, controle de versão, geração de visualizações/transcodificação, gerenciamento de referências e adição de informações de controle de acesso. Esses serviços consomem mais tempo e recursos de infraestrutura.

Geralmente, armazenar todos os ativos e atualizações não é desejável. Por exemplo, se as atualizações de ativos específicos forem de baixa qualidade e consumirem recursos excessivos, os ativos podem não ser armazenados no DAM.

#### Quando os ativos são armazenados no DAM {#when-assets-are-stored-in-dam}

As equipes de criação (e organizações) geralmente não estão interessadas em armazenar ativos em cada estágio do ciclo de vida do ativo. Por exemplo, eles evitam armazenar ativos nos seguintes casos:

* Assets que ainda não foram finalizadas ou estão sujeitas a experimentação.
* Assets que não passam no ciclo de revisão criativa/interna da equipe.
* Em comparação ao ativo em questão, a equipe tem melhores candidatos para representar seu trabalho para equipes externas.

Normalmente, as seguintes classes de ativos são armazenadas no DAM:

* Assets que atingiram uma certa maturidade e são considerados prontos para serem compartilhados.
* Assets pré-selecionados pela equipe criativa.
* Formatos de ativos específicos que podem ser usados ou solicitados por marketing, dependendo de um contrato ou contrato específico (por exemplo, arquivos de JPG de arquivos RAW, TIFF/imagens de originais de PSD).

#### Quando as atualizações de ativos são armazenadas no DAM {#when-updates-to-assets-are-stored-in-dam}

Como regra, somente as atualizações de ativos que são relevantes para o conjunto mais amplo de usuários do DAM devem ser armazenadas no DAM. Ele garante que os usuários (marketing e funções semelhantes) vejam apenas as versões relevantes na linha do tempo do ativo DAM.

Normalmente, alterações relacionadas aos principais marcos no ciclo de vida do ativo. Por exemplo, o ativo pronto para marketing inicial ou uma atualização oficial com base na solicitação/revisão fornecida pela equipe criativa deve ser armazenado e ter a versão atualizada no DAM.

A atualização da equipe criativa para análise pela equipe de marketing após uma solicitação de alteração no ativo existente no DAM é um exemplo de atualização relevante. Ele deve ser armazenado e ter sua versão atualizada no DAM para referência adicional ou para reverter para a versão anterior.

Veja a seguir exemplos de atualizações que normalmente não são relevantes:

* Versões anteriores de ativos carregados antes de estarem prontos para revisão de marketing
* Alterações criativas frequentes no ativo na fase de trabalho em andamento antes que as equipes de criação e marketing decidam que o ativo está pronto

### Acesso do usuário ao DAM {#user-access-to-dam}

O [!DNL Assets] oferece suporte a dois tipos de usuários com base em seu acesso à implantação do [!DNL Assets]. Normalmente, os usuários dentro da rede corporativa (firewall) têm acesso direto ao DAM. Outros usuários fora da rede corporativa não teriam acesso direto. O tipo de usuário determina quais integrações podem ser usadas do ponto de vista técnico.

#### Usuários de criação com acesso direto ao DAM {#creative-users-with-direct-access-to-dam}

Normalmente, as equipes de criação internas ou agências/profissionais de criação integrados à rede interna têm acesso à implantação do DAM, incluindo o logon do [!DNL Experience Manager]. O [!DNL Experience Manager] e a infraestrutura de rede podem ser configurados para permitir acesso direto a terceiros - geralmente organizações confiáveis, como agências que trabalham para um cliente - para ter acesso ao [!DNL Experience Manager] pela rede, por exemplo, por meio de VPN ou lista de permissões IP.

Nesses casos, o Adobe Asset Link ou o aplicativo de desktop [!DNL Experience Manager] ajuda a fornecer acesso fácil aos ativos finais/aprovados e permite salvar ativos prontos para criação no DAM.

#### Usuários de criação sem acesso ao DAM {#creative-users-without-access-to-dam}

Agências externas e freelancers sem acesso direto à implantação do DAM podem exigir acesso a ativos aprovados ou adicionar seus novos designs ao DAM.

Use as seguintes estratégias para fornecer acesso aos ativos finais/aprovados:

* Use o aplicativo de desktop se o Asset Link não funcionar.
* Use o [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=pt-BR) para distribuir ativos com segurança para parceiros externos
* Use uma implementação personalizada de um portal de distribuição e fornecimento com base em [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Use o Controle de Acesso configurado no [!DNL Experience Manager] e a infraestrutura de rede necessária (por exemplo, VPN e lista de permissões IP) para conceder a terceiros acesso a uma área dedicada de conteúdo em seu DAM. Eles podem usar a interface da Web do [!DNL Experience Manager] para obter ativos e carregar novo conteúdo para o seu DAM.

#### Trabalho em andamento em ativos de [!DNL Experience Manager] {#work-in-progress-on-assets-from-aem}

Conforme discutido neste documento, é recomendável realizar atualizações importantes nos ativos, às vezes chamadas de trabalho em andamento, sem que todas as edições sejam salvas no arquivo local também sejam carregadas no [!DNL Experience Manager] como alterações. Isso acelera o trabalho de um usuário de desktop, limita a largura de banda de rede usada e mantém a linha do tempo dos ativos limpa e concentrada em atualizações importantes e controladas.

O Adobe Asset Link oferece um bom suporte para este caso de uso:

* Quando usuários em [!DNL Photoshop], [!DNL InDesign] ou [!DNL Illustrator] pretendem editar um arquivo, eles executam uma operação de Check-out no ativo especificado
* O ativo é baixado em segundo plano, é colocado na conta de Creative Cloud dos usuários sincronizada em disco pelo aplicativo de desktop Creative Cloud, e o sinalizador de check-out é alternado em [!DNL Experience Manager] no ativo para minimizar os conflitos de edição
* A partir daí, o usuário trabalha em um arquivo armazenado localmente no local sincronizado e pode continuar trabalhando e salvando as alterações necessárias a qualquer frequência necessária
* Além disso, como o ativo está na conta Creative Cloud, ele também está disponível em outros dispositivos que o usuário pode ter (por exemplo, pode ser aberto ou editado em um aplicativo móvel Creative Cloud dedicado) e pode ser compartilhado com outros usuários Creative Cloud para fins de colaboração.
* Quando o usuário criativo conclui as alterações, ele pode executar uma operação de Check-in nesse arquivo no aplicativo Creative Cloud com um comentário opcional. O ativo correspondente em [!DNL Experience Manager] tem a versão e foi atualizado para com o novo binário. [!DNL Experience Manager] usuários como profissionais de marketing ou usuários de LOB têm acesso a grandes alterações de ativos, ou marcos, por meio da interface do usuário da linha do tempo do ativo [!DNL Experience Manager].

O aplicativo de desktop [!DNL Experience Manager] fornece um compartilhamento de rede para ativos abertos no aplicativo nativo. Por padrão, todas as alterações feitas localmente são carregadas para [!DNL Experience Manager] automaticamente após algum tempo. Com essa configuração, salvamentos frequentes durante a fase de trabalho em andamento seriam carregados para o [!DNL Experience Manager] e teriam suas versões alteradas, criando um grande número de tráfego de rede e possíveis desafios de escalabilidade - sem mencionar as versões desnecessárias do [!DNL Experience Manager].

A abordagem recomendada aqui é usar uma opção no aplicativo de desktop [!DNL Experience Manager] para desativar atualizações automáticas e carregar alterações para ativos no [!DNL Experience Manager] manualmente, usando a ação carregar alterações na interface de status do ativo do aplicativo.

#### Upload em massa para DAM {#bulk-upload-to-dam}

Você pode ter um requisito para carregar simultaneamente um número maior de arquivos no DAM em alguns cenários, por exemplo:

* Carregamento de resultados de sessões de fotos ou projetos maiores
* Upload de ativos fornecidos por agências de criação
* Fazer upload de ativos selecionados de um conjunto maior se a seleção for feita fora do DAM

A descrição se refere ao upload de arquivos operacionalmente (por exemplo, toda semana ou com cada sessão de fotos), como uma parte normal do fluxo de trabalho do usuário do desktop. As migrações de ativos grandes não são contempladas aqui.

Você pode usar os seguintes recursos de upload:

* Para carregar pastas grandes/hierárquicas em massa, use o aplicativo de desktop [!DNL Experience Manager] que fornece a funcionalidade de [carregamento de pasta](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR#upload-and-add-new-assets-to-aem). Também é possível fazer upload de estruturas hierárquicas de pastas. [!DNL Assets] são carregados em segundo plano e, portanto, não estão vinculados a uma sessão do navegador da Web
* Para carregar alguns arquivos de uma única pasta, arraste os arquivos diretamente para a interface da Web ou use a opção Criar na interface da Web do [!DNL Assets].
* Dependendo das necessidades da sua empresa, também é possível usar o carregador personalizado.

#### Gerenciar ativos digitais diretamente do desktop {#managing-digital-assets-directly-from-desktop}

Se você usa Compartilhamentos de Arquivos de Rede para gerenciar ativos digitais, o uso do compartilhamento de rede mapeado pelo aplicativo de desktop [!DNL Experience Manager] pode ser visto como um substituto conveniente. Ao fazer a transição de compartilhamentos de arquivos de rede, a interface da Web do [!DNL Experience Manager] fornece um conjunto avançado de recursos de Gerenciamento de Ativos Digitais que vão muito além do que é possível em um compartilhamento de rede (pesquisa, coleções, metadados, colaboração, visualizações e assim por diante), e o aplicativo de desktop do [!DNL Experience Manager] fornece um link útil para conectar o repositório DAM do lado do servidor com o trabalho no desktop.

Evite usar o aplicativo de desktop [!DNL Experience Manager] para gerenciar ativos diretamente no compartilhamento de rede do [!DNL Assets]. Por exemplo, evite usar o aplicativo de desktop [!DNL Experience Manager] para mover/copiar vários arquivos. Em vez disso, use a interface [!DNL Assets] para arrastar pastas do Finder/Explorer para o compartilhamento de rede ou use o recurso Carregamento de Pasta [!DNL Assets].

#### Migração de ativos {#asset-migration}

Para planejar e executar migrações de ativos do sistema existente para um novo sistema ou para a migração de um grande volume de ativos armazenados em servidores, consulte o [Guia de Migração](/help/assets/assets-migration-guide.md). O aplicativo de desktop [!DNL Experience Manager] e as integrações de [!DNL Experience Manager] com [!DNL Creative Cloud] não oferecem suporte a essas migrações. Devido aos grandes volumes de ativos que serão assimilados e aos requisitos adicionais sobre mapeamento, transformação e assimilação de metadados, as migrações devem ser tratadas usando ferramentas e abordagens diferentes.

>[!MORELIKETHIS]
>
>* [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html)
>* [práticas recomendadas para o aplicativo de desktop do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/archive/best-practices-for-v1.html?lang=pt-BR)
>* [Experience Manager Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/introduction/brand-portal.html?lang=pt-BR)
>* [integração com o Experience Manager e o Adobe Stock](aem-assets-adobe-stock.md)
