---
title: Migração do Dynamic Media - Modo híbrido para Dynamic Media - modo S7
description: Saiba como migrar a instância do Dynamic Media - modo híbrido para o Dynamic Media - modo S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Scene7 Mode,Hybrid Mode
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 2%

---

# Sobre a mudança do Dynamic Media-Hybrid para o Dynamic Media-Scene7 {#about-migrating}

O Dynamic Media-Hybrid é uma versão mais antiga da integração do Dynamic Media com o Adobe Experience Manager. A versão híbrida foi introduzida pela primeira vez no Adobe Experience Manager 6.1. Embora o Adobe continue a ser compatível com o modo híbrido, ele não é o modo preferido; Dynamic Media-Scene7 é o modo preferido para usar. O modo híbrido também não é compatível com novos recursos, como Recorte inteligente e imagens panorâmicas, enquanto o Dynamic Media-Scene7 é compatível com eles.

As principais diferenças entre o Dynamic Media-Hybrid e o Dynamic Media-Scene7 incluem o seguinte:

* Estrutura de URLs.
* Assimilação de vídeos.
* Criação e armazenamento de representações de imagem.
* Configuração e credenciais da nuvem (provisionamento).

Duas opções estão disponíveis ao migrar do Dynamic Media-Hybrid para o Dynamic Media-Scene7. A primeira opção é simplesmente provisionar uma nova instância do Dynamic Media-Scene7 no Experience Manager. A segunda opção é migrar sua instância existente do Dynamic Media-Hybrid para o Dynamic Media-Scene7. Essa opção descreve o formato da tabela abaixo das etapas e considerações que você deve fazer durante a movimentação.

>[!IMPORTANT]
>
>A Adobe recomenda que você não migre uma implementação híbrida do Dynamic Media para o Dynamic Media-Scene7 em instâncias de produção ativas.

## Opção 1 - Provisionar uma nova instância do Dynamic Media-Scene7 no Experience Manager {#provision-new-dms7}

Considere apenas começar do zero com uma nova instância provisionada do Dynamic Media-Scene7 no Adobe Experience Manager. Além da assimilação e do processamento de ativos por meio do Dynamic Media Cloud Service, uma auditoria de Adobe do uso de ativos, fluxos de trabalho e componentes é altamente recomendada. Geralmente, você pode substituir componentes e fluxos de trabalho personalizados usando recursos mais recentes e prontos para uso.

## Opção 2 - Migrar sua instância existente do Dynamic Media-Hybrid para o Dynamic Media-Scene7 {#process-for-migrating}

| Etapa | Tarefa | Considerações |
|---|---|---|
| 1 | Clonar a instância do autor Dynamic Media-Hybrid. | Mantenha sua instância existente do Dynamic Media-Hybrid Author para fins de fallback até que as etapas restantes desse processo de migração sejam concluídas com êxito. |
| 2 | Iniciar instância do autor clonada no modo Dynamic Media-Scene7. |  |
| 3 | No Adobe Experience Manager Cloud Services, configure o Dynamic Media com credenciais do Dynamic Media-Scene7. | O Adobe deve aprovar o provisionamento Dynamic Media-Scene7. Dessa forma, você tem ambientes simultâneos Dynamic MediaM-Hybrid e Dynamic Media-Scene7 compatíveis com o Adobe, mas somente por um tempo limitado. |
| 4 | Crie um pacote de migração para assimilar ativos conforme necessário.<br>Exclua os PTIFFs locais que foram criados durante a assimilação inicial no Dynamic Media Hybrid. | Se todos os ativos estiverem disponíveis atualmente na instância Dynamic Media-Hybrid, um clone do que já os incluirá todos. Portanto, nenhum pacote é necessário. |
| 5 | Execute o fluxo de trabalho de atualização de ativos para sincronizar ativos ao Dynamic Media Cloud Service. | A Adobe recomenda que você execute o fluxo de trabalho de atualização em lotes para permitir a compactação. |
| 6 | Migrar predefinições de visualizador, imagem e vídeo. |  |
| 7 | Percorra cada ativo referenciado ao Gerenciamento de conteúdo da Web e atualize seus URLs associados. |  |
| 8 | Migre todos os workflows personalizados que deseja que sejam compatíveis com o novo modo Dynamic Media-Scene7 (atualizações manuais). |  |
| 9 | Verifique o upload e a configuração do Gerenciamento de conteúdo da Web. |  |
| 10 | Após a verificação, obtenha uma aprovação para desativar o Dynamic Media-Hybrid Author (manter como um fallback). |  |
| 11 | Exclua a instância do autor híbrido do Dynamic Media após aproximadamente um mês de uso bem-sucedido do Dynamic Media-Scene7. |  |
