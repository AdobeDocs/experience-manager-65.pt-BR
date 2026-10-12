---
title: Modelos de carta de referência
description: A AEM Forms fornece modelos de layout de correspondência do Gerenciamento de correspondências que você pode usar para criar cartas rapidamente.
products: SG_EXPERIENCEMANAGER/6.3/FORMS
content-type: reference
topic-tags: correspondence-management
exl-id: 40d127b5-1ce6-41fb-ac4c-2bf7ae79da82
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%
---
# Modelos de carta de referência {#reference-letter-templates}

No Gerenciamento de correspondências, um modelo de correspondência contém campos de formulário típicos, recursos de layout como cabeçalho e rodapé e &quot;áreas de destino&quot; vazias para a inserção de conteúdo.

O Gerenciamento de Correspondências fornece modelos de correspondência no [pacote complementar do AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=en). Você pode personalizar os modelos no Designer de acordo com suas necessidades comerciais e de marca. O pacote inclui os seguintes templates:

* Clássico
* Simples clássico
* Balanceado à esquerda
* Equilibrado à direita
* Visual à esquerda
* Visual superior
* Visual Top - Classic

Após instalar o pacote, os modelos de layout (XDPs) são listados na pasta de modelos no seguinte local:

`https://'[server]:[port]'/[context-root]/aem/forms.html/content/dam/formsanddocuments/templates-folder`

A seguir estão os campos comuns em todos os templates neste pacote:

* Data
* Saudação
* Texto de encerramento
* Texto da assinatura

![Todos os modelos de letra CM listados](assets/templatescorrespondence.png)

Após instalar o pacote AEM-FORMS-6.3-REFERENCE-LAYOUT-TEMPLATES, os modelos são listados na pasta templates

## Clássico {#classic}

Com um logotipo em cima, modelo clássico é adequado para uma carta profissional simples.

![clássico](assets/classic.png)

Visualização no PDF de uma carta criada usando o modelo Clássico

## Simples clássico {#classic-simple}

Inclui campos para capturar número de telefone e endereço de email. Um modelo Simples Clássico é semelhante ao modelo Clássico, exceto que não tem campos em que você possa inserir o endereço do destinatário.

![Fragmento de informações de contato](assets/classicsimple.png)

Visualização no PDF de uma carta criada usando o modelo Simples Clássico

## Balanceado à esquerda {#balanced-left}

O modelo Balanced Left inclui o logotipo à esquerda da letra.

![balancedleft](assets/balancedleft.png)

Visualização PDF de uma carta criada usando o modelo Balanceado à Esquerda

## Equilibrado à direita {#balanced-right}

O modelo Balanced Right tem o logotipo da empresa à esquerda e fornece espaço para inserir o endereço dos destinatários na própria carta. O modelo Equilibrado à direita também inclui um rodapé que flui quando a carta tem várias páginas.

![balancedright](assets/balancedright.png)

Visualização PDF de uma carta criada usando o modelo Balanced Right

## Visual à esquerda {#visual-left}

O modelo Visual Esquerdo tem um lado esquerdo à esquerda da página com o logotipo da empresa colocado sobre o lado esquerdo. O modelo Visual Left tem um campo de assunto, mas nenhum rodapé.

![visualleft](assets/visualleft.png)

Visualização PDF de uma carta criada usando o modelo Visual Esquerdo

## Visual superior {#visual-top}

O modelo Visual Superior tem margem visual na parte superior. O modelo Visual Top tem um campo para inserir o endereço do recipient na própria página. O modelo Visual Superior tem o campo de assunto e um rodapé que reflui para cartas que se estendem por várias páginas.

![visualtop](assets/visualtop.png)

Visualização PDF de uma carta criada usando o modelo Visual Top

## Visual Top - Classic {#visual-top-classic}

O modelo Visual Top - Classic tem um cabeçalho na parte superior da página com o logotipo da empresa. O modelo Visual Top - Classic tem um campo para inserir um assunto, mas nenhum rodapé.

![visualtopclassic](assets/visualtopclassic.png)

Visualização PDF de uma carta criada usando o modelo Visual Top - Classic
