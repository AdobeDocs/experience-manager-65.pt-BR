---
title: Introdução à criação de formulários adaptáveis
seo-title: Introduction to authoring adaptive forms
description: O AEM Forms fornece interface fácil de usar, mas eficiente para a criação de formulários adaptáveis. Ele fornece vários componentes e ferramentas que podem ser usadas para criar formulários.
seo-description: AEM Forms provide easy-to-use yet powerful interface for authoring adaptive forms. It provides a host of components and tools that you can use to build forms.
uuid: 3b150507-41b9-47c2-a94c-f85b903b2274
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction, author
discoiquuid: ba70921e-db7e-43f6-902c-1065d3b13aef
docset: aem65
feature: Adaptive Forms
exl-id: 935b734c-6fb1-45e8-8515-e98c8b85286c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3138'
ht-degree: 57%

---

# Introdução à criação de formulários adaptáveis {#introduction-to-authoring-adaptive-forms}

## Visão geral {#overview}

Os formulários adaptáveis permitem criar formulários envolventes, responsivos, dinâmicos e adaptáveis. O AEM Forms fornece uma interface de usuário intuitiva e componentes prontos para uso para criar e trabalhar com formulários adaptáveis. Você pode optar por criar um formulário adaptável com base em um modelo de formulário ou esquema ou sem um modelo de formulário. É importante escolher cuidadosamente o modelo de formulário que atenda não apenas às suas necessidades, mas que amplie seus investimentos de infraestrutura e ativos. Escolha entre as seguintes opções para criar um formulário adaptável:

* **Usar um modelo de dados de formulário**
   [Integração de dados](../../forms/using/data-integration.md) O permite integrar entidades e serviços de diferentes fontes de dados em um modelo de dados de formulário que você pode usar para criar formulários adaptáveis. Escolha o modelo de dados de formulário se o formulário adaptável que você está criando envolver a busca e gravação de dados de e para várias fontes de dados.

* **Usar um modelo de formulário XDP**
Esse é um modelo de formulário ideal se você tiver investido em formulários baseados em XFA ou XDP. Ele fornece uma maneira direta de converter seus formulários baseados em XFA em formulários adaptáveis. Quaisquer regras XFA existentes são mantidas nos formulários adaptáveis associados. Os formulários adaptáveis resultantes são compatíveis com construções XFA, como validações, eventos, propriedades e padrões.

* **Usar uma definição de esquema XML (XSD) ou um esquema JSON**
Os esquemas XML e JSON representam a estrutura na qual os dados são produzidos ou consumidos pelo sistema de back-end na sua organização. Você pode associar o esquema a um formulário adaptável e usar seus elementos para adicionar conteúdo dinâmico ao formulário adaptável. Os elementos do esquema estarão disponíveis para uso na guia Objetos do modelo de dados do navegador de conteúdo ao criar formulários adaptáveis.

* **Uso de nenhum ou sem um modelo de formulário**
Os formulários adaptáveis criados com essa opção não usam nenhum modelo de formulário. O XML de dados gerado desses formulários tem uma estrutura simples com campos e valores correspondentes.

Para obter mais informações sobre como criar um formulário adaptável, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).

## Interface de criação do formulário adaptável {#adaptive-form-authoring-ui}

A interface otimizada para toque para a criação de formulários adaptáveis é intuitiva e fornece:

* Funcionalidade de arrastar e soltar
* Componentes de formulário padrão
* Repositório integrado de ativos

Ao criar um novo formulário adaptável ou editar um formulário adaptável existente, use os seguintes elementos de interface do usuário:

* [Barra lateral](#sidebar)
* [Barra de ferramentas da página](#page-toolbar)
* [Barra de ferramentas Componente](#component-toolbar)
* [Página de formulário adaptável](#af-page)

![Interface de criação do formulário adaptável](assets/formeditor.png)

**A.** Barra lateral **B.** Barra de ferramentas da página **C** Página de formulário adaptável

### Barra lateral {#sidebar}

A barra lateral permite

* Visualize o conteúdo do formulário, como painéis, componentes, campos e layout.
* Edite propriedades de componentes.
* Pesquisar, visualizar e usar ativos no seu repositório de gerenciamento de ativos digitais (DAM) do AEM.
* Adicione componentes ao formulário.

![Barra lateral](assets/sidebar-comps.png)

**A.** Navegador de conteúdo **B.** Navegador de propriedades **C.** Navegador de ativos **D.** Navegador de componentes

<!--Click to enlarge

](assets/sidebar-comps-1.png) -->

A barra lateral inclui os seguintes navegadores:

* **Navegador de conteúdo**
No navegador de conteúdo, é possível ver

   * **Objetos de formulário**
Mostra a hierarquia de objetos do formulário. O autor pode navegar até um componente de formulário específico selecionando esse elemento na Árvore de objetos de formulário. O autor pode pesquisar objetos e reorganizá-los a partir dessa árvore.

   * **Objetos do modelo de dados**
Permite ver a hierarquia do modelo de formulário.
Ela permite arrastar e soltar elementos do modelo de formulário no formulário adaptável. Os elementos adicionados são convertidos automaticamente em componentes de formulário, mantendo suas propriedades originais. É possível ver objetos de modelo de dados quando o formulário usa esquema XML, esquema JSON ou modelo XDP.

* **Navegador de propriedades**

   Permite editar as propriedades de um componente. As propriedades mudam de acordo com um componente. Para ver as propriedades do contêiner de formulário adaptável:

   Selecione um componente e toque em ![nível de campo](assets/field-level.png) > **[!UICONTROL Contêiner de formulário adaptável]** e toque em ![cmppr](assets/cmppr.png).

* **Navegador de ativos**

   Segmenta diferentes tipos de conteúdo, como imagens, documentos, páginas, filmes e assim por diante.

* **Navegador de componentes**

   Inclui componentes que você pode usar para criar um formulário adaptável. Você pode arrastar componentes de para o formulário adaptável para adicionar elementos de formulário e configurar elementos adicionados de acordo com os requisitos. A tabela a seguir descreve os componentes listados no navegador de componentes.

<table>
 <tbody>
  <tr>
   <th><strong>Componente</strong></th>
   <th><strong>Funcionalidade</strong></th>
  </tr>
  <tr>
   <td>Bloco do Adobe Sign</td>
   <td>Adiciona um bloco de texto com espaços reservados para que os campos sejam preenchidos ao assinar usando o Adobe Sign.</td>
  </tr>
  <tr>
   <td>Botão</td>
   <td>Adiciona um botão, que pode ser configurado para executar ações, como salvar, redefinir, prosseguir, voltar e assim por diante.</td>
  </tr>
  <tr>
   <td>Captcha</td>
   <td>Adiciona a validação CAPTCHA usando o serviço Google reCAPTCHA. Para obter detalhes, consulte <a href="../../forms/using/captcha-adaptive-forms.md" target="_blank">Uso de CAPTCHA em formulários adaptáveis</a>.</td>
  </tr>
  <tr>
   <td>Gráfico</td>
   <td>Adiciona um gráfico que pode ser usado em formulários e documentos adaptáveis para representação visual de dados bidimensionais em painéis e linhas de tabela repetíveis.</td>
  </tr>
  <tr>
   <td>Caixa de seleção</td>
   <td>Adiciona uma caixa de seleção.</td>
  </tr>
  <tr>
   <td>Campo de entrada de data</td>
   <td>Use o componente Campo de entrada de data em seu formulário para permitir que os clientes preencham dia, mês e ano separadamente em três caixas. Você pode personalizar a aparência do componente e alterar o formato da data. Por exemplo, você pode permitir que seus clientes insiram as datas no formato MM/DD/AAAA ou DD/MM/AAAA.</td>
  </tr>
  <tr>
   <td>Seletor de data</td>
   <td>Adiciona um campo de calendário para escolher uma data.</td>
  </tr>
  <tr>
   <td>Fragmento do documento</td>
   <td>Permite adicionar componentes reutilizáveis de uma correspondência.</td>
  </tr>
  <tr>
   <td>Grupo de fragmento de documento</td>
   <td>Permite adicionar um grupo de fragmentos de documento relacionados que você pode usar em um modelo de carta como uma única unidade.</td>
  </tr>
  <tr>
   <td>Lista suspensa</td>
   <td>Adiciona uma lista suspensa - seleção única ou múltipla</td>
  </tr>
  <tr>
   <td>Email</td>
   <td><p>Adicione um campo para capturar o endereço de email. O componente Email, por padrão, valida endereços de email usando a seguinte expressão regular.</p> <p><code>^[a-zA-Z0-9.!#$%&amp;’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:.[a-zA-Z0-9-]+)*$</code></p> </td>
  </tr>
  <tr>
   <td>Anexo de arquivo</td>
   <td><p>Adiciona um botão que permite aos usuários navegar e anexar documentos compatíveis a um formulário. Você pode anexar vários arquivos a um componente de anexo de arquivo. Você também pode especificar o **[!UICONTROL Tamanho Máximo do Arquivo]** e **[!UICONTROL Tipos de Arquivos Suportados]** para os anexos no navegador de propriedades do componente. </p> <p><strong> Nota: </strong><ul> <li> O componente não oferece suporte à anexação de arquivos com nomes de arquivo que comecem com caracteres (.), contendo os caracteres \ / : * ? " &lt; &gt; | ; % $ ou contendo nomes de arquivo especiais reservados para o sistema operacional Windows, como nul, prn, con, lpt ou com. </li> <li> Para anexar vários arquivos a um componente de anexo de arquivo aberto no navegador Apple Safari, selecione e anexe arquivos um por um. Não é possível selecionar e anexar vários arquivos de uma só vez.</li> <li>O componente de Anexo de arquivo é compatível com um conjunto predefinido de formatos de arquivo em formulários adaptáveis habilitados para o Adobe Sign. Para obter mais informações, consulte <a href="https://helpx.adobe.com/br/document-cloud/help/supported-file-formats-fill-sign.html#main-pars_text">Formatos de arquivo compatíveis</a>. </li></ul></p> </td>
  </tr>
  <tr>
   <td>Listagem de Anexo de arquivo</td>
   <td>Adiciona um campo que lista todos os anexos enviados usando o componente Anexo de arquivo.</td>
  </tr>
  <tr>
   <td>Cabeçalho<br /> </td>
   <td>Adiciona o cabeçalho da página que normalmente inclui o logotipo de uma corporação, o título do formulário e o resumo.<br /> </td>
  </tr>
  <tr>
   <td>Rodapé</td>
   <td>Adiciona o rodapé da página que normalmente inclui informações sobre direitos autorais e links para outras páginas. </td>
  </tr>
  <tr>
   <td>Imagem</td>
   <td>Permite inserir uma imagem.</td>
  </tr>
  <tr>
   <td>Opção de imagem</td>
   <td>Permite que seus clientes selecionem uma imagem para fornecer informações. Você pode usar as informações para fornecer serviços personalizados aos seus clientes.</td>
  </tr>
  <tr>
   <td>Próximo botão</td>
   <td>Adiciona um botão para navegar para o próximo painel em um formulário.</td>
  </tr>
  <tr>
   <td>Caixa numérica</td>
   <td>Adiciona um campo para capturar valores numéricos</td>
  </tr>
  <tr>
   <td>Escalonador numérico</td>
   <td>Use o Escalonador numérico em seu formulário para permitir que os clientes insiram um valor numérico, o qual eles podem aumentar ou diminuir com base em um passo predefinido.</td>
  </tr>
  <tr>
   <td>Painel</td>
   <td><p>Adiciona um painel ou subpainel.</p> <p>Você também pode adicionar um componente de painel da barra de ferramentas do painel principal usando o botão <span class="uicontrol">Adicionar painel secundário</code>. Da mesma forma, é possível adicionar uma barra de ferramentas específica do painel usando o botão <span class="uicontrol">Adicionar barra de ferramentas do painel</code>. É possível configurar a posição da barra de ferramentas do painel usando a caixa de diálogo Editar painel.</code></code></p> </td>
  </tr>
  <tr>
   <td>Caixa de senha</td>
   <td>Adiciona um campo para capturar uma senha.</td>
  </tr>
  <tr>
   <td>Botão Anterior</td>
   <td>Adiciona um botão que os usuários precisam para retornar à página ou ao painel anterior.</td>
  </tr>
  <tr>
   <td>Botão de opção</td>
   <td>Adiciona botões de opção.</td>
  </tr>
  <tr>
   <td>Botão de redefinição</td>
   <td>Adiciona um botão para redefinir os campos do formulário.</td>
  </tr>
  <tr>
   <td>Botão Salvar</td>
   <td>Adiciona um botão para salvar os dados do formulário.</td>
  </tr>
  <tr>
   <td>Assinatura escrita</td>
   <td>Adiciona um campo para capturar assinaturas escritas.</td>
  </tr>
  <tr>
   <td>Separador</td>
   <td>Permite a separação visual de painéis em seu formulário.</td>
  </tr>
  <tr>
   <td>Etapa de assinatura</td>
   <td>Exibe as informações fornecidas no formulário e os campos de assinatura para o usuário verificar e assinar o formulário.</td>
  </tr>
  <tr>
   <td>Texto</td>
   <td>Permite especificar um texto estático.</td>
  </tr>
  <tr>
   <td>Botão Enviar</td>
   <td>Adiciona um botão enviar para enviar o formulário à ação de envio configurada.</td>
  </tr>
  <tr>
   <td>Etapa de resumo</td>
   <td>Envia o formulário e exibe o texto resumido que os autores especificam após o envio do formulário. </td>
  </tr>
  <tr>
   <td>Alternar</td>
   <td>Adiciona um botão que executa uma ação de alternância ou ativação/desativação. Não é possível adicionar mais de duas opções no componente Alternar. Como um botão de alternância pode ter apenas dois valores: ligado ou desligado, não é possível torná-lo obrigatório. Pelo menos um valor é salvo independentemente da entrada do usuário. <br /> </td>
  </tr>
  <tr>
   <td>Tabela</td>
   <td>Adiciona uma tabela que permite organizar dados em linhas e colunas. </td>
  </tr>
  <tr>
   <td>Telefone</td>
   <td><p>Adicione um campo para capturar o número de telefone. O componente Telefone permite que os autores configurem um dos seguintes tipos de número de telefone. Cada tipo está associado a uma expressão regular padrão para validação.</p>
    <ul>
     <li>O tipo Internacional é validado por <code>^[+][0-9]{0,14}$</code>.</li>
     <li>O tipo USPhoneNumber é validado por <code>{'+1 ('999') '999-9999}</code>.</li>
     <li>O tipo UKPhoneNumber é validado por <code>text{'+'99 999 999 9999}</code>.</li>
     <li>Tipo Personalizado não fornece um padrão de validação modelo. Obtém o valor do último tipo de número de telefone selecionado. Você também pode especificar seu próprio padrão de validação personalizado.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Termos e condições<br /> </td>
   <td>Adiciona um campo que os autores podem usar para especificar os termos e condições para que os usuários revisem antes de preencher o formulário.</td>
  </tr>
  <tr>
   <td>Caixa de texto </td>
   <td><p>Adiciona uma caixa de texto na qual o usuário pode especificar as informações necessárias. </p> <p>Por padrão, o componente Caixa de texto apenas aceita texto sem formatação. Você pode ativar um componente Caixa de texto para aceitar rich text. Um componente de texto Rich text habilitado fornece opções para adicionar cabeçalhos, alterar estilos de caracteres (negrito, itálico, sublinhar os caracteres), criar listas ordenadas e não ordenadas, alterar o plano de fundo do texto e a cor do texto e adicionar hiperlinks. Para ativar o rich text de uma caixa de texto, ative a opção<strong> Permitir Rich text</strong> nas propriedades do componente.</p> </td>
  </tr>
  <tr>
   <td>Título</td>
   <td>Especifica um título para o formulário adaptável.</td>
  </tr>
  <tr>
   <td>Etapa de verificação</td>
   <td><p>Adicione um espaço reservado para exibir o formulário preenchido para verificação por usuário.</p> <p><strong>Nota</strong>: o formulário adaptável que contém o componente Verificar não é compatível com usuários anônimos. Além disso, não é recomendável usar o componente Verificar em um fragmento de formulário adaptável.</p> </td>
  </tr>
 </tbody>
</table>

#### Práticas recomendadas para trabalhar com componentes {#best-practices}

Algumas práticas recomendadas e pontos principais a serem lembrados ao trabalhar com componentes de formulário adaptáveis são os seguintes:

* Cada componente tem propriedades associadas que controlam sua aparência e funcionalidade. Para configurar as propriedades de um componente, toque no componente e ![cmppr](assets/cmppr.png) para abrir as propriedades do componente no navegador Propriedades.
* Um componente é identificado com seu nome de elemento. Ao tocar em ![cmppr](assets/cmppr.png), é possível alterar o nome do componente alterando o **[!UICONTROL Nome do elemento]** no navegador de propriedades. O campo Nome do elemento aceita somente letras, números, hifens (-) e sublinhados (_). Outros caracteres especiais não são permitidos e o nome do elemento deve começar com uma letra.

* Você pode modificar a propriedade Título de um componente de formulário adaptável em linha no editor de formulários sem abrir o navegador Propriedades, desde que o título esteja visível no formulário. Para fazer isso:

   1. Toque para selecionar um componente que tenha uma **[!UICONTROL Título]** propriedade e cuja **[!UICONTROL Ocultar título]** propriedade está desativada.

   1. Toque ![aem_6_3_edit](assets/aem_6_3_edit.png) para tornar o título editável.

   1. Modifique o título e toque na tecla Return ou em qualquer lugar fora do componente para salvar as alterações. Toque na tecla Esc para descartar as alterações.

* Alguns componentes de formulário adaptáveis, como Email e Telefone, incluem padrões de validação prontos para uso. No entanto, você pode especificar a validação personalizada atualizando o **[!UICONTROL Padrão de validação]** sob a opção Padrões nas propriedades do componente. Consulte descrições de componentes na tabela acima para obter mais informações sobre validações padrão.

* Campos de formulários adaptáveis, como Caixa numérica e Email podem ser configurados para incluir tipos de entrada de HTML5 especializados. Quando esses campos estão em foco em dispositivos móveis e tablets, o teclado exibe inicialmente o alfabeto, os números e os caracteres específicos que são normalmente usados para inserir informações nos campos. Isso ajuda os usuários a inserir informações rapidamente, sem precisar alternar entre conjuntos de caracteres no teclado numérico. Para permitir entrada especializada para um componente, ative a opção **[!UICONTROL Usar número do tipo de HTML]** em suas propriedades de componente.

* Você pode ativar um componente Caixa de texto para aceitar rich text. Para habilitar rich text para uma caixa de texto, habilite a opção **[!UICONTROL Permitir Rich Text]** nas propriedades do componente.

* Você pode ativar os componentes Caixa de texto, Email e Telefone para preencher automaticamente valores para campos como nome, endereço, cartão de crédito, telefone e email a partir das informações armazenadas nas configurações de preenchimento automático do navegador. Para ativar esse recurso, selecione **[!UICONTROL Ativar preenchimento automático]** nas propriedades do componente e selecione um **[!UICONTROL Preencher atributo automaticamente]**. Quando um usuário preenche um formulário adaptável, os valores são sugeridos pelo perfil de preenchimento automático no navegador ou com base nos valores preenchidos anteriormente pelo usuário. Observe que o preenchimento automático funciona se as configurações de preenchimento automático no navegador do usuário estiverem ativadas.

* Especificar valores para os itens Botão de opção e Caixa de seleção em `{value}={text}` formato nas propriedades do componente.
* O componente de anexo de Arquivo, por padrão, permite que um usuário anexe apenas um arquivo. No entanto, você pode configurar as propriedades do componente para suportar vários anexos. Além disso, se um usuário anexar vários arquivos com o mesmo nome de arquivo, os anexos poderão causar alguns problemas. Portanto, é recomendável associar um identificador exclusivo para cada anexo enviado no envio do formulário. Para fazer isso:

   1. No servidor do AEM Forms, navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
   1. Localizar e tocar **[!UICONTROL Serviço de configuração adaptável do Forms]**.
   1. Na caixa de diálogo Serviço de configuração do Forms adaptável, ative **[!UICONTROL Tornar Nomes de Arquivos Exclusivos]**. Por padrão, está desativado.

* Para permitir que os usuários anexem um PDF usando o navegador Safari, verifique se **application/pdf** é adicionado à propriedade Tipos de arquivo suportados do componente de anexo de arquivo. Os formulários adaptáveis criados com a versão anterior do AEM Forms podem conter **.pdf** em vez de **application/pdf** na propriedade Tipos de arquivos suportados.

Para obter mais práticas recomendadas sobre formulários adaptáveis, consulte [Práticas recomendadas para trabalhar com formulários adaptáveis](/help/forms/using/adaptive-forms-best-practices.md).

>[!NOTE]
>
>Os componentes do formulário adaptável não são compatíveis com idiomas da direita para a esquerda (RTL). Por exemplo, hebraico.

### Barra de ferramentas da página {#page-toolbar}

A barra de ferramentas da página na parte superior fornece opções que permitem visualizar o formulário, alterar as propriedades do formulário e editar o layout do formulário. É possível visualizar o formulário ao criá-lo e fazer alterações de acordo. Na barra de ferramentas da página, você observa:

* **Alternar painel lateral** ![alternar-painel-lateral](assets/toggle-side-panel.png): Permite exibir ou ocultar a Barra Lateral.

* **Informações da página** ![opções-tema](assets/theme-options.png): permite exibir as propriedades da página, publicar/desfazer a publicação de um formulário, iniciar um fluxo de trabalho de formulário e abrir o formulário na interface clássica.

* **Emulador** ![régua](assets/ruler.png): permite você emular a aparência de seu formulário para diferentes tamanhos de exibição, como tablets e telefones.

* **Editar**: permite selecionar outros modos, como: **[!UICONTROL Editar]**, **[!UICONTROL Estilo]**, **[!UICONTROL Desenvolvedor]** e **[!UICONTROL Design]**.

   * **Editar**: permite editar as propriedades do formulário e seus componentes. Por exemplo, adicionar um componente, soltar uma imagem e especificar campos obrigatórios.
   * **Estilo**: permite estilizar a aparência dos componentes do formulário. Por exemplo, no modo de estilo, é possível selecionar um painel e especificar a cor do plano de fundo.

   * **Desenvolvedor**: permite que um desenvolvedor:

      * Descubra que formulários são compostos.
      * Depure onde e quando está acontecendo, o que, por vezes, ajuda a resolver problemas.
   * **Design**. Permitir ativar ou desativar componentes personalizados ou componentes prontos para uso que não estejam listados na Barra lateral.


* **Visualizar**: permite que você visualize a aparência do formulário ao publicá-lo.

### Barra de ferramentas Componente {#component-toolbar}

![Barra de ferramentas Componente na interface de toque](assets/component-toolbar.png)

Ao selecionar um componente, você visualiza uma barra de ferramentas que permite trabalhar nele. Há opções para recortar, colar, mover e especificar as propriedades dos componentes. As opções são:

A.**Configurar**: ao tocar em **[!UICONTROL Configurar]**, as propriedades do componente ficam visíveis na barra lateral. A configuração dessas propriedades permite personalizar a experiência de captura de dados. Você pode alterar o nome do elemento do componente, especificar o texto do rótulo no campo Título do componente. O nome do elemento permite capturar valores inseridos pelos usuários usando o componente. Nas propriedades do componente, especifique o comportamento do componente e gerencie a entrada do usuário. Configure as propriedades na barra lateral para capturar os dados do usuário e usá-los para processamento adicional. As propriedades para o contêiner de formulário adaptável permitem especificar as bibliotecas do cliente, os Layouts, os Temas, as configurações do Documento de registro, as configurações de salvamento, as configurações de envio e as configurações de metadados.

B.**Copiar**: você pode usar a opção de copiar para copiar um componente e colá-lo em outros lugares do formulário. Quando você cola um componente, o componente colado obtém um novo nome de elemento, mas retém as propriedades do componente copiado.

C **Recortar**: Você pode usar a opção recortar para mover um componente de um local para outro no formulário adaptável.

D. **Excluir**: permite excluir o componente do formulário.

E. **Inserir**: permite inserir um componente acima do componente selecionado.

F. **Colar**: permite colar o componente cortado ou copiado usando as opções descritas acima.

G. **Editar regras**: permite abrir o editor de regras. Para obter mais informações, consulte [Editor de regras](../../forms/using/rule-editor.md).

H. **Grupo**: permite selecionar vários componentes se você deseja cortar, copiar ou colar mais de um componente.

I. **Página principal**: permite selecionar a página principal de um componente. Por exemplo, um campo de texto está em uma subseção, que fica em uma seção. A seção reside no painel raiz da guia, e o contêiner de formulário adaptável é o pai de um painel raiz da guia. Para um componente, você pode observar todas as opções com a hierarquia classificada de baixo para cima.

Por exemplo, se você tocar em **[!UICONTROL Página principal]** numa caixa de texto, é possível ver:

* Subseção
* Seção
* guideRootPanel
* Container de formulário adaptativo

J. **Outros**: fornece mais opções para trabalhar com o componente selecionado.

* Exibir expressão SOM
* Salvar um painel como fragmento (somente para painéis)
* Adicionar painel filho (somente para painéis)
* Adicionar barra de ferramentas do painel (somente para painéis)
* Substituir (exceto para painéis)

### Página de formulário adaptável {#af-page}

A página do formulário adaptável é o formulário real. É como qualquer outra página WCM modelada como o WCM componente `cq:Page`. A imagem a seguir mostra a estrutura de conteúdo de um formulário adaptável típico.

![Estrutura de conteúdo de uma página WCM de formulário adaptável](assets/afstructure.png)

A estrutura de conteúdo normalmente contém os seguintes componentes principais:

* **guideContainer**: A raiz de um formulário adaptável, que está marcada como **[!UICONTROL Início do formulário adaptável]** na interface do formulário adaptável. Nesse componente, você pode especificar:

   * *Layout de dispositivo móvel do formulário adaptável*: define a aparência do formulário em dispositivos móveis.
   * *Página de agradecimento*: define a página para a qual o usuário é redirecionado após enviar o formulário.
   * *Enviar ação*: define como o formulário é processado no servidor depois que o usuário envia o formulário.
   * *Estilo*: especifica o caminho para o arquivo CSS usado para personalizar a aparência do formulário.

* **rootPanel:** O painel raiz de um formulário adaptável. Ele pode conter sub-painéis sob o nó itens. Cada painel, incluindo o painel raiz, pode ter um layout associado a ele. O layout do painel determina como o formulário é posicionado. Por exemplo, no layout Accordion, seus itens são apresentados como etapas Accordion.

* **barra de ferramentas:** Um container de formulário adaptável tem uma barra de ferramentas global associada, que é global para o formulário. Essa barra de ferramentas pode ser adicionada usando o **[!UICONTROL Adicionar barra de ferramentas]** na barra de edição, que permite que se adicionem ações, como Enviar, Salvar, Redefinir e assim por diante.

* **ativos:** esse nó contém informações adicionais usadas para a criação de formulários. Por exemplo, detalhes do modelo de formulário, detalhes de localização e assim por diante).
