---
title: Migração do Dynamic Media - Modo híbrido para o Dynamic Media - Modo S7
description: Saiba como migrar sua instância do Dynamic Media - Modo híbrido para o Dynamic Media - modo S7
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 7aba1f3b492a07fe502f95535a94c8054a044eb5

---


# Sobre a mudança do Dynamic Media-Hybrid para o Dynamic Media-Scene7 {#about-migrating}

O Dynamic Media-Hybrid é uma versão mais antiga da integração do Dynamic Media com o Adobe Experience Manager. A versão híbrida foi introduzida pela primeira vez no AEM (Adobe Experience Manager) 6.1. Embora a Adobe continue a oferecer suporte ao modo Híbrido, ele não é o modo preferencial (o Dynamic Media-Scene7 é o modo preferencial). Também não oferece suporte a novos recursos, como o Smart Crop e imagens panorâmicas. Enquanto o Dynamic Media-Scene7 faz isso.

As principais diferenças adicionais entre o Dynamic Media-Hybrid e o Dynamic Media-Scene7 incluem:

* Estrutura de URLs.
* Ingestão de vídeos.
* Criação e armazenamento de execuções de imagem.
* Configuração e credenciais da nuvem (provisionamento).

Duas opções estão disponíveis ao mover do Dynamic Media-Hybrid para o Dynamic Media-Scene7. A primeira opção é simplesmente provisionar uma nova instância do Dynamic Media-Scene7 no AEM. A segunda opção é migrar a instância existente do Dynamic Media-Hybrid para o Dynamic Media-Scene7. Esta opção descreve o formulário de tabela abaixo das etapas e considerações que você deve realizar durante a mudança.

>[!IMPORTANT]
>
>A Adobe recomenda que você não migre uma implementação do Dynamic Media-Hybrid para o Dynamic Media-Scene7 em instâncias de produção ativas.

## Opção 1 - Provisionamento de uma nova instância do Dynamic Media-Scene7 no AEM {#provision-new-dms7}

Considere apenas começar de novo com uma nova instância provisionada do Dynamic Media-Scene7 no Adobe Experience Manager. Além da ingestão e do processamento de ativos por meio do Serviço da Dynamic Media Cloud, uma auditoria da Adobe sobre o uso de ativos, workflows e componentes é altamente recomendada. Em muitos casos, os componentes e workflows personalizados podem ser substituídos por recursos mais novos e prontos para uso.

## Opção 2 - Migração da instância existente do Dynamic Media-Hybrid para o Dynamic Media-Scene7 {#process-for-migrating}

| Etapa | Tarefa | Considerações |
|---|---|---|
| 1 | Clonar instância do autor híbrido do Dynamic Media. | Você deve manter sua instância atual do Autor do Dynamic Media-Hybrid para fins de fallback até que as etapas restantes neste processo de migração sejam concluídas com êxito. |
| 2 | Instância do autor clonada pelo Start no modo Dynamic Media-Scene7. |  |
| 3 | No Adobe Experience Manager Cloud Services, configure o Dynamic Media com credenciais do Dynamic Media-Scene7. | A Adobe precisa aprovar o provisionamento do Dynamic Media-Scene7. Você terá ambientes simultâneos do Dynamic MediaM-Hybrid e do Dynamic Media-Scene7 que serão suportados por um tempo limitado. |
| 4 | Criar pacote de migração para assimilar ativos conforme necessário.<br>Exclua os PTIFFs locais criados durante a ingestão inicial no Dynamic Media-Hybrid. | Se todos os ativos estiverem disponíveis no momento na sua instância do Dynamic Media-Hybrid, um clone do qual já inclui todos eles. Portanto, nenhum pacote é necessário. |
| 5 | Execute o fluxo de trabalho de atualização de ativos para sincronizar ativos com o serviço da Dynamic Media Cloud. | A Adobe recomenda que o fluxo de trabalho de atualização seja feito em lotes para permitir a compactação. |
| 6 | Migrar predefinições de visualizador, imagem e vídeo. |  |
| 7 | Percorra cada ativo referenciado por Gestão de conteúdo da Web e atualize seus URLs associados. |  |
| 8 | Migre quaisquer workflows personalizados para suportar o novo modo Dynamic Media-Scene7 (atualizações manuais). |  |
| 9 | Verifique o upload e a configuração de sua Gestão de conteúdo da Web. |  |
| 10 | Após a verificação, obtenha uma aprovação para desabilitar o Autor do Dynamic Media-Hybrid (manter como retorno de queda). |  |
| 11 | Exclua a instância do Autor do Dynamic Media-Hybrid após aproximadamente um mês de uso bem-sucedido do Dynamic Media-Scene7. |  |
