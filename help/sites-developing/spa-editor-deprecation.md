---
title: Descontinuação do Editor SPA
description: Embora o Editor de SPA continue sendo compatível com o Adobe, saiba o que sua desativação significa para o seu projeto e quais opções você tem para projetos futuros.
feature: Developing
role: Admin, Architect, Developer
exl-id: ea6e46ee-4a90-4236-8d93-292a4dda4dc0
source-git-commit: d619c969604119a8686050fdc34d77c0ffee33cf
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 1%

---


# Descontinuação do Editor SPA {#spa-editor-deprecation}

Embora o Editor de SPA continue sendo compatível com o Adobe, saiba o que sua desativação significa para o seu projeto e quais opções você tem para projetos futuros.

## Resumo {#summary}

O Adobe substituiu o Editor de SPA pela [versão 6.5.23 do AEM 6.5](/help/release-notes/release-notes.md#spa-editor), o que significa que não serão feitos mais aprimoramentos ou atualizações em seus SDKs. A Adobe incentiva você a usar o [Editor universal](/help/sites-developing/universal-editor/introduction.md) para qualquer novo projeto headless, a fim de aproveitar as vantagens das mais recentes inovações da AEM.

## Detalhes da descontinuação {#details}

A descontinuação do Editor de SPA **não significa remoção imediata** e, se você tiver implementações existentes, **poderá continuar usando-a, contanto que atenda às suas necessidades.** No entanto, esteja ciente das seguintes implicações de sua desativação.

* Além disso, o Adobe somente solucionará os problemas P1 e P2 e as vulnerabilidades de segurança.
* Não serão feitos mais desenvolvimentos, aprimoramentos ou atualizações nos SDKs.

A desativação significa que os seguintes SDKs estão agora no congelamento de recursos.

* [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype/)
* [Núcleo do projeto do AEM SPA](https://github.com/adobe/aem-spa-project-core)
* [Gerenciador de Modelos de Página SPA do AEM](https://github.com/adobe/aem-spa-page-model-manager)
* [Mapeamento de componentes do SPA do AEM](https://github.com/adobe/aem-spa-component-mapping)
* [Componentes editáveis do editor de SPA do AEM](https://github.com/adobe/aem-react-editable-components)
   * [Componentes principais do AEM React](https://github.com/adobe/aem-react-core-wcm-components)
   * [Base dos Componentes Principais do AEM React](https://github.com/adobe/aem-react-core-wcm-components-base)
   * [Componentes principais do AEM React SPA](https://github.com/adobe/aem-react-core-wcm-components-spa)
   * [Exemplos de componentes principais do AEM React](https://github.com/adobe/aem-react-core-wcm-components-examples)
* [Componentes editáveis do AEM SPA Angular](https://github.com/adobe/aem-angular-editable-components)
   * [Componentes principais do AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components)
   * [Base dos Componentes Principais do AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components-base)
   * [Componentes principais do AEM Angular SPA](https://github.com/adobe/aem-angular-core-wcm-components-spa)
   * [Exemplos de componentes principais do AEM Angular](https://github.com/adobe/aem-angular-core-wcm-components-examples)
* [Componentes editáveis do AEM SPA Vue](https://github.com/mavicellc/aem-vue-editable-components)

## Alternativas para o Editor SPA {#alternatives}

O substituto mais adequado para o Editor de SPA depende das necessidades dos projetos.

* **[O Editor Universal](/help/sites-developing/universal-editor/introduction.md)** é a melhor substituição direta para o Editor SPA.
   * O Editor universal também é um editor visual e foi projetado especificamente para implementações dissociadas, incorporando toda a experiência do Adobe no Editor SPA.
   * O Editor Universal também foi [lançado para AEM as a Cloud Service](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/introduction) e, portanto, é compatível com AMS e casos de uso no local, além dos Serviços em Nuvem.
* **[O Editor de Fragmento de Conteúdo](/help/sites-developing/universal-editor/introduction.md)** é uma alternativa para aqueles que preferem um editor baseado em formulário.
   * O Editor de fragmento de conteúdo é mais adequado quando o conteúdo é estruturado como fragmentos de conteúdo do que como páginas.

A estruturação de conteúdo com fragmentos de conteúdo não exclui o uso do Universal Editor como um editor visual, e ambos os editores podem ser usados juntos.

## Migração para o Editor universal {#migrate-ue}

O Editor universal oferece muitas vantagens, tornando a migração para ele uma ótima solução para novos projetos.

* **Edição visual:** assim como para o Editor de SPA, os autores podem editar o conteúdo diretamente na visualização e ver instantaneamente como suas alterações afetam a experiência do visitante.
* **À prova de obsolescência:** o roteiro do AEM prioriza o Editor universal como editor visual. A sua adoção garante o acesso às mais recentes inovações e melhorias.
* **Integração mais simples**: nenhuma SDK específica do AEM é necessária para usar o Editor Universal, reduzindo o bloqueio da pilha técnica.
* **Traga Seu Próprio Aplicativo:** O Universal Editor oferece suporte a qualquer estrutura ou arquitetura da Web, permitindo a adoção sem a necessidade de refatoração complexa.
* **Extensibilidade:** o Editor Universal se beneficia de uma [estrutura de extensão](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/implementing/developing/universal-editor/extending) robusta, que inclui integrações com GenAI, Workfront e muito mais.

Não há caminho de migração direto do Editor de SPA para o Editor universal. Isso se deve a diferenças fundamentais nas duas tecnologias.

* O Editor universal não reintroduz recursos como o Editor de modelo, o Sistema de estilos ou a Grade responsiva.
   * Esses casos de uso agora podem ser tratados com mais eficiência com CSS e JS de front-end enxuto no Edge Delivery Services ou em projetos headless.
* Como o Editor universal é um editor como um serviço, ele não pode permitir que os implementadores injetem CSS ou JS nas caixas de diálogo do componente.
   * Isso impede a conversão automática das caixas de diálogo do componente no Editor de páginas.
   * Isso afeta muitas áreas das caixas de diálogo, como widgets personalizados, validação de campo, regras de mostrar/ocultar e personalizações baseadas em modelo.

Com essas diferenças técnicas em mente, a recomendação da Adobe é:

* Mantenha os sites existentes do SPA Editor como estão, pois o suporte continua.
* Adotar o Editor universal para todos os novos desenvolvimentos, incluindo novos sites, seções ou páginas.

Lembre-se de que, embora não haja implementação direta de determinados recursos do Editor SPA no Editor universal, há novas maneiras de resolver os mesmos problemas usando a nova flexibilidade do Editor universal.

## Comparação entre o editor de SPA e o editor universal {#spa-vs-ue}

O Editor universal oferece muito mais liberdade para implementadores de aplicativos da Web, conforme ilustrado neste diagrama.

![Comparação entre o Editor Universal e as arquiteturas do Editor SPA](assets/spa-editor-vs-ue.png)

|  | Editor SPA | Editor universal |
|---|---|---|
| **Tema** | O aplicativo deve implementar layout com CSS de grade do AEM. | O aplicativo pode usar qualquer técnica CSS moderna para layout. |
| **Renderização** | O aplicativo deve seguir a estrutura de roteamento do Editor de SPA. | O aplicativo pode ser implementado livremente, sem regras ou padrões impostos a serem seguidos. |
| **SDK** | A implementação deve integrar totalmente a SDK. | No nível do autor, o aplicativo apenas carrega o `corlib.js` e instrui o Editor Universal via anotações do HTML. |
| **Estrutura** | O aplicativo deve usar uma versão compatível do React ou do Angular. | O aplicativo pode usar qualquer estrutura ou arquitetura. |
| **Hospedagem** | O aplicativo deve ser hospedado no domínio do AEM. | O aplicativo pode ser totalmente dissociado e hospedado em qualquer lugar. |
| **API** | O aplicativo deve recuperar o conteúdo da API `model.json`. | O aplicativo pode usar qualquer API, incluindo personalizadas. |
| **Persistência** | O Editor SPA só oferece suporte ao conteúdo da página para edição visual. | O Universal Editor oferece suporte nativo à edição visual de páginas e Fragmentos de conteúdo. |
|  |  | O Universal Editor pode ser estendido para editar conteúdo externo com os mesmos recursos visuais. |
|  | Os desenvolvedores devem implantar os Modelos Sling e `cq:Dialog`s no AEM. | Os desenvolvedores precisam de pouca ou nenhuma experiência com o AEM e não precisam gravar nenhum Java. |
