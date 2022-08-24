---
title: Criar carta
seo-title: Create Letter
description: 'Este tópico fornece as etapas para criar uma carta, adicionar módulos de dados e anexos a ela e visualizá-la no Gerenciamento de correspondência. '
seo-description: This topic gives you the steps to create a letter, add data modules and attachments to it, and preview it in Correspondence Management.
uuid: b5cdbf01-db85-4ff8-9fda-1489542bffef
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: correspondence-management
discoiquuid: 6cef0bcf-e2f0-4a5a-85a1-6d8a5dd9bd01
feature: Correspondence Management
exl-id: 2f996a50-7c7d-41b6-84b2-523b6609254b
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3982'
ht-degree: 2%

---

# Criar carta {#create-letter}

## Fluxo de trabalho do Gerenciamento de correspondência {#correspondence-management-workflow}

O fluxo de trabalho do Gerenciamento de correspondência consiste em quatro fases:

1. Criação do template
1. Criação do fragmento do documento
1. Criação de cartas
1. Pós-processamento

### Criação do template {#template-creation}

O gráfico a seguir mostra um fluxo de trabalho típico para criar um template de correspondência.

![Fluxo de trabalho para criar um template de correspondência](assets/01.png)

Neste workflow:

1. Os designers de formulários criam layouts e layouts de fragmento usando o Adobe Forms Designer e os carregam em um repositório CRX. Os layouts contêm campos de formulário típicos, recursos de layout como um cabeçalho e rodapé e &quot;áreas de destino&quot; vazias para o posicionamento de conteúdo. Posteriormente, os Application Specialists mapeiam o conteúdo necessário para essas áreas de destino. Mais informações sobre [layout de criação](/help/forms/using/layout-design-details.md).
1. Especialistas em assuntos de assunto dos departamentos Jurídico, Financeiro ou de Marketing, criam e fazem upload de conteúdo, como cláusulas de texto, isenções de responsabilidade, termos e condições, e imagens, como logotipos, que são reutilizadas em vários modelos de correspondência.
1. Os Application Specialists criam modelos de correspondência. O especialista em pedidos

   * Mapeia cláusulas de texto e imagens para áreas de destino nos modelos de layout
   * Define condições/regras para a inclusão de conteúdo
   * Vincula campos e variáveis de layout a modelos de dados subjacentes

1. O autor visualiza a carta e a envia para processamento de publicação. Mais informações sobre [pós-processamento](/help/forms/using/submit-letter-topostprocess.md).

#### Uso de modelos de carta fornecidos com o Gerenciamento de correspondência {#using-letter-templates-provided-with-correspondence-management}

Em vez de criar um modelo de layout do zero, você pode optar por modificar e reutilizar os modelos fornecidos pelo Gerenciamento de correspondência. Você pode usar o designer para modificar rapidamente a marca e os campos de dados e conteúdo dos modelos para atender às necessidades de sua organização. Para obter mais informações sobre modelos de Gerenciamento de correspondência, consulte [Modelos de carta de referência](/help/forms/using/reference-cm-layout-templates.md).

### Criação do fragmento do documento {#document-fragment-creation}

Fragmentos de documento são partes reutilizáveis\componentes de uma correspondência usando letras\correspondência.

Os fragmentos de documento são dos seguintes tipos:

#### Texto {#text}

Um ativo de texto é uma parte do conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico. Um parágrafo dinâmico contém referências a elementos de dados, cujos valores são fornecidos em tempo de execução.

#### Lista {#list}

A lista é uma série de fragmentos de documento, incluindo texto, listas (a mesma lista não pode ser &quot;adicionada em si mesma), condições e imagens. A ordem dos elementos da lista pode ser corrigida ou editável. Ao criar uma carta, você pode usar alguns ou todos os elementos da lista para replicar um padrão reutilizável de elementos.

#### Condição {#condition}

As condições permitem definir qual conteúdo é incluído no momento da criação da correspondência, com base nos dados fornecidos. A condição é descrita em termos de variáveis de controle. As variáveis podem ser um elemento de dicionário de dados ou um espaço reservado. Ao adicionar uma condição, você pode optar por incluir um ativo com base no valor que a variável de controle tem. As condições têm uma única saída com base em uma expressão. A primeira expressão é encontrada como verdadeira, com base na variável de condição atual. Seu valor se torna a saída da condição.

#### Fragmento de layout {#layout-fragment}

Um fragmento de layout é um layout que pode ser usado em uma ou mais letras. Um fragmento de layout é usado para criar padrões repetíveis, especialmente tabelas dinâmicas. O layout pode conter campos de formulário típicos, como &quot;Endereço&quot; e &quot;Número de referência&quot;. Também contém subformulários vazios que indicam áreas de destino. Os layouts (XDPs) são criados no Designer e, em seguida, são [carregado no Forms e Documentos](/help/forms/using/get-xdp-pdf-documents-aem.md).

### Criação de cartas {#letter-creation}

Há duas maneiras de gerar a correspondência enviada aos clientes: orientada pelo usuário e pelo sistema.

#### Orientado pelo usuário {#user-driven}

Os funcionários voltados para o cliente, como os ajustadores de solicitações ou os funcionários de caso, podem criar correspondência personalizada. Usando uma interface de preenchimento de cartas simples e intuitiva, os usuários empresariais podem adicionar texto opcional à correspondência, personalizar conteúdo editável ao visualizar a correspondência em tempo real. Em seguida, eles podem enviar a correspondência personalizada para um processo de back-end.

![Correspondência personalizada e orientada pelo usuário](assets/02.png)

#### Orientado pelo sistema {#system-driven}

A geração da correspondência é automatizada, impulsionada por acionadores de eventos. Por exemplo, um aviso de lembrete enviado a um cidadão solicitando o depósito prévio de imposto é gerado pela fusão do modelo predefinido com dados do cidadão. A carta final pode ser enviada por email, impressa, enviada por fax ou arquivada.

![Correspondência orientada pelo sistema](assets/us_cm_generate.png)

### Pós-processamento {#post-processing}

A correspondência final pode ser enviada a um processo de back-end para pós-processamento. A correspondência pode ser:

1. Processado para impressão por email, fax ou em lote ou colocado em uma pasta para impressão ou e-mail.
1. Enviado para revisão e aprovação.
1. Protegido pela aplicação de assinaturas digitais, certificação, criptografia ou gerenciamento de direitos.
1. Convertido em um documento PDF pesquisável que contém todos os metadados necessários para fins de arquivamento e auditoria.
1. Incluído em um PDF que inclui mais documentos, como material de marketing. O PDF pode então ser enviado como a correspondência final.

### Arquitetura da solução de gerenciamento de correspondência {#correspondence-management-solution-architecture}

O gráfico a seguir fornece uma visão geral de uma arquitetura de exemplo da Solução Letters.

![Arquitetura da solução alfabética](assets/us_cm_architecture_es3.png)

## Desconstrução de uma carta {#deconstructing-a-letter}

Este documento de Aviso de Cancelamento é um exemplo de uma correspondência típica:

![Um exemplo de carta de cancelamento](assets/5_deconstructingaletter.png)

<table> 
 <tbody> 
  <tr> 
   <td><strong>Elementos de carta</strong></td> 
   <td><strong>Descrição</strong></td> 
   <td><strong>Formado por</strong></td> 
  </tr> 
  <tr> 
   <td>Dados de sistemas empresariais back-end</td> 
   <td>Dados provenientes de sistemas de empresas de back-end. Os dados são unidos dinamicamente ao template de correspondência.</td> 
   <td>O<br /> Arquivo de dados criado com base em um Dicionário de dados</td> 
  </tr> 
  <tr> 
   <td>Dados<br /> Inserido por Funcionário de Linha de Frente</td> 
   <td>Dados que podem ser fornecidos por um funcionário front-line que está personalizando a carta antes de enviá-la.<br /> </td> 
   <td><p>Elementos de DD não protegidos<br /> Parágrafos de texto editáveis<br /> Variáveis/espaços reservados<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>Pré-aprovado<br /> Parágrafos de texto</td> 
   <td>Conteúdo de texto pré-aprovado. Especialistas em assuntos legais, financeiros ou de uma linha de negócios que entendem o contexto comercial da carta, normalmente criam o conteúdo do texto. Conteúdo como cabeçalho, rodapé, isenções de responsabilidade e saudação seria comum à maioria das letras. No entanto, conteúdo como "motivo para rescisão" seria específico para a carta específica.</td> 
   <td><p>Texto\Listas\<br /> Condições\Layout</p> <p> </p> </td> 
  </tr> 
  <tr> 
   <td>Dados<br /> Com base na lógica personalizada ?</td> 
   <td>Para algumas cartas, como uma carta para solicitar mais informações sobre uma solicitação, usuários como o Ajustador de solicitações podem adicionar conteúdo de texto personalizado.</td> 
   <td>Documento<br /> Fragmento do tipo Condição </td> 
  </tr> 
  <tr> 
   <td>Armazenado<br /> Imagens do Repositório Central</td> 
   <td>Imagens como logotipos e imagens de assinatura. Imagens como logotipos corporativos seriam exibidas na maioria ou em toda a correspondência. As imagens de assinatura são específicas da carta e da pessoa em cujo nome a carta é enviada.</td> 
   <td><p>Imagens armazenadas AEM ativos (DAM)<br /> </p> <p> </p> </td> 
  </tr> 
 </tbody> 
</table>

## Analise uma carta antes de construí-la {#analyze-a-letter-before-you-construct-it}

Analise cada carta para descobrir as várias partes que compõem a carta. O Application Specialist analisa as correspondências geradas.

* Quais partes da correspondência são estáticas e quais são dinâmicas. As variáveis preenchidas a partir de fontes de dados de backend ou por usuários finais.
* A ordem em que os vários parágrafos de texto aparecem na correspondência, como se um usuário empresarial pudesse alterar parágrafos durante a criação da correspondência.
* O sistema de correspondência é gerado ou requer um usuário final para editar a correspondência? Quantas correspondências são geradas pelo sistema e quantas exigem a intervenção do usuário?
* Com que frequência o modelo de correspondência muda? Irá ser atualizado anualmente, trimestralmente ou apenas quando uma determinada legislação mudar? Que tipo de alterações é esperado? É uma alteração para corrigir erros tipográficos, uma alteração de layout, adição de mais campos, adição de mais parágrafos e assim por diante.
* Ao planejar seus requisitos de correspondência, monte a lista de novos modelos de correspondência. Para cada template de correspondência, é necessário:

   * Cláusulas de texto, imagens e tabelas
   * Valores de dados de sistemas de back-end
   * Layouts de layout e fragmentos da correspondência
   * A ordem em que o conteúdo aparece na carta e as regras para inclusão e exclusão de conteúdo

* As condições em que os usuários empresariais, como ajustadores de solicitações ou trabalhadores de caixa, modificam o conteúdo ou partes da carta.
* Os cenários são narrativas que descrevem a experiência do usuário, os requisitos e os benefícios de usar a Solução Letters.
* Os cenários também fornecem:os conjuntos de habilidades e as ferramentas necessárias para o seu projeto.
* Práticas recomendadas para planejar sua implementação. &quot;Visão geral da implementação de alto nível.

## Benefícios da realização da análise {#benefits-of-performing-the-analysis}

**Reutilização de conteúdo** Você tem uma lista consolidada de novo conteúdo necessário para gerar correspondência. Grande parte do conteúdo, como cabeçalhos, rodapés, isenções de responsabilidade e introduções, é comum a muitas letras e pode ser reutilizada em várias letras. Todo esse conteúdo comum pode ser criado e aprovado por especialistas uma vez e depois reutilizado em muitas peças de correspondência.

**Criação do dicionário de dados** Haverá valores de dados, como &quot;ID do cliente&quot; e &quot;Nome do cliente&quot;, comuns a muitas cartas. Você pode preparar uma lista consolidada de todos esses valores de dados. Normalmente, alguém da equipe de middleware da empresa é consultado ao planejar a estrutura. Essa é a base para criar o Dicionário de dados.

**Fornecimento de dados a partir de sistemas de backend para empresas** Você também saberá todos os valores de dados necessários e de onde os dados do sistema empresarial são obtidos. Em seguida, você pode arquitetar a implementação para extrair os dados do sistema empresarial e alimentar a solução Letters.

**Estimativa da complexidade das letras** É importante determinar a complexidade de criar uma determinada correspondência. Essa análise ajuda a determinar a quantidade de tempo e conjuntos de habilidades que serão necessários para criar os modelos de carta. Isso, por sua vez, ajudará na estimativa de recursos e custos da implementação da solução Cartas.

## Complexidade da correspondência {#correspondence-complexity}

A complexidade da correspondência pode ser determinada pela análise dos seguintes parâmetros:

**Complexidade do layout** Qual é a complexidade do layout? Cartas como o Aviso de cancelamento têm layouts simples. Enquanto letras como Confirmação de cobertura de solicitações tem um layout complexo com várias tabelas e mais de 60 campos de formulário. A criação de layouts complexos leva mais tempo e requer conjuntos avançados de habilidades de design de layout.

**Número de parágrafos e condições de texto** Um contrato de empréstimo pode ter 10 páginas e conter mais de 40 cláusulas de texto. Muitas destas cláusulas dependeriam de &quot;parâmetros de empréstimo&quot;. Com base nos termos e condições exatos, as cláusulas seriam incluídas ou excluídas do contrato. A criação dessas cartas requer um planeamento minucioso e uma definição cuidadosa das condições complexas.

Esta tabela fornece algumas diretrizes que podem ser usadas para classificar suas cartas:

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Nível de complexidade</strong></p> </td> 
   <td><p><strong>Complexidade de layout (subjetiva)</strong></p> </td> 
   <td><p><strong>Número de parágrafos de texto</strong></p> </td> 
   <td><p><strong>Número de textos ou imagens condicionais</strong></p> </td> 
   <td><p><strong>Conjunto de habilidades necessário</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Baixa complexidade</p> </td> 
   <td><p>Baixa. O layout tem poucos campos de formulário (&lt;15).</p> <p>Normalmente, uma página<span class="acrolinxCursorMarker"></span>.</p> </td> 
   <td><p>8</p> </td> 
   <td><p>1</p> </td> 
   <td><p>Habilidades do Designer médio.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Complexidade média</p> </td> 
   <td><p>Layout de média complexidade. Inclui estruturas como tabelas. Normalmente, tem mais de uma página.</p> </td> 
   <td><p>16</p> </td> 
   <td><p>2</p> </td> 
   <td><p>Habilidades do Designer médio.</p> <p> </p> <p>Capacidade de criar expressões complexas usando interfaces do usuário.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Alta complexidade</p> </td> 
   <td><p>Layout complexo. Pode ser maior que três páginas. Contém tabelas e mais de 60 campos de formulário.</p> </td> 
   <td><p>40</p> </td> 
   <td><p>8</p> </td> 
   <td><p>Habilidades do Expert Designer.</p> <p> </p> <p>Capacidade de criar expressões complexas usando interfaces do usuário.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Visão geral da criação de uma carta {#overview-of-creating-a-letter}

1. Selecione o layout apropriado que serve como a base da carta e crie uma carta.
1. Adicione módulos de dados ou fragmentos de layout à letra e configure-os.
1. Escolha visualizar a correspondência.
1. Edite e configure os campos, variáveis, conteúdo e anexos.

### Pré-requisitos {#prerequisites}

Primeiro, você precisa do seguinte em vigor para criar uma correspondência:

* [Pacote de Compatibilidade](compatibility-package.md). Instale o Pacote de Compatibilidade para visualizar o **Letras** na **Forms** página.
* A letra XDP ([layout](/help/forms/using/document-fragments.md)).
* Outros XDPs ([fragmentos de layout](document-fragments.md#document-fragments)) que formam partes da carta. Os XDPs\Layouts são criados em [Designer](http://www.adobe.com/go/learn_aemforms_designer_65).
* Os [dicionário de dados](/help/forms/using/data-dictionary.md) (Opcional).
* O [módulos de dados](/help/forms/using/document-fragments.md) deseja usar na correspondência.
* [Testar dados](/help/forms/using/data-dictionary.md#p-working-with-test-data-p) é o arquivo XML com os dados de teste inseridos nele. Os dados de teste são necessários se você estiver usando um dicionário de dados.

## Criar um modelo de carta {#create-a-letter-template}

### Selecione um layout e insira as propriedades de letras {#select-a-layout-and-enter-the-letter-properties}

1. Selecionar **Forms** > **Letras**.

1. Selecionar **Criar > Carta**. O Gerenciamento de correspondência exibe os layouts disponíveis (XDPs). Esses layouts vêm do Designer. Os layouts também incluem os templates de carta que o Gerenciamento de correspondência fornece prontos para uso. Para obter mais informações sobre modelos de Gerenciamento de correspondência, consulte [Modelos de carta de referência](/help/forms/using/reference-cm-layout-templates.md). Para adicionar seus próprios layouts, crie arquivos XDP (layout) no Designer e [carregá-los no AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md).

   ![create-letter](assets/create-letter.png)

1. Selecione um layout ao tocar nele e tocar em **Próximo**.

   ![Selecione o layout para criar uma carta](assets/selectlayout.png)

1. Insira as propriedades da Correspondência e toque em **Salvar:**

   * **Título (Opcional):** Insira o título da carta. O título não precisa ser exclusivo e pode ter caracteres especiais e caracteres que não sejam inglês.
   * **Nome:** O nome exclusivo da carta. Não podem existir duas letras em nenhum estado com o mesmo nome. No campo Nome , é possível inserir somente caracteres, números e hifens em inglês. O campo Nome é automaticamente preenchido com base no campo Título . Os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hífens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor.
   * **Descrição (Opcional):** Descreva a carta de referência.
   * **Dicionário de dados (opcional)**: O Dicionário de dados pode ser associado à correspondência. Os ativos que você inserir posteriormente nesta correspondência devem ter o mesmo dicionário de dados que o escolhido para a correspondência aqui ou nenhum dicionário de dados.
   * **Tags (Opcional):** Selecione as tags para aplicar à correspondência. Você também pode digitar um nome de tag novo/personalizado e pressionar Enter para criá-lo.
   * **Pós-processo (Opcional):** Selecione o processo de postagem a ser aplicado ao modelo de carta. Há processos de postagem prontos e os que você criou usando AEM, como email e impressão.

   ![Propriedades de correspondência](assets/createcorrespondenceproperties.png)

1. O sistema exibe uma mensagem: &quot;Carta criada com êxito.&quot; (na mensagem de alerta) Toque em **Abrir** para configurar os módulos de dados e os fragmentos de layout nele. Ou toque **Concluído** para retornar à página anterior.

   ![Mensagem de alerta: carta criada com êxito](assets/createcorrespondencecreated.png)

   **Próximo**: Ao tocar **Abrir**, o Gerenciamento de correspondência exibe uma representação do layout com todos os componentes do layout (XDP) listados. Vá em frente com a inserção da variável [Módulos de dados e fragmentos de layout e configuração](/help/forms/using/create-letter.md#p-insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them-p).

### Inserir módulos de dados e fragmentos de layout em uma carta e configurá-los {#insert-data-modules-and-layout-fragments-in-a-letter-and-configure-them}

Depois de criar uma correspondência, toque em Abrir, o Gerenciamento de correspondência exibe uma representação do layout com todos os subformulários/áreas de destino no layout (XDP) listado. Em cada uma das áreas de destino, você pode optar por inserir um Módulo de dados ou um Fragmento de layout (e, em seguida, módulos de dados no fragmento de layout).

>[!NOTE]
>
>Você também pode optar por tocar no ícone Editar para uma carta na página Letras para Inserir módulos de dados e fragmentos de layout em uma carta e configurá-los.

1. Toque **Inserir** para cada um dos subformulários e selecione Módulos de dados ou um Fragmento de layout a ser inserido em cada um dos subformulários.

   ![Inserir módulos de dados e fragmentos de layout](assets/insertdmandlf.png)

1. Selecione Módulo de dados ou Fragmento de layout para essas opções de cada um dos subformulários e escolha os Módulos de dados ou Fragmentos de layout a serem inseridos. Um fragmento de layout permite inserir módulos de dados ou fragmentos de layout nele de acordo com seu design (até quatro níveis).

   ![nestedlf](assets/nestedlf.png)

1. Se um fragmento de layout for inserido, o nome do fragmento de layout aparecerá no subformulário. E de acordo com o fragmento selecionado, subformulários aninhados aparecem no subformulário.
1. Depois que os Módulos de dados selecionados forem inseridos no layout, toque no modo de configuração e defina o seguinte após tocar no ícone Editar para cada um dos módulos:

   1. **Editável**: Quando essa opção é selecionada, o conteúdo pode ser editado na interface do usuário Criar correspondência . Marque o conteúdo como editável somente se ele exigir que o usuário empresarial (como um Ajustador de solicitações) o modifique.
   1. **Obrigatório**: Quando essa opção é selecionada, o conteúdo é necessário na interface do usuário Criar correspondência .
   1. **Selecionado**: Quando essa opção é selecionada, o conteúdo é selecionado por padrão na interface do usuário Criar correspondência .
   1. **Recuo**: Aumente ou diminua o recuo do módulo/conteúdo na letra. O recuo é especificado em termos de níveis, começando em 0. Cada nível recua 36pts. Para obter mais informações sobre como personalizar formulários, consulte **[!UICONTROL Configurações de gerenciamento de correspondência]** em [Fluxo de trabalho do Forms](submit-letter-topostprocess.md#formsworkflow).
   1. **Quebra de página antes de**: Se você definir a Quebra de página antes como ativada, o conteúdo DESTE módulo sempre será exibido em uma nova página.
   1. **Quebra de página depois de**: Se você definir a Quebra de página depois de para um módulo específico, o conteúdo do módulo AVANÇAR sempre será exibido em uma nova página.

   ![Módulos de dados e fragmentos de layout inseridos](assets/insertdmandlf2.png)

1. Para editar um módulo, toque no ícone Editar ao lado dele. Depois de editar os módulos, toque em **Salvar**.

   Nesta página, você também pode fazer o seguinte para os subformulários:

   1. **Permitir texto livre**: Se a opção Permitir texto livre estiver ativada, o usuário poderá adicionar texto em linha na exibição de CCR. Na visualização de CCR, uma ação &#39;T&#39; é ativada para as áreas de destino que têm a opção Permitir texto livre ativada e, quando o usuário a tocar, solicita o nome e a descrição do texto e, ao tocar, abre o texto no modo de edição, onde o usuário pode adicionar texto. Isso funciona como outros módulos de texto
   1. **Bloquear ordem**: Bloqueia a ordem dos subformulários na letra. O autor não tem permissão para reordenar os subformulários/componentes ao criar a carta.

   Nesta página, você também pode fazer o seguinte para cada um dos ativos nos subformulários:

   1. **Alterar a ordem dos ativos**: arraste e solte um ativo com o ícone de reordenar para um ativo ( ![dragnódromo](assets/dragndrop.png)).
   1. **Excluir ativos**: Toque no ícone Excluir ao lado de um ativo para excluí-lo.
   1. **Visualizar ativos**: Toque no ícone de visualização mostrar ( ![showpreview](assets/showpreview.png)) ao lado de um ativo.


1. Toque **Próximo**.
1. A página Dados detalha como os campos de dados e as variáveis são usados no modelo. Os dados podem ser vinculados a fontes de dados, como um dicionário de dados ou uma entrada do usuário. Cada campo define as propriedades a partir das quais o dicionário de dados mapeia dados ou qual legenda é exibida para os campos de entrada do usuário.

   Ligação:

   * O **campo** Os elementos podem ser vinculados a um literal, a um elemento de dicionário de dados, a um ativo ou a um valor especificado pelo usuário. Você também pode ignorar um elemento de campo vinculando-o à opção Ignorar .
   * O **variável** Os elementos podem ser vinculados a um literal, a um elemento de dicionário de dados, a um campo, a uma variável, a um ativo ou a um valor especificado pelo usuário.

   A seguir estão alguns campos principais no link :

   * **Várias linhas**: É possível especificar se a entrada de dados de um campo ou variável é de várias linhas. Se você selecionar essa opção, a caixa de entrada do campo ou da variável será exibida como uma caixa de entrada de várias linhas na Exibição da edição de dados. O campo ou variável também é exibido como várias linhas nas visualizações de Dados e Conteúdo na interface do usuário Criar correspondência . O campo de entrada de várias linhas é semelhante ao campo para inserir um comentário em um TextModule. A opção de várias linhas está disponível somente para campos e variáveis com o tipo de link Usuário ou Elementos de dicionário de dados desprotegidos.
   * **Opcional**: Você pode especificar se o valor do campo ou da variável é opcional ou não. A opção de campo opcional está disponível para campos e variáveis com o tipo de link Usuário ou Elementos de dicionário de dados desprotegidos.

   * **Validação de campo/variável**: Para fornecer uma validação aprimorada do valor de um campo ou variável, é possível atribuir um validador ao campo ou à variável. Essa opção está disponível somente para campos e variáveis com link tipo Usuário ou Elementos de dicionário de dados desprotegidos.
   * **Legenda** e **Dica de ferramenta**: Legenda é o rótulo do campo que aparece antes do campo na interface do usuário do CCR. Essa opção está disponível para campos e variáveis com link tipo Usuário ou Elementos de dicionário de dados desprotegidos.

   A seguir estão os tipos de validação que você pode usar para os campos:

   * **Validador de cadeia de caracteres**: Use o Validador de cadeia de caracteres para especificar um comprimento mínimo e máximo da cadeia de caracteres inserida no campo ou na variável . Ao criar um Validador de cadeia de caracteres, especifique parâmetros de validação válidos. Insira um comprimento válido para os valores mínimo e máximo. Para o validador de cadeia de caracteres, você pode especificar o comprimento mínimo e máximo do valor que pode ser inserido. Se o valor inserido não estiver de acordo com os valores mín. e máx. especificados, o campo relevante na interface do usuário do CCR será marcado em vermelho.

   * **Validador de número**: Use o Validador de números para especificar o valor numérico mínimo e máximo inserido em um campo ou variável. Ao criar um Validador de números, especifique parâmetros de validação válidos. Insira valores numéricos para os valores mínimo e máximo.

   * **Validador de expressão regular**: Use o Validador de expressão regular para definir uma expressão regular usada para validar o valor de um campo ou variável. Além disso, você pode personalizar a mensagem de erro. Ao criar um Validador de expressão regular, especifique uma expressão regular válida.
   >[!NOTE]
   >
   >Os validadores de campo e variável só estão disponíveis em campos ou variáveis com o tipo de link Usuário ou Elementos de dicionário de dados desprotegidos.

   ![ligações](assets/linkages.png)

1. Depois de especificar o link, toque em **Próximo**. O Gerenciamento de correspondência exibe a tela Anexos .

### Configurar os anexos {#set-up-the-attachments}

1. Selecionar **Adicionar ativo**.
1. Na tela Selecionar ativo , toque nos ativos para anexar com a letra e toque em **Concluído**. Primeiro, é necessário fazer upload dos ativos para os Ativos. É recomendável anexar apenas documentos do PDF e do Microsoft Office, mas também pode anexar imagens. Para obter mais informações sobre como fazer upload de ativos no DAM, consulte [Fazer upload de ativos](/help/assets/manage-assets.md).
1. Para bloquear a ordem dos ativos na lista, de modo que o Ajustador de Reivindicações não possa alterar a ordem, toque em **Bloquear ordem**. Se você não selecionar esta opção, o Ajustador de Reivindicações poderá alterar a ordem dos itens da lista.
1. Para alterar a ordem dos ativos, arraste e solte um ativo contendo o ícone de reordenação de um ativo ( ![dragnódromo](assets/dragndrop.png)).
1. Toque **Editar** na frente de um anexo e especifique um anexo como Obrigatório se não quiser que o autor o exclua. Especifique um anexo como Selecionado se desejar que ele seja pré-selecionado na interface do CCR.
1. Selecionar **Acesso à biblioteca** para conceder acesso à biblioteca. Se o Acesso à biblioteca estiver ativado, o Ajustador de solicitações poderá acessar a biblioteca de conteúdo ao criar uma carta e inserir anexos.
1. Selecionar **Configuração de anexos** e especifique o número máximo de anexos.

1. Toque **Salvar**. Sua correspondência é criada e listada na página Cartas.

Depois que um modelo de carta é criado no Gerenciamento de correspondência, o usuário final/agente/ajustador de solicitação pode abrir a carta na interface do usuário do CCR e criar uma correspondência inserindo dados, configurando o conteúdo e gerenciando anexos. Para obter mais informações, consulte [Criar correspondência](/help/forms/using/create-correspondence.md).

## Tipos de vinculação disponíveis para cada um dos campos {#types-of-linkage-available-for-each-of-the-fields}

A tabela a seguir descreve quais tipos de vinculação estão disponíveis para vários tipos de campos.

Os seguintes valores na tabela

* **Sim**: O tipo de campo na coluna mais à esquerda oferece suporte a esse tipo de mapeamento
* **Não**: O tipo de campo na coluna mais à esquerda não é compatível com esse tipo de mapeamento
* **N/D**: O tipo de campo na coluna mais à esquerda não é aplicável

<table> 
 <tbody> 
  <tr> 
   <td> </td> 
   <td><strong>Literal</strong></td> 
   <td><strong>Ativo</strong></td> 
   <td><strong>Dicionários de dados</strong></td> 
   <td><strong>Ignorar</strong></td> 
   <td><strong>Usuário</strong></td> 
   <td><strong>Texto</strong></td> 
   <td><strong>Variável</strong></td> 
  </tr> 
  <tr> 
   <td><strong>date</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/A</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>time</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>datetime</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>integer</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim<br /> </td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>float</strong></td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim<br /> </td> 
   <td>N/D</td> 
   <td>N/A<br /> </td> 
  </tr> 
  <tr> 
   <td><strong>richtext</strong></td> 
   <td>Sim</td> 
   <td>somente texto</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>plain</strong> <strong>texto</strong></td> 
   <td>Sim</td> 
   <td>somente texto</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>Sim</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>imagem</strong></td> 
   <td>Não</td> 
   <td>somente imagem</td> 
   <td>Não</td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>N/D</td> 
   <td>N/D</td> 
  </tr> 
  <tr> 
   <td><strong>signature</strong></td> 
   <td>Não</td> 
   <td>Não</td> 
   <td>Não<br /> </td> 
   <td>Sim</td> 
   <td>Não</td> 
   <td>N/D</td> 
   <td>N/D<br /> </td> 
  </tr> 
 </tbody> 
</table>

## Criar cópia de um modelo de carta {#createcopylettertemplate}

Você pode usar um modelo de carta existente para criar rapidamente um modelo de carta com propriedades, conteúdo e ativos herdados semelhantes, como fragmentos de documento e dicionário de dados. Para fazer isso, copie e cole uma carta.

1. Na página Cartas, selecione uma ou mais letras. A interface do usuário exibe o ícone Copiar .
1. Toque em Copiar. A interface do usuário exibe o ícone Colar. Você também pode optar por entrar em uma pasta antes de colar. Pastas diferentes podem conter ativos com os mesmos nomes. Para obter mais informações sobre pastas, consulte [Pastas e ativos organizacionais](/help/forms/using/import-export-forms-templates.md#folders-and-organizing-assets).
1. Toque em Colar. A caixa de diálogo Colar é exibida. Se você estiver copiando e colando as letras no mesmo lugar, o sistema atribui automaticamente nomes e títulos às novas cópias de letras, mas você poderá editar os títulos e nomes das letras.
1. Se necessário, edite o Título e o Nome com os quais deseja salvar a cópia da carta.
1. Toque em Colar. A cópia da carta é criada. Agora você pode fazer as alterações necessárias na carta recém-criada.
