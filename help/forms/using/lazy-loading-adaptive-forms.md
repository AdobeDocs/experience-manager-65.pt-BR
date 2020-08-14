---
title: Melhore o desempenho de formulários grandes com carregamento lento
seo-title: Melhore o desempenho de formulários grandes com carregamento lento
description: O carregamento lento melhora significativamente o desempenho de formulários adaptativos grandes e complexos ao adiar a inicialização e o carregamento de fragmentos de formulário até que eles fiquem visíveis.
seo-description: O carregamento lento melhora significativamente o desempenho de formulários adaptativos grandes e complexos ao adiar a inicialização e o carregamento de fragmentos de formulário até que eles fiquem visíveis.
uuid: 6be3d2f0-1b2a-4090-af66-2b08487c31bc
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a20736b7-f7b4-4da1-aa32-2408049b1209
docset: aem65
translation-type: tm+mt
source-git-commit: 428d675bd254c18651c1188de26b706b5ad3d55c
workflow-type: tm+mt
source-wordcount: '1027'
ht-degree: 0%

---


# Melhore o desempenho de formulários grandes com carregamento lento{#improve-performance-of-large-forms-with-lazy-loading}

## Introdução ao carregamento lento {#introduction-to-lazy-loading}

Quando o formulário se torna grande e complexo com centenas e milhares de campos, os usuários finais experimentam um longo tempo de resposta ao renderizar formulários em tempo de execução. Para minimizar o tempo de resposta, os formulários adaptáveis permitem que você quebre formulários em fragmentos lógicos e configure para adiar a inicialização ou o carregamento dos fragmentos até que o fragmento precise estar visível. É chamado de carregamento lento. Além disso, os fragmentos configurados para carregamento lento são descarregados depois que o usuário navega para outras seções no formulário e os fragmentos não ficam mais visíveis.

Primeiro, vamos entender os requisitos e as etapas preparatórias antes de configurar o carregamento lento.

## Preparação para configurar o carregamento lento {#preparing-to-configure-lazy-loading}

Antes de configurar o carregamento lento de fragmentos em seu formulário adaptável, é importante definir estratégias para criar fragmentos, identificar valores que são usados em scripts ou referenciados em outros fragmentos e definir regras para controlar a visibilidade dos campos em fragmentos carregados preguiçosamente.

* **Identificar e criar fragmentos** Você pode configurar somente fragmentos de formulário adaptáveis para carregamento lento. Um fragmento é um segmento independente que reside fora de um formulário adaptável e pode ser reutilizado em formulários. Portanto, o primeiro passo para implementar o carregamento lento é identificar seções lógicas em um formulário e convertê-las em fragmentos. É possível criar um fragmento do zero ou salvar um painel de formulário existente como fragmento.

   Para obter mais informações sobre como criar fragmentos, consulte [Fragmentos](../../forms/using/adaptive-form-fragments.md)de formulário adaptáveis.

* **Identificar e marcar valores** globais As transações baseadas no Forms envolvem elementos dinâmicos para capturar dados relevantes dos usuários e processá-los para simplificar a experiência de preenchimento de formulários. Por exemplo, seu formulário tem o campo A no fragmento X cujo valor determina a validade do campo B em outro fragmento. Nesse caso, se o fragmento X estiver marcado para carregamento lento, o valor do campo A deve estar disponível para validar o campo B mesmo quando o fragmento X não estiver carregado. Para isso, é possível marcar o campo A como global, garantindo que seu valor esteja disponível para a validação do campo B quando o fragmento X não for carregado.

   Para obter informações sobre como tornar um valor de campo global, consulte [Configuração de carregamento](../../forms/using/lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p)lento.

* **As regras de gravação para controlar a visibilidade dos campos** Forms incluem alguns campos e seções que não se aplicam a todos os usuários e em todas as condições. Os autores e desenvolvedores do Forms usam regras de visibilidade ou mostrar para controlar sua visibilidade com base em entradas do usuário. Por exemplo, o campo Endereço do escritório não é exibido para os usuários que escolhem Não empregado no campo Status do Emprego em um formulário. Para obter mais informações sobre como escrever regras, consulte [Uso do editor](../../forms/using/rule-editor.md)de regras.

   É possível aproveitar as regras de visibilidade nos fragmentos carregados com preguiça para que os campos condicionais sejam exibidos somente quando forem necessários. Além disso, marque o campo condicional como global para referenciá-lo na expressão de visibilidade do fragmento carregado com preguiça.

## Configurando carregamento lento {#configuring-lazy-loading}

Execute as seguintes etapas para habilitar o carregamento lento em um fragmento de formulário adaptável:

1. Abra o formulário adaptável no modo de criação que contém o fragmento que deseja ativar para carregamento lento.
1. Selecione o fragmento de formulário adaptável e toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, ative **[!UICONTROL Carregar fragmento preguiçosamente]** e toque em **Concluído**.

   ![Ativar carregamento lento para o fragmento de formulário adaptável](assets/lazy-loading-fragment.png)

   O fragmento agora está habilitado para carregamento lento.

É possível marcar os valores de objetos no fragmento carregado com preguiça como globais para que eles estejam disponíveis para uso em scripts quando o fragmento contido não for carregado. Faça o seguinte:

1. Abra o fragmento de formulário adaptável no modo de criação.
1. Toque no campo cujo valor você deseja marcar como global e, em seguida, toque em ![cmppr](assets/cmppr.png).
1. Na barra lateral, ative **Usar valor durante o carregamento** lento.

   ![Campo de carregamento lento na barra lateral](assets/enable-lazy-loading.png)

   O valor agora é marcado como global e estará disponível para uso em scripts mesmo quando o fragmento contido for descarregado.

## Considerações e práticas recomendadas para configurar o carregamento lento {#considerations-and-best-practices-for-configuring-lazy-loading}

Algumas limitações, recomendações e pontos importantes a serem considerados ao trabalhar com carregamento lento são os seguintes:

* É recomendável usar formulários adaptativos baseados em schemas XSD em formulários adaptáveis baseados em XFA para configurar o carregamento lento em formulários grandes. O ganho de desempenho devido à implementação de carregamento lento em formulários adaptativos baseados em XFA é relativamente menor do que o ganho em formulários adaptativos baseados em XSD.
* Não configure o carregamento lento em fragmentos em um formulário adaptável que use **[!UICONTROL Responsive -tudo em uma página sem layout de navegação]** para o painel raiz. Como resultado da configuração do layout Responsivo, todos os fragmentos são carregados simultaneamente em um formulário adaptável. Também pode resultar em desempenho degradado.
* É recomendável não configurar o carregamento lento em fragmentos no primeiro painel que é renderizado ao carregar o formulário adaptável.
* O carregamento lento é compatível com até dois níveis na hierarquia do fragmento.
* Certifique-se de que os campos marcados como globais sejam exclusivos em um formulário adaptável.
* Considere gravar regras de visibilidade para fragmentos que devem ser exibidos ou ocultados com base em uma condição. Por exemplo, você pode mostrar ou ocultar o fragmento Detalhes do Cônjuge com base no status civil especificado por um usuário.
* Os componentes de anexo de arquivo e Termos e condições não são suportados em fragmentos carregados de forma preguiçosa.

### Práticas recomendadas de script para configurar o carregamento lento {#scripting-best-practices-for-configuring-lazy-loading}

Os pontos importantes a serem lembrados ao desenvolver scripts para painéis de carregamento lento são os seguintes:

* Certifique-se de que os scripts de inicialização e cálculo usados nos campos de um fragmento carregado lento estejam desnecessários na natureza. Scripts despotentes são aqueles que têm o mesmo efeito mesmo após várias execuções.
* Use a propriedade de campos globalmente disponível para disponibilizar o valor dos campos localizados em um painel de carregamento lento para todos os outros painéis de um formulário.
* Não encaminhe o valor de referência de um campo dentro de um painel lento, independentemente do campo estar marcado globalmente em fragmentos ou não.
* Use o recurso de redefinição do painel para redefinir tudo o que está visível no painel usando a expressão de clique a seguir.\
   guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;): &quot;navigablePanel&quot;}).resetData()

