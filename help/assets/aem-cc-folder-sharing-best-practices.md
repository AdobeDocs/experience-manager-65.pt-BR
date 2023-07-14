---
title: Compartilhamento de pasta para [!DNL Adobe Creative Cloud] práticas recomendadas
description: Configurar [!DNL Adobe Experience Manager] para permitir usuários em [!DNL Experience Manager Assets] para trocar pastas com usuários do Adobe Creative Cloud.
contentOwner: AG
role: User, Admin
feature: Collaboration
exl-id: 130cec6d-1cdd-4304-94bb-65e6bb573e55
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# [!DNL Adobe Experience Manager] para [!DNL Adobe Creative Cloud] compartilhamento de pastas {#aem-to-creative-cloud-folder-sharing-best-practices}

>[!CAUTION]
>
>A variável [!DNL Experience Manager] para [!DNL Creative Cloud] O recurso Compartilhamento de pastas foi descontinuado. O Adobe recomenda usar recursos mais recentes, como [Adobe Asset Link](https://helpx.adobe.com/br/enterprise/using/adobe-asset-link.html) ou [aplicativo de desktop do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html). Saiba mais em [Práticas recomendadas de integração de Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md).

[!DNL Adobe Experience Manager] O pode ser configurado para permitir que usuários do [!DNL Assets] para compartilhar pastas com os usuários do [!DNL Adobe Creative Cloud] aplicativos, para que estejam disponíveis como pastas compartilhadas na [!DNL Adobe Creative Cloud] serviço de ativos. O recurso pode ser usado para trocar arquivos entre equipes criativas e [!DNL Assets] especialmente quando os utilizadores criativos não têm acesso à informação [!DNL Assets] implantação (não estão na rede corporativa).

Esse tipo de integração pode ser usado nos seguintes casos de uso, especialmente ao trabalhar com usuários que não têm acesso direto ao [!DNL Assets]:

* [!DNL Assets] usuários compartilham um conjunto de ativos digitais específicos com usuários do [!DNL Adobe Creative Cloud] arquivos (por exemplo, um resumo criativo e um conjunto de ativos aprovados para trabalho de design para uma nova atividade de marketing).
* [!DNL Assets] os usuários recebem os novos arquivos criados por [!DNL Adobe Creative Cloud] usuários do aplicativo.

>[!NOTE]
>
>Antes de ler este documento, você pode revisar o [Práticas recomendadas de integração de Experience Manager e Creative Cloud](/help/assets/aem-cc-integration-best-practices.md) para obter uma visão geral da integração.

## Visão geral {#overview}

[!DNL Experience Manager] para [!DNL Creative Cloud] o compartilhamento de pastas depende do compartilhamento de pastas e arquivos do lado do servidor entre [!DNL Assets] e [!DNL Creative Cloud] contas. Profissionais de criação, que utilizam o [!DNL Creative Cloud] aplicativo de desktop da em seus desktops, o também pode disponibilizar as pastas compartilhadas diretamente em seus discos usando [!DNL Adobe CreativeSync] tecnologia.

O diagrama a seguir fornece uma visão geral da integração.

![chlimage_1-179](assets/chlimage_1-406.png)

A integração inclui os seguintes elementos:

* **[!DNL Experience Manager Assets]** implantado na rede corporativa (Managed Services ou no local): o compartilhamento de pastas é iniciado aqui.
* **[!DNL Adobe Experience Cloud Assets]serviço principal**: atua como um intermediário entre [!DNL Experience Manager] e [!DNL Creative Cloud] serviços de armazenamento. Um administrador de uma organização que usa a integração deve estabelecer uma relação de confiança entre a organização Experience Cloud e a [!DNL Assets] implantação. Eles também [definir uma lista de colaboradores de Creative Cloud aprovados](https://experienceleague.adobe.com/docs/core-services/interface/services/assets/t-admin-add-cc-user.html), que [!DNL Assets] os usuários também podem compartilhar pastas para maior segurança.

* **[!DNL Creative Cloud]Serviços Web de ativos** (armazenamento e [!DNL Creative Cloud] Web de arquivos): é aqui que usuários específicos do aplicativo Creative Cloud, com os quais um [!DNL Assets] a pasta foi compartilhada, poderia aceitar o convite e ver a pasta em seu armazenamento da conta Creative Cloud.
* **aplicativo de desktop do Creative Cloud**: (opcional) permite acesso direto a pastas/arquivos compartilhados do desktop do usuário criativo por meio da sincronização com o [!DNL Creative Cloud] Armazenamento de ativos.

## Características e limitações {#characteristics-and-limitations}

* **Propagação unidirecional de alterações:** As alterações em arquivos são propagadas somente em uma direção - do sistema ([!DNL Experience Manager] ou [!DNL Creative Cloud Assets]), onde o ativo foi criado originalmente (carregado). A integração não fornece uma sincronização bidirecional totalmente automatizada entre os dois sistemas.
* **Versões:**

   * [!DNL Experience Manager] O só cria versões de um ativo em atualizações se o arquivo tiver origem em [!DNL Experience Manager] e é atualizado lá.
   * [!DNL Creative Cloud] Os ativos fornecem os seus próprios [recurso de controle de versão](https://helpx.adobe.com/creative-cloud/help/versioning-faq.html) que é direcionado para atualizações de Trabalho em andamento (basicamente, armazena atualizações por até dez dias)

* **Limitações de espaço:** Os tamanhos e volumes de arquivos trocados são limitados pelas [Cota de ativos Creative Cloud](https://helpx.adobe.com/creative-cloud/kb/file-storage-quota.html) para usuários criativos (depende do nível de assinatura) e uma limitação de tamanho máximo de arquivo de 5 GB. O espaço também é limitado pela cota de ativos que a organização tem no serviço principal do Adobe Experience Cloud Assets.

* **Requisitos de espaço:** Os arquivos nas pastas compartilhadas também devem ser fisicamente armazenados no [!DNL Experience Manager] e depois em [!DNL Creative Cloud] conta, com uma cópia em cache no [!DNL Experience Cloud Assets] serviço principal.
* **Rede e largura de banda:** Os arquivos nas pastas compartilhadas e todas as atualizações devem ser transportados pela rede entre os sistemas. Certifique-se de que somente os arquivos e as atualizações relevantes sejam compartilhados.
* **Tipo de pasta**: Compartilhamento de um [!DNL Assets] pasta do tipo `sling:OrderedFolder`, não é compatível no contexto de compartilhamento em [!DNL Adobe Experience Cloud]. Se quiser compartilhar uma pasta, ao criá-la no [!DNL Assets], não selecione a variável [!UICONTROL Encomendado] opção.

## Práticas recomendadas {#best-practices}

Práticas recomendadas para usar o [!DNL Experience Manager] para [!DNL Creative Cloud] o compartilhamento de pastas inclui:

* **Considerações sobre volume:** [!DNL Experience Manager] e [!DNL Creative Cloud] O Compartilhamento de pastas deve ser usado para compartilhar um número menor de arquivos, por exemplo, relevantes para uma campanha ou atividade específica. Para compartilhar conjuntos maiores de ativos, como todos os ativos aprovados na organização, use outros métodos de distribuição (por exemplo, [!DNL Assets Brand Portal]ou [!DNL Experience Manager] aplicativo de desktop.
* **Evite compartilhar hierarquias profundas:** O compartilhamento funciona de forma recursiva e não permite o descompartilhamento seletivo. Normalmente, somente as pastas sem subpastas ou com uma hierarquia superficial, como um nível de subpasta, devem ser consideradas para compartilhamento.
* **Pastas separadas para compartilhamento unidirecional:** Pastas separadas devem ser usadas para compartilhar ativos finais de [!DNL Assets] para [!DNL Creative Cloud] arquivos e para compartilhar ativos prontos para criação de volta do [!DNL Creative Cloud] arquivos para [!DNL Assets]. Juntamente com uma boa convenção de nomenclatura para essas pastas, cria um ambiente de trabalho mais fácil de entender para [!DNL Assets] e [!DNL Creative Cloud] usuários.
* **Evitar Trabalho em andamento na pasta compartilhada:** A pasta compartilhada não deve ser usada para Trabalho em andamento - use uma pasta separada em Arquivos Creative Cloud para realizar trabalhos que exigem alterações frequentes no arquivo.
* **Iniciar novo trabalho fora da pasta compartilhada:** Os novos designs (arquivos criativos) devem ser iniciados na pasta WIP separada em Arquivos Creative Cloud e quando estiverem prontos para serem compartilhados com [!DNL Assets] usuários, eles devem ser movidos ou salvos na pasta compartilhada.
* **Simplifique a estrutura de compartilhamento:** Para uma configuração operacional mais gerenciável, pense em simplificar a estrutura de compartilhamento. Em vez de compartilhar com todos os usuários criativos, [!DNL Assets] as pastas devem ser compartilhadas somente com representantes da equipe, como um diretor criativo ou gerente de equipe. O gerente do lado criativo receberia os ativos finais, decidiria as atribuições de trabalho e deixaria os designers trabalharem em suas próprias contas do Creative Cloud em ativos do WIP. Eles podem usar os recursos de colaboração do Creative Cloud para coordenar o trabalho e, finalmente, selecionar e colocar os ativos que estão prontos para serem compartilhados no [!DNL Assets] na pasta compartilhada criativa.

O diagrama a seguir ilustra um exemplo de configuração para criar designs com base nos ativos finais existentes no [!DNL Assets].

![chlimage_1-180](assets/chlimage_1-407.png)
