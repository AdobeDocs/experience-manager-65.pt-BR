---
title: Compartilhamento de pastas para  [!DNL Adobe Creative Cloud] práticas recomendadas
description: Configure [!DNL Adobe Experience Manager] to allow users in [!DNL Experience Manager Assets] para trocar pastas com usuários do Adobe Creative Cloud (CC).
contentOwner: AG
role: User, Admin
feature: Colaboração
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] para compartilhamento de  [!DNL Adobe Creative Cloud] pastas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>O recurso [!DNL Experience Manager] para [!DNL Creative Cloud] Compartilhamento de pastas está obsoleto. O Adobe recomenda utilizar recursos mais recentes, como [Adobe Asset Link](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/adobe-asset-link.ug.html) ou [Experience Manager para aplicativos de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Saiba mais em [Práticas recomendadas de integração do Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] O pode ser configurado para permitir que os usuários do  [!DNL Assets] no compartilhem pastas com os usuários dos  [!DNL Adobe Creative Cloud] aplicativos, de modo que fiquem disponíveis como pastas compartilhadas no serviço de  [!DNL Adobe Creative Cloud] ativos. O recurso pode ser usado para trocar arquivos entre equipes criativas e usuários [!DNL Assets], especialmente quando os usuários criativos não têm acesso à implantação [!DNL Assets] (eles não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto a [!DNL Assets]:

* [!DNL Assets] os usuários compartilham um conjunto de ativos digitais específicos com usuários de  [!DNL Adobe Creative Cloud] arquivos (por exemplo, um resumo criativo e um conjunto de ativos aprovados para o trabalho de design de uma nova atividade de marketing).
* [!DNL Assets] os usuários recebem novos arquivos criados por usuários  [!DNL Adobe Creative Cloud] do aplicativo.

>[!NOTE]
>
>Antes de ler este documento, você pode revisar as [práticas recomendadas de integração do Experience Manager e do Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obter uma visão geral da integração.

## Visão geral {#overview}

[!DNL Experience Manager] o compartilhamento de  [!DNL Creative Cloud] pastas depende do compartilhamento de pastas e arquivos entre  [!DNL Assets] e  [!DNL Creative Cloud] contas pelo lado do servidor. Os profissionais criativos, que usam o [!DNL Creative Cloud] aplicativo de desktop em seus desktops, podem também disponibilizar as pastas compartilhadas diretamente em seus discos usando a tecnologia [!DNL Adobe CreativeSync].

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **[!DNL Experience Manager Assets]** implantado na rede corporativa (serviços gerenciados ou no local): O compartilhamento de pastas é iniciado aqui.
* **[!DNL Adobe Marketing Cloud Assets]serviço** principal: Atua como um intermediário entre os serviços  [!DNL Experience Manager] e  [!DNL Creative Cloud] de armazenamento. Um administrador de uma organização que usa a integração precisa estabelecer uma relação de confiança entre a organização do Marketing Cloud e a implantação [!DNL Assets]. Eles também [definem uma lista de Creative Cloud colaboradores aprovados](https://experienceleague.adobe.com/docs/core-services/interface/assets/t-admin-add-cc-user.html), que os usuários [!DNL Assets] podem compartilhar pastas também para segurança adicional.

* **[!DNL Creative Cloud]Serviços Web de ativos**  (interface da Web de armazenamento e  [!DNL Creative Cloud] arquivos): É aqui que usuários específicos do aplicativo Creative Cloud, com quem uma  [!DNL Assets] pasta foi compartilhada, poderiam aceitar o convite e ver a pasta em seu armazenamento de conta do Creative Cloud.
* **Aplicativo** de desktop do Creative Cloud: (Opcional) Permite acesso direto a pastas compartilhadas/arquivos da área de trabalho do usuário criativo por meio da sincronização com o armazenamento de  [!DNL Creative Cloud] Ativos.

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional de alterações:** as alterações de arquivo são propagadas em uma única direção - do sistema ([!DNL Experience Manager] ou  [!DNL Creative Cloud Assets]), onde o ativo foi criado originalmente (carregado). A integração não oferece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * [!DNL Experience Manager] O cria apenas versões de um ativo em atualizações se o arquivo tiver sido originado  [!DNL Experience Manager] e for atualizado lá.
   * [!DNL Creative Cloud] O Assets fornece seu próprio recurso  [de controle de versão ](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) direcionado para atualizações do Work in Progress (basicamente, armazena atualizações por até 10 dias)

* **Limitações de espaço:** Tamanhos e volumes de arquivos trocados são limitados pela cotação específica do  [Creative Cloud Assets ](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuários criativos (depende do nível de assinatura) e por uma limitação de 5 GB do tamanho máximo de arquivo. O espaço é também limitado pela cota de ativos que a organização tem no serviço principal do Adobe Marketing Cloud Assets.

* **Requisitos de espaço:** os arquivos em pastas compartilhadas também precisam ser armazenados fisicamente no  [!DNL Experience Manager] e depois na  [!DNL Creative Cloud] conta, com uma cópia em cache no serviço  [!DNL Marketing Cloud Assets] principal.
* **Rede e largura de banda:** Os arquivos em pastas compartilhadas e todas as atualizações precisam ser transportados pela rede entre os sistemas. Você deve garantir que somente os arquivos e atualizações relevantes sejam compartilhados.
* **Tipo** de pasta: O compartilhamento de uma  [!DNL Assets] pasta do tipo  `sling:OrderedFolder` não é compatível no contexto de compartilhamento no  [!DNL Adobe Marketing Cloud]. Se quiser compartilhar uma pasta, ao criá-la em [!DNL Assets], não selecione a opção [!UICONTROL Ordered].

## Práticas recomendadas {#best-practices}

As práticas recomendadas para aproveitar o [!DNL Experience Manager] para [!DNL Creative Cloud] compartilhamento de pastas incluem:

* **Considerações de volume:** [!DNL Experience Manager] e o Compartilhamento de  [!DNL Creative Cloud] pastas devem ser usados para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, [!DNL Assets Brand Portal]) ou [!DNL Experience Manager] aplicativo de desktop.
* **Evite compartilhar hierarquias profundas:** o compartilhamento funciona de forma recursiva e não permite o descompartilhamento seletivo. Normalmente, somente pastas sem subpastas ou com uma hierarquia muito superficial, como 1 nível de subpasta, devem ser consideradas para compartilhamento.
* **Pastas separadas para compartilhamento unidirecional:** pastas separadas devem ser usadas para compartilhar ativos finais de  [!DNL Assets] a  [!DNL Creative Cloud] arquivos e para compartilhar ativos prontos para criação de  [!DNL Creative Cloud] volta de arquivos para  [!DNL Assets]. Juntamente com uma boa convenção de nomenclatura para essas pastas, ela cria um ambiente de trabalho mais fácil de entender para os usuários [!DNL Assets] e [!DNL Creative Cloud] da mesma forma.
* **Evite o WIP na pasta compartilhada:** a pasta compartilhada não deve ser usada para o Trabalho em Andamento - use uma pasta separada em Arquivos de Creative Cloud para realizar um trabalho que exija alterações frequentes no arquivo.
* **Iniciar novo trabalho fora da pasta compartilhada:** novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada em Arquivos de Creative Cloud e, quando estiverem prontos para serem compartilhados com  [!DNL Assets] usuários, eles devem ser movidos ou salvos na pasta compartilhada.
* **Simplifique a estrutura de compartilhamento:** para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, as pastas [!DNL Assets] devem ser compartilhadas somente com representantes da equipe, como um diretor criativo ou gerente de equipe. O gerente do lado criativo receberia ativos finais, decidiria sobre atribuições de trabalho e deixaria os designers trabalharem em suas próprias contas de Creative Cloud em ativos WIP. Eles podem usar os recursos de colaboração do Creative Cloud para coordenar o trabalho e, por fim, selecionar e colocar ativos prontos para compartilhar de volta em [!DNL Assets] em sua pasta compartilhada pronta para criação.

O diagrama a seguir ilustra um exemplo de configuração para criar novos designs com base em ativos finais existentes de [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
