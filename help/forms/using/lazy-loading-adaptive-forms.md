---
title: Melhorar o desempenho de formulários grandes com carregamento lento
seo-title: Improve performance of large forms with lazy loading
description: O carregamento lento melhora significativamente o desempenho de formulários adaptáveis grandes e complexos ao adiar a inicialização e o carregamento de fragmentos de formulário até que eles fiquem visíveis.
seo-description: Lazy loading significantly improves the performance of large and complex adaptive forms by deferring initialization and loading of form fragments until they are visible.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
feature: Adaptive Forms
exl-id: f7e3e2cd-0cbe-4b26-9e55-7afc6dc3af63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# Melhorar o desempenho de formulários grandes com carregamento lento{#improve-performance-of-large-forms-with-lazy-loading}

## Introdução ao carregamento lento {#introduction-to-lazy-loading}

Quando o formulário se torna grande e complexo com centenas e milhares de campos, os usuários finais experimentam um longo tempo de resposta ao renderizar formulários no tempo de execução. Para minimizar o tempo de resposta, os formulários adaptáveis permitem dividir formulários em fragmentos lógicos e configurar para adiar a inicialização ou o carregamento de fragmentos até que o fragmento precise estar visível. É chamado de carregamento lento. Além disso, os fragmentos configurados para carregamento lento são descarregados depois que o usuário navega para outras seções no formulário e os fragmentos não estão mais visíveis.

Vamos primeiro entender os requisitos e as etapas preparatórias antes de configurar o carregamento lento.

## Preparação para configurar o carregamento lento {#preparing-to-configure-lazy-loading}

Antes de configurar o carregamento lento de fragmentos em seu formulário adaptável, é importante definir estratégias para criar fragmentos, identificar valores que são usados em scripts ou referenciados em outros fragmentos e definir regras para controlar a visibilidade dos campos em fragmentos carregados lentamente.

* **Identificar e criar fragmentos**
Você pode configurar apenas fragmentos de formulário adaptáveis para carregamento lento. Um fragmento é um segmento independente que fica fora de um formulário adaptável e pode ser reutilizado em formulários. Assim, o primeiro passo para implementar o carregamento lento é identificar seções lógicas em um formulário e convertê-las em fragmentos. É possível criar um fragmento do zero ou salvar um painel de formulário existente como fragmento.

   Para obter mais informações sobre como criar fragmentos, consulte [Fragmentos de formulário adaptáveis](../../forms/using/adaptive-form-fragments.md).

* **Identificar e marcar valores globais**
As transações baseadas em Forms envolvem elementos dinâmicos para capturar dados relevantes dos usuários e processá-los para simplificar a experiência de preenchimento de formulários. Por exemplo, seu formulário tem o campo A no fragmento X cujo valor determina a validade do campo B em outro fragmento. Nesse caso, se o fragmento X estiver marcado para carregamento lento, o valor do campo A deverá estar disponível para validar o campo B mesmo quando o fragmento X não estiver carregado. Para isso, é possível marcar o campo A como global, o que garante que seu valor esteja disponível para a validação do campo B quando o fragmento X não estiver carregado.

   Para obter informações sobre como tornar um valor de campo global, consulte [Configuração do carregamento lento](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Gravar regras para controlar a visibilidade dos campos**
O Forms inclui alguns campos e seções que não se aplicam a todos os usuários e em todas as condições. Os autores e desenvolvedores do Forms usam regras de visibilidade ou mostrar para controlar sua visibilidade com base nas entradas do usuário. Por exemplo, o campo Endereço do escritório não é exibido para os usuários que escolhem Desempregado no campo Status do Emprego em um formulário. Para obter mais informações sobre regras de gravação, consulte [Uso do editor de regras](../../forms/using/rule-editor.md).

   Você pode aproveitar as regras de visibilidade nos fragmentos carregados de preguiça para que os campos condicionais sejam exibidos somente quando forem necessários. Além disso, marque o campo condicional global para referenciá-lo na expressão de visibilidade do fragmento carregado lentamente.

## Configuração do carregamento lento {#configuring-lazy-loading}

Execute as seguintes etapas para habilitar o carregamento lento em um fragmento de formulário adaptável:

1. Abra o formulário adaptável no modo de criação que contém o fragmento que deseja ativar para carregamento lento.
1. Selecione o fragmento do formulário adaptável e toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, ative **[!UICONTROL Carregar fragmento lentamente]** e tocar **Concluído**.

   ![Habilitar carregamento lento para o fragmento de formulário adaptável](assets/lazy-loading-fragment.png)

   O fragmento agora está ativado para carregamento lento.

É possível marcar os valores dos objetos no fragmento carregado lentamente como global para que eles estejam disponíveis para uso em scripts quando o fragmento contido não estiver carregado. Faça o seguinte:

1. Abra o fragmento de formulário adaptável no modo de criação.
1. Toque no campo cujo valor você deseja marcar como global e toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, ative **Usar valor durante o carregamento lento**.

   ![Campo de carregamento lento na barra lateral](assets/enable-lazy-loading.png)

   O valor agora é marcado como global e estará disponível para uso em scripts, mesmo quando o fragmento que contém for descarregado.

## Considerações e práticas recomendadas para configurar o carregamento lento {#considerations-and-best-practices-for-configuring-lazy-loading}

Algumas limitações, recomendações e pontos importantes a serem considerados ao trabalhar com o carregamento lento são as seguintes:

* É recomendável usar formulários adaptáveis baseados em esquema XSD em formulários adaptáveis baseados em XFA para configurar o carregamento lento em formulários grandes. O ganho de desempenho devido à implementação de carregamento lento em formulários adaptáveis baseados em XFA é relativamente menor do que o ganho em formulários adaptáveis baseados em XSD.
* Não configure o carregamento lento em fragmentos em um formulário adaptável que use **[!UICONTROL Responsivo - tudo em uma página sem navegação]** layout para o painel raiz. Como resultado da configuração do layout responsivo, todos os fragmentos são carregados simultaneamente em um formulário adaptável. Também pode resultar em desempenho degradado.
* É recomendável não configurar o carregamento lento no primeiro fragmento em um formulário adaptável.
* É recomendável não configurar o carregamento lento em fragmentos no primeiro painel que é renderizado ao carregar o formulário adaptável.
* O carregamento lento é compatível com até dois níveis na hierarquia de fragmentos.
* Certifique-se de que os campos marcados como globais sejam exclusivos em um formulário adaptável.
* Considere escrever regras de visibilidade para fragmentos que devem mostrar ou ocultar com base em uma condição. Por exemplo, você pode mostrar ou ocultar o fragmento Detalhes do Cônjuge com base no status civil especificado por um usuário.
* O anexo de arquivo e os componentes Termos e condições não são suportados em fragmentos carregados de forma preguiçosa.

### Práticas recomendadas de script para configurar o carregamento lento {#scripting-best-practices-for-configuring-lazy-loading}

Pontos importantes a serem considerados ao desenvolver scripts para painéis de carregamento lento são os seguintes:

* Certifique-se de que os scripts de inicialização e cálculo usados nos campos de um fragmento carregado lento sejam despotentes na natureza. Os scripts Idempotentes são aqueles que têm o mesmo efeito mesmo após várias execuções.
* Use a propriedade de campos globalmente disponível para disponibilizar o valor dos campos localizados em um painel de carregamento lento para todos os outros painéis de um formulário.
* Não encaminhe o valor de referência de um campo dentro de um painel lento, independentemente de o campo estar sendo marcado globalmente em fragmentos ou não.
* Use o recurso de redefinição do painel para redefinir tudo o que está visível no painel, usando a seguinte expressão de clique.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;: &quot;navigablePanel&quot;}).resetData()
