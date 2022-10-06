---
title: Compartilhamento de pastas para [!DNL Adobe Creative Cloud] práticas recomendadas
description: Configurar [!DNL Adobe Experience Manager] para permitir que os usuários [!DNL Experience Manager Assets] para trocar pastas com usuários do Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: a76772b8761e35a828814ffe0ac3b019266ff008
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] para [!DNL Adobe Creative Cloud] compartilhamento de pastas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O [!DNL Experience Manager] para [!DNL Creative Cloud] O recurso Compartilhamento de pastas está obsoleto. O Adobe recomenda utilizar recursos mais recentes, como [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) ou [Aplicativo de desktop do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Saiba mais em [Práticas recomendadas de integração de Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] pode ser configurado para permitir que os usuários em [!DNL Assets] para compartilhar pastas com os usuários do [!DNL Adobe Creative Cloud] para que fiquem disponíveis como pastas compartilhadas na [!DNL Adobe Creative Cloud] serviço de ativos. O recurso pode ser usado para trocar arquivos entre equipes criativas e [!DNL Assets] , especialmente quando os usuários criativos não têm acesso ao [!DNL Assets] implantação (não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto ao [!DNL Assets]:

* [!DNL Assets] os usuários compartilham um conjunto de ativos digitais específicos com os usuários de [!DNL Adobe Creative Cloud] arquivos (por exemplo, um resumo criativo e um conjunto de ativos aprovados para o trabalho de design para uma nova atividade de marketing).
* [!DNL Assets] os usuários recebem novos arquivos criados por [!DNL Adobe Creative Cloud] usuários do aplicativo.

>[!NOTE]
>
>Antes de ler este documento, você pode revisar o [Práticas recomendadas de integração de Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obter uma visão geral da integração.

## Visão geral {#overview}

[!DNL Experience Manager] para [!DNL Creative Cloud] o compartilhamento de pastas depende do compartilhamento de pastas e arquivos no lado do servidor entre [!DNL Assets] e [!DNL Creative Cloud] contas. Profissionais criativos, que usam o [!DNL Creative Cloud] o aplicativo de desktop em seus desktops pode, além disso, disponibilizar as pastas compartilhadas diretamente em seus discos usando [!DNL Adobe CreativeSync] tecnologia.

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **[!DNL Experience Manager Assets]** implantado na rede corporativa (serviços gerenciados ou no local): O compartilhamento de pastas é iniciado aqui.
* **[!DNL Adobe Marketing Cloud Assets]serviço principal**: Atua como intermediário entre [!DNL Experience Manager] e [!DNL Creative Cloud] serviços de armazenamento. Um administrador de uma organização que usa a integração precisa estabelecer uma relação de confiança entre a organização do Marketing Cloud e a [!DNL Assets] implantação. Eles também [definir uma lista de colaboradores aprovados do Creative Cloud](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que [!DNL Assets] os usuários do podem compartilhar pastas também para obter segurança adicional.

* **[!DNL Creative Cloud]Serviços da Web de ativos** (armazenamento e [!DNL Creative Cloud] interface da Web de arquivos): É aqui que usuários específicos do aplicativo Creative Cloud, com quem [!DNL Assets] foi compartilhada, poderia aceitar o convite e ver a pasta em seu armazenamento de conta do Creative Cloud.
* **Aplicativo de desktop do Creative Cloud**: (Opcional) Permite acesso direto a pastas compartilhadas/arquivos da área de trabalho do usuário criativo por meio da sincronização com o [!DNL Creative Cloud] Armazenamento de ativos.

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional das alterações:** As alterações de arquivo são propagadas apenas em uma direção - do sistema ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]), em que o ativo foi criado originalmente (carregado). A integração não oferece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * [!DNL Experience Manager] cria apenas versões de um ativo em atualizações se o arquivo tiver sido originado em [!DNL Experience Manager] e é atualizado nessa página.
   * [!DNL Creative Cloud] Os ativos fornecem seu próprio [recurso de controle de versão](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) direcionado para atualizações do Work in Progress (basicamente, armazena atualizações por até 10 dias)

* **Limitações de espaço:** Os tamanhos e volumes de ficheiros trocados são limitados pela [Cota do Creative Cloud Assets](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuários criativos (depende do nível de assinatura) e uma limitação de tamanho máximo de arquivo de 5 GB. O espaço é também limitado pela cota de ativos que a organização tem no serviço principal do Adobe Marketing Cloud Assets.

* **Requisitos de espaço:** Os arquivos em pastas compartilhadas também precisam ser armazenados fisicamente no [!DNL Experience Manager] e, em seguida, [!DNL Creative Cloud] conta, com uma cópia em cache em [!DNL Marketing Cloud Assets] serviço principal.
* **Rede e largura de banda:** Os arquivos em pastas compartilhadas e todas as atualizações precisam ser transportados pela rede entre os sistemas. Você deve garantir que somente os arquivos e atualizações relevantes sejam compartilhados.
* **Tipo de pasta**: Compartilhamento de um [!DNL Assets] pasta do tipo `sling:OrderedFolder`, não é compatível no contexto de compartilhamento no [!DNL Adobe Marketing Cloud]. Se você deseja compartilhar uma pasta, ao criá-la em [!DNL Assets], não selecione o [!UICONTROL Solicitado] opção.

## Práticas recomendadas {#best-practices}

Práticas recomendadas para aproveitar o [!DNL Experience Manager] para [!DNL Creative Cloud] o compartilhamento de pastas inclui:

* **Considerações sobre volume:** [!DNL Experience Manager] e [!DNL Creative Cloud] O Compartilhamento de pastas deve ser usado para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, [!DNL Assets Brand Portal]) ou [!DNL Experience Manager] aplicativo de desktop.
* **Evite compartilhar hierarquias profundas:** O compartilhamento funciona de forma recursiva e não permite o descompartilhamento seletivo. Normalmente, somente pastas sem subpastas ou com uma hierarquia muito superficial, como 1 nível de subpasta, devem ser consideradas para compartilhamento.
* **Pastas separadas para compartilhamento unidirecional:** Pastas separadas devem ser usadas para compartilhar ativos finais de [!DNL Assets] para [!DNL Creative Cloud] arquivos e para compartilhar ativos prontos para criação a partir de [!DNL Creative Cloud] arquivos para [!DNL Assets]. Juntamente com uma boa convenção de nomenclatura para essas pastas, ela cria um ambiente de trabalho mais fácil de entender para [!DNL Assets] e [!DNL Creative Cloud] usuários.
* **Evite o WIP na pasta compartilhada:** A pasta compartilhada não deve ser usada para o Trabalho em Andamento - use uma pasta separada em Arquivos do Creative Cloud para realizar um trabalho que exija alterações frequentes no arquivo.
* **Iniciar novo trabalho fora da pasta compartilhada:** Novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada em Arquivos de Creative Cloud e quando estiverem prontos para serem compartilhados com [!DNL Assets] usuários, eles devem ser movidos ou salvos na pasta compartilhada.
* **Simplifique a estrutura de compartilhamento:** Para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, [!DNL Assets] as pastas devem ser compartilhadas somente com o(s) representante(s) da equipe, como um diretor criativo ou um gerente de equipe. O gerente do lado criativo receberia ativos finais, decidiria sobre atribuições de trabalho e deixaria os designers trabalharem em suas próprias contas de Creative Cloud em ativos WIP. Eles podem usar os recursos de colaboração do Creative Cloud para coordenar o trabalho e, por fim, selecionar e colocar ativos prontos para compartilhar com o [!DNL Assets] na pasta compartilhada pronta para criação.

O diagrama a seguir ilustra um exemplo de configuração para criar novos designs com base nos ativos finais existentes do [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
