---
title: Migração do Dynamic Media - Modo híbrido para o Dynamic Media - Modo S7
description: Saiba como migrar sua instância do Dynamic Media - Modo híbrido para o Dynamic Media - Modo S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
feature: Modo Scene7, Modo híbrido
exl-id: 07f0803c-4ec4-4745-8214-63370e9d0282
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 2%

---

# Sobre a mudança do Dynamic Media-Hybrid para o Dynamic Media-Scene7 {#about-migrating}

O Dynamic Media-Hybrid é uma versão mais antiga da integração do Dynamic Media com o Adobe Experience Manager. A versão híbrida foi introduzida pela primeira vez no Adobe Experience Manager 6.1. Embora o Adobe continue a oferecer suporte ao modo híbrido, ele não é o modo preferido; O Dynamic Media-Scene7 é o modo preferencial. O modo híbrido também não oferece suporte a novos recursos, como Corte inteligente e imagens panorâmicas, enquanto o Dynamic Media-Scene7 oferece suporte a eles.

Outras diferenças importantes entre o Dynamic Media-Hybrid e o Dynamic Media-Scene7 incluem o seguinte:

* Estrutura de URLs.
* Ingestão de vídeos.
* Criação e armazenamento de representações de imagens.
* Configuração da nuvem e credenciais (provisionamento).

Duas opções estão disponíveis ao migrar do Dynamic Media-Hybrid para o Dynamic Media-Scene7. A primeira opção é simplesmente provisionar uma nova instância do Dynamic Media-Scene7 no Experience Manager. A segunda opção é migrar a instância existente do Dynamic Media-Hybrid para o Dynamic Media-Scene7. Essa opção descreve o formulário da tabela abaixo das etapas e considerações que você deve realizar durante a mudança.

>[!IMPORTANT]
>
>O Adobe recomenda que você não migre uma implementação Dynamic Media-Hybrid para Dynamic Media-Scene7 em instâncias de produção ativas.

## Opção 1 - Provisionar uma nova instância do Dynamic Media-Scene7 no Experience Manager {#provision-new-dms7}

Considere apenas começar de novo com uma nova instância provisionada do Dynamic Media-Scene7 no Adobe Experience Manager. Além da assimilação e do processamento de ativos por meio do Dynamic Media Cloud Service, uma auditoria Adobe de uso de ativos, fluxos de trabalho e componentes é altamente recomendada. Geralmente, é possível substituir componentes e fluxos de trabalho personalizados usando recursos mais recentes e prontos para uso.

## Opção 2: migrar a instância existente do Dynamic Media-Hybrid para o Dynamic Media-Scene7 {#process-for-migrating}

| Etapa | Tarefa | Considerações |
|---|---|---|
| 1 | Clone a instância do autor híbrido do Dynamic Media. | Mantenha sua instância existente do Dynamic Media-Hybrid Author para fins de fallback até que as etapas restantes nesse processo de migração sejam concluídas com êxito. |
| 2 | Inicie a instância Autor clonado no modo Dynamic Media-Scene7. |  |
| 3 | No Adobe Experience Manager Cloud Services, configure o Dynamic Media com credenciais do Dynamic Media-Scene7. | O Adobe deve aprovar o provisionamento Dynamic Media-Scene7. Dessa forma, você tem ambientes simultâneos do Dynamic MediaM-Hybrid e do Dynamic Media-Scene7 compatíveis com o Adobe, mas por um tempo limitado. |
| 4 | Crie o pacote de Migração para poder assimilar ativos conforme necessário.<br>Exclua os PTIFF locais que foram criados durante a assimilação inicial no Dynamic Media-Hybrid. | Se todos os ativos estiverem disponíveis no momento na sua instância Dynamic Media-Hybrid, um clone do que já os incluirá todos. Portanto, nenhum pacote é necessário. |
| 5 | Execute o fluxo de trabalho de atualização de ativos para sincronizar ativos com o Dynamic Media Cloud Service. | O Adobe recomenda executar o workflow de atualização em lotes para permitir a compactação. |
| 6 | Migrar predefinições do visualizador, imagem e vídeo. |  |
| 7 | Percorra cada ativo referenciado pelo Gerenciamento de conteúdo da Web e atualize seus URLs associados. |  |
| 8 | Migre todos os workflows personalizados que você deseja oferecer suporte ao novo modo Dynamic Media-Scene7 (atualizações manuais). |  |
| 9 | Verifique o upload e a configuração do Gerenciamento de conteúdo da Web. |  |
| 10 | Após a verificação, obtenha uma aprovação para desativar o Autor Híbrido do Dynamic Media (manter como fallback). |  |
| 11º | Exclua a instância Dynamic Media-Hybrid Author após aproximadamente um mês de uso bem-sucedido do Dynamic Media-Scene7. |  |
