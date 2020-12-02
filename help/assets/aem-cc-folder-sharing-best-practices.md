---
title: Compartilhamento de pasta para  [!DNL Adobe Creative Cloud] práticas recomendadas
description: Configure [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] para trocar pastas com usuários do Adobe Creative Cloud (CC).
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---


# [!DNL Adobe Experience Manager] para compartilhamento de  [!DNL Adobe Creative Cloud] pastas  {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O recurso [!DNL Experience Manager] para [!DNL Creative Cloud] Compartilhamento de pasta está obsoleto. O Adobe recomenda usar recursos mais recentes, como [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou [aplicativo de desktop Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Saiba mais sobre as práticas recomendadas de integração [Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] pode ser configurado para permitir que os usuários compartilhem pastas  [!DNL Assets] com os usuários dos  [!DNL Adobe Creative Cloud] aplicativos, de modo que eles estejam disponíveis como pastas compartilhadas no serviço de  [!DNL Adobe Creative Cloud] ativos. O recurso pode ser usado para trocar arquivos entre equipes de criação e usuários [!DNL Assets], especialmente quando os usuários de criação não têm acesso à implantação [!DNL Assets] (eles não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto a [!DNL Assets]:

* [!DNL Assets] os usuários compartilham um conjunto de ativos digitais específicos com usuários de  [!DNL Adobe Creative Cloud] arquivos (por exemplo, um resumo criativo e um conjunto de ativos aprovados para o trabalho de design de uma nova atividade de marketing).
* [!DNL Assets] os usuários recebem novos arquivos criados pelos usuários do  [!DNL Adobe Creative Cloud] aplicativo.

>[!NOTE]
>
>Antes de ler este documento, você pode consultar as práticas recomendadas gerais de integração de Experience Manager e Creative Cloud para obter uma visão geral da integração.[](/help/assets/aem-cc-integration-best-practices.md)

## Visão geral {#overview}

[!DNL Experience Manager] o compartilhamento de  [!DNL Creative Cloud] pastas depende do compartilhamento de pastas e arquivos entre  [!DNL Assets] e  [!DNL Creative Cloud] contas pelo lado do servidor. Os profissionais criativos, que usam o [!DNL Creative Cloud] aplicativo desktop em seus desktops, podem disponibilizar as pastas compartilhadas diretamente em seus discos usando a tecnologia [!DNL Adobe CreativeSync].

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **[!DNL Experience Manager Assets]** implantado na rede corporativa (serviços gerenciados ou no local): O compartilhamento de pastas é iniciado aqui.
* **[!DNL Adobe Marketing Cloud Assets]serviço** principal: Atua como intermediário entre serviços  [!DNL Experience Manager] e serviços  [!DNL Creative Cloud] armazenamentos. Um administrador de uma organização que usa a integração precisa estabelecer uma relação de confiança entre a organização do Marketing Cloud e a implantação [!DNL Assets]. Eles também [definem uma lista de colaboradores aprovados do Creative Cloud](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que [!DNL Assets] os usuários também podem compartilhar pastas para obter segurança adicional.

* **[!DNL Creative Cloud]Serviços**  da Web de ativos (interface do usuário da Web de armazenamentos e  [!DNL Creative Cloud] arquivos): É aqui que usuários específicos do aplicativo Creative Cloud, com quem uma  [!DNL Assets] pasta foi compartilhada, poderão aceitar o convite e ver a pasta em seu armazenamento de conta Creative Cloud.
* **Aplicativo** para desktop Creative Cloud: (Opcional) Permite acesso direto a pastas compartilhadas/arquivos da área de trabalho do usuário criativo por meio da sincronização com o armazenamento  [!DNL Creative Cloud] Assets.

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional de alterações:Alterações de** arquivo são propagadas em uma única direção - do sistema ([!DNL Experience Manager] ou  [!DNL Creative Cloud Assets]), onde o ativo foi originalmente criado (carregado). A integração não fornece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * [!DNL Experience Manager] cria somente versões de um ativo em atualizações se o arquivo tiver se originado  [!DNL Experience Manager] e for atualizado nele.
   * [!DNL Creative Cloud] O Assets fornece seu próprio recurso  [de controle de versão ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) direcionado para atualizações do Work in Progress (basicamente, armazena atualizações por até 10 dias)

* **Limitações de espaço:** Tamanhos e volumes de arquivos trocados são limitados pela cotação específica do  [Creative Cloud Assets ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuários criativos (depende do nível de subscrição) e uma limitação de 5 GB do tamanho máximo do arquivo. O espaço é adicionalmente limitado pela cota de ativos que a organização tem no serviço principal do Adobe Marketing Cloud Assets.

* **Requisitos de espaço:** os arquivos em pastas compartilhadas também precisam ser armazenados fisicamente em  [!DNL Experience Manager] e depois em  [!DNL Creative Cloud] conta, com uma cópia em cache no serviço  [!DNL Marketing Cloud Assets] principal.
* **Rede e largura de banda:** Os arquivos em pastas compartilhadas e todas as atualizações precisam ser transportados pela rede entre os sistemas. Você deve garantir que somente os arquivos e as atualizações relevantes sejam compartilhados.
* **Tipo** de pasta: O compartilhamento de uma  [!DNL Assets] pasta do tipo  `sling:OrderedFolder` não é suportado no contexto do compartilhamento em  [!DNL Adobe Marketing Cloud]. Se quiser compartilhar uma pasta, ao criá-la em [!DNL Assets], não selecione a opção [!UICONTROL Solicitado].

## Práticas recomendadas {#best-practices}

As práticas recomendadas para aproveitar o compartilhamento de pastas [!DNL Experience Manager] para [!DNL Creative Cloud] incluem:

* **Considerações sobre volume:** [!DNL Experience Manager] e o Compartilhamento de  [!DNL Creative Cloud] pastas devem ser usados para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, [!DNL Assets Brand Portal]) ou [!DNL Experience Manager] aplicativo para desktop.
* **Evite compartilhar hierarquias profundas:** o compartilhamento funciona recursivamente e não permite o compartilhamento seletivo. Normalmente, somente pastas sem subpastas ou com uma hierarquia muito superficial, como 1 nível de subpasta, devem ser consideradas para compartilhamento.
* **Pastas separadas para compartilhamento unidirecional:pastas** separadas devem ser usadas para compartilhar ativos finais de  [!DNL Assets] para  [!DNL Creative Cloud] arquivos e para compartilhar ativos prontos para criação de  [!DNL Creative Cloud] arquivos para  [!DNL Assets]arquivos. Junto com uma boa convenção de nomenclatura para essas pastas, ela cria um ambiente de trabalho mais fácil de entender para [!DNL Assets] e [!DNL Creative Cloud] usuários.
* **Evite o WIP na pasta compartilhada:A pasta** compartilhada não deve ser usada para o Trabalho em andamento - use uma pasta separada em Arquivos de Creative Cloud para realizar um trabalho que exija alterações frequentes no arquivo.
* **Start novo trabalho fora da pasta compartilhada:** novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada em Arquivos Creative Cloud e, quando estiverem prontos para serem compartilhados com  [!DNL Assets] os usuários, devem ser movidos ou salvos para a pasta compartilhada.
* **Simplificar a estrutura de compartilhamento:** para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, as pastas [!DNL Assets] devem ser compartilhadas somente com os representantes da equipe, como um diretor criativo ou um gerente de equipe. O gerente do lado criativo receberia ativos finais, decidiria sobre atribuições de trabalho e deixaria os designers trabalharem em suas próprias contas de Creative Cloud nos ativos WIP. Eles podem usar os recursos de colaboração Creative Cloud para coordenar o trabalho e, por fim, selecionar e colocar ativos prontos para compartilhar de volta para [!DNL Assets] em sua pasta compartilhada pronta para criação.

O diagrama a seguir ilustra um exemplo de configuração para a criação de novos designs com base em ativos finais existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
