---
title: Personalização
description: Saiba mais sobre a personalização no Adobe Experience Manager para fornecer ao usuário um ambiente personalizado que exibe conteúdo dinâmico.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 3a550a33-b54b-4217-b9a6-b5a7971276ee
solution: Experience Manager, Experience Manager Sites
feature: Administering,Personalization
role: Admin
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 2%

---

# Personalização {#personalization}

## O que é o Personalization? {#what-is-personalization}

Há um volume cada vez maior de conteúdo disponível hoje, seja na Internet, extranet ou sites de intranet.

O Personalization se concentra em fornecer ao usuário um ambiente personalizado que exibe o conteúdo dinâmico que é selecionado de acordo com suas necessidades específicas; seja com base em perfis predefinidos, seleção de usuário ou comportamento interativo do usuário.

Há três elementos principais envolvidos na personalização:

### Usuários {#users}

* Ter perfis individuais e em grupo. Esses perfis contêm características (como descrição do trabalho, localização, interesses) que podem ser usadas para personalizar o conteúdo que podem ver.
* Execute ações. Eles podem ser analisados e comparados com regras de comportamento para adaptar o conteúdo que veem.

### Conteúdo {#content}

* É o que o usuário deseja ver. De preferência conteúdo de interesse, e uso, para eles para o cumprimento de suas tarefas.
* Podem ser categorizadas e, portanto, disponibilizadas aos usuários de acordo com regras predefinidas.
* Deve ser dinâmico.

Em outras palavras, o conteúdo deve, de alguma forma, ser dependente do usuário. Se cada usuário visualizar o mesmo conteúdo, a personalização será redundante.

### Regras {#rules}

* Defina como a personalização realmente acontece: qual conteúdo o usuário pode ver e quando.

O Personalization pode ser:

#### Explícito {#explicit}

* Personalização: o usuário faz seleções a partir de uma seleção de fontes de conteúdo.

#### Implícito {#implicit}

* Regras baseadas: os gerentes de negócios definem regras específicas para ações com base em perfis e/ou comportamentos específicos.
* Filtragem simples: as seleções são feitas com base em perfis predefinidos no nível do usuário e/ou do grupo.
* Filtragem colaborativa/por recomendação: o comportamento do usuário é registrado de acordo com as regras predefinidas. Essas regras se baseiam no comportamento observado com indivíduos com ideais semelhantes. As informações coletadas são usadas para personalizar as informações exibidas para o usuário, principalmente na forma de recomendações.

## Como e quando o Personalization pode ser usado? {#how-and-when-can-personalization-be-used}

O Personalization pode ser usado em muitos casos, por exemplo:

### Páginas da Intranet {#intranet-pages}

* O conteúdo pode ser oferecido com base no local, departamento e/ou função de um usuário - já definido em uma rede interna.
* Dependendo da escolha disponível, o usuário poderá fazer outras seleções.

### Grupos De Usuários Específicos, Limitados E Alvo - Extranets {#extranets}

* Os usuários exigem um logon para autorização; isso será vinculado a um perfil que fornece as informações necessárias para personalização; possivelmente detalhes como localização, relacionamento com o produto, histórico de uso, responsabilidades orçamentárias e assim por diante.
* Essas instâncias podem variar em sites como:
* Empresas que fornecem sites para uma seção altamente especializada de seu mercado, por exemplo, uma empresa farmacêutica que fornece um site especializado para médicos.
* Empresas que fornecem sites que permitem que seus clientes visualizem informações atuais de conta e faturamento; por exemplo, provedores de telefone.

### Site de Vendas e Distribuição {#sales-site}

* Sites de vendas e distribuição, como o Amazon, podem combinar o perfil do usuário, o histórico de vendas do usuário e seu histórico de navegação para fazer sugestões sobre o que pode interessar o usuário em seguida.

### Pesquisar sites {#search-site}

* Muitos dos principais sites de mecanismos de pesquisa têm ferramentas analíticas muito poderosas que registram o comportamento do usuário, os termos de pesquisa que eles usam e os sites que eles realmente visitam. Isso é usado para personalizar o conteúdo fornecido, principalmente em relação à exibição de anúncios.

### Pontos fortes do Personalization e pontos a serem considerados {#strengths-of-personalization-and-points-to-consider}

Os motivos pelos quais a personalização deve ser usada são:

* Um usuário pode experimentar um site confortável e focado.
* O Personalization pode ser usado para propagar automaticamente o acesso à versão mais recente do conteúdo.
* Os recursos de colaboração social estão disponíveis para que os usuários se comuniquem entre si, pois podem ser identificados por seus perfis.
* Um usuário pode receber o conteúdo de que precisa para realizar uma tarefa específica. Na intranet de uma empresa, isso pode fornecer uma ferramenta inestimável para a disseminação de informações.
* Um usuário pode receber o conteúdo de que precisa/deseja, reduzindo o tempo que precisa para executar operações de pesquisa.
* O provedor de conteúdo pode orientar o conteúdo a ser visto por categorias específicas de usuários.
* As regras podem ser definidas para fornecer conteúdo com base em combinações de características e comportamento do usuário. Isso fornece um mecanismo sofisticado para personalizar a experiência online.

Ao usar a personalização, considere o seguinte:

#### Desempenho {#performance}

* Naturalmente, a análise e a avaliação suplementares têm impacto no desempenho. No entanto, os métodos usados são altamente sofisticados e podem ser otimizados para minimizar o impacto.

#### Autorização {#authorization}

* O Personalization requer um mecanismo de logon, pois o site deve ser capaz de identificar o usuário.

#### Armazenamento em cache {#caching}

* O armazenamento em cache é um aspecto que o usuário verá em termos de desempenho e precisão: a rapidez com que o site fornece conteúdo personalizado e ele está sempre atualizado.
* O armazenamento em cache é uma consideração importante ao configurar a personalização e o tempo deve ser levado para garantir que a implementação correta seja usada.

>[!TIP]
>
>O efeito do Personalization no desempenho e os tópicos relacionados ao cache são discutidos mais detalhadamente no documento [Otimização de Desempenho.](/help/sites-deploying/configuring-performance.md)

#### Precisão das regras {#accuracy}

* O Personalization realizado rastreando o comportamento do usuário, ou definindo regras com base no perfil do usuário, deve ser preciso e lógico.
* Não há nada mais frustrante para o usuário do que ter conteúdo forçado ou negado a ele por causa da lógica imprecisa de uma regra.
* Portanto, as regras devem ser bem pensadas - com as necessidades do usuário em primeiro plano. Isso pode exigir muito esforço e não deve ser subestimado. Definir as regras de negócios geralmente supera o esforço técnico ao implementar a personalização.

#### Quando usar {#when-to-use}

* Como muitos recursos na Web, a personalização deve ser usada com cuidado. Seu uso realmente beneficiará o usuário? deve ser sempre a primeira consideração - ou se o objetivo desejado pode ser alcançado com menos esforço por outro método. O Personalization pode correr o risco de ser um recurso que os usuários configuram uma vez (para ver como funciona) e apenas uma vez, pois não traz vantagens reais.
* O Personalization só é significativo quando o conteúdo é dinâmico - depende do usuário de alguma forma. Se todos os usuários virem o mesmo conteúdo, a personalização será redundante.

#### Confidencialidade {#confidentiality}

* Muitos usuários estão preocupados com a Proteção e a Segurança dos Dados. Em particular, no que se refere aos dados recuperados ao rastrear o comportamento deles ao navegar na Web.

## Personalization e Access {#personalization-and-access}

O Personalization deve ser considerado separadamente do controle de acesso, mas eles se inter-relacionam.

O próprio Personalization não cria nenhuma forma de controle de acesso. É simplesmente um método para direcionar o que o usuário vê; não restringe o acesso do usuário a outros conteúdos e, como em qualquer conteúdo, é necessário que os controles de acesso corretos já estejam atribuídos.

No entanto, o controle de acesso pode ser usado para criar uma forma de personalização. Se você permitir ou negar acesso ao conteúdo a um usuário, isso inevitavelmente afetará a escolha do conteúdo que ele tem disponível, personalizando assim sua experiência na Web.

## Componentes disponíveis para o Personalization {#components-available-for-personalization}

Vários componentes são fornecidos com AEM para personalização. Alguns permitem que os usuários façam logon e editem seus perfis, outros (como Meus gadgets) permitem que os usuários configurem uma página específica:

| Título no Sidekick | Propósito |
|---|---|
| Campo de senha marcado | Solicita senha e confirmação de senha. |
| Inscrição combinada | Permite que o usuário faça logon em uma conta existente ou cadastre-se em uma nova conta. |
| Campo de endereço do Forms | Um campo complexo que permite a entrada de um endereço internacional. |
| Início do Forms | Inicia uma definição de formulário |
| Forms Captcha | Um campo que consiste em uma palavra alfanumérica que é atualizada automaticamente. O componente captcha protege os sites contra bots. |
| Grupo de caixas de seleção Forms | Vários itens organizados em uma lista e precedidos por caixas de seleção. Os usuários podem marcar várias caixas de seleção. |
| Lista suspensa Forms | Vários itens organizados em uma lista suspensa. A opção Multi Seletable especifica se vários elementos podem ser selecionados na lista. |
| Fim do Forms | Finaliza a definição do formulário. |
| Upload de arquivo do Forms | Um elemento de upload que permite ao usuário carregar um arquivo no servidor. |
| Campo oculto do Forms | Este campo não é exibido ao usuário. Ele pode ser usado para transportar um valor para o cliente e de volta para o servidor. Este campo não deve ter restrições. |
| Botão de imagem do Forms | Um botão de envio adicional para o formulário que é renderizado como uma imagem. |
| Campo de senha do Forms | Igual ao campo de texto, mas somente uma única linha é permitida, e a entrada de texto do usuário não é visível no campo. |
| Grupo de opções Forms | Vários itens organizados em uma lista precedida por um botão de opção. Os usuários devem selecionar apenas um botão de opção. |
| Botão Enviar do Forms | Um botão de envio adicional para o formulário no qual o título é exibido como texto no botão. |
| Campo de texto do Forms | Campo de texto que permite aos usuários inserir informações. |
| Meus gadgets | Permite incluir um de uma seleção de gadgets disponíveis. |
| Foto de avatar do perfil  | Permite a entrada de uma foto de avatar. |
| Nome detalhado de perfil | Entrada de detalhes do nome, incluindo elementos como título, nome do meio e sufixo, se necessário. |
| Nome de exibição no perfil | Nome a ser exibido. |
| E-mail do perfil | Entrada de um endereço de email. |
| Gênero do perfil | Permite a entrada do gênero. |
| Número de telefone principal do perfil | Permite a entrada de um número de telefone. |
| URL principal do perfil | Permite a entrada de um URL. |
| Propriedade de perfil de texto geral | Propriedades do perfil. |
| Fazer logon | Permite enviar um nome de usuário e senha ao fazer login. |
| Fazer logoff | Indica o usuário que está logado no momento e fornece um link para desconectar. |
| Nuvem de tags | Uma nuvem de tags para mostrar uma seleção de tags apresentada graficamente em seu site |
| Teaser | Um conteúdo (geralmente uma imagem) exibido em uma página principal para &quot;provocar&quot; os usuários para acessarem o conteúdo subjacente. |

## Conteúdo do Personalization e da comunidade {#personalization-and-community-content}

Recursos da comunidade, como blogs, fóruns e calendários, resultam na criação de conteúdo da comunidade, comumente conhecido como conteúdo gerado pelo usuário (UGC). Quando o UGC é inserido em um ambiente de publicação que consiste em várias instâncias do AEM (um [farm de publicação](/help/communities/topologies.md)), um problema importante tem sido como sincronizar o UGC em todas as instâncias.

Com a extensão do [AEM Communities 6.1](/help/communities/overview.md), esse problema é resolvido com o uso de um [armazenamento comum para UGC](/help/communities/working-with-srp.md). No que diz respeito à personalização, as Comunidades incluem [Logon social](/help/communities/social-login.md) - a capacidade de fornecer a opção para que os visitantes do site entrem com o Facebook e o Twitter.

Sem a extensão Communities, vários métodos a serem explorados para abordar o problema de consistência da UGC são:

* Sincronizar as várias instâncias de publicação quando necessário
* Envie o UGC da instância de publicação para o ambiente de criação, de onde ele pode ser publicado de uma maneira semelhante à publicação do conteúdo da página

O método usado para obter consistência de UGC em um ambiente de publicação que consiste em várias instâncias de publicação deve ser cuidadosamente projetado e testado para desempenho e consistência.
