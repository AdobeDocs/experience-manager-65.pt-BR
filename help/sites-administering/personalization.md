---
title: Personalização
seo-title: Personalização
description: Saiba mais sobre a personalização no AEM.
seo-description: Saiba mais sobre a personalização no AEM.
uuid: 5790a3e0-f0ec-4785-b915-330a10dea30c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 03ebc494-8baa-4741-b8de-dac5ace743c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1684'
ht-degree: 16%

---


# Personalização{#personalization}

## O que é personalização? {#what-is-personalization}

Existe um volume cada vez maior de conteúdo disponível atualmente, seja na Internet, na extranet ou em sites da intranet.

A personalização centra-se em fornecer ao usuário um ambiente feito à medida que exibe o conteúdo dinâmico que é selecionado de acordo com suas necessidades específicas; seja com base em perfis predefinidos, na seleção do usuário ou no comportamento interativo do usuário.

Há três elementos principais envolvidos na personalização:

**Usuários**

* têm perfis individuais e de grupo. Esses perfis contêm características (como descrição da tarefa, localização, interesses) que podem ser usadas para personalizar o conteúdo que podem ver.
* tome medidas. Eles podem então ser analisados e comparados com regras de comportamento para adaptar o conteúdo que veem.

**Conteúdo**

* é o que o usuário deseja ver. De preferência, o conteúdo dos interesses e a sua utilização para o cumprimento das suas tarefas.
* podem ser categorizados e, portanto, disponibilizados aos usuários de acordo com regras predefinidas.devem ser dinâmicos; por outras palavras, o conteúdo
* deve, de alguma forma, depender do usuário - se cada usuário visualizasse o mesmo conteúdo, a personalização seria redundante.

**Regras**

* defina como a personalização realmente acontece - qual conteúdo o usuário pode ver e quando.

A personalização pode ser:

**Explícita**

* Personalização: em que o usuário faz seleções a partir de uma escolha de fontes de conteúdo.

**Implicado**

* Baseado em regras: os gerentes de negócios definem regras específicas para ações com base em perfis e/ou comportamentos específicos.
* Filtragem simples: as seleções são feitas com base em perfis predefinidos no nível do usuário e/ou grupo.
* Filtragem colaborativa/de recomendação: o comportamento do usuário é registrado de acordo com regras predefinidas. Estas regras baseiam-se no comportamento observado com indivíduos com ideias semelhantes. As informações coletadas são usadas para adaptar as informações exibidas ao usuário, principalmente sob a forma de recomendações.

## Como e quando a Personalização pode ser usada? {#how-and-when-can-personalization-be-used}

A personalização pode ser usada em muitos casos, por exemplo:

**Páginas da intranet**

* O conteúdo pode ser oferecido com base na localização, no departamento e/ou na função de um usuário - já definido em uma rede interna.
* Dependendo da escolha disponível, o usuário pode fazer outras seleções.

**Grupos de usuários específicos, limitados e públicos alvos (extranets)**

* Os utilizadores requerem um início de sessão para autorização; isso estará ligado a um perfil que forneça as informações necessárias para a personalização; possivelmente detalhes como localização, relacionamento com o produto, histórico de utilização, responsabilidades orçamentárias etc.
* Essas instâncias podem variar em sites como:
* Empresas que fornecem sítios Web a uma seção altamente especializada do seu mercado, por exemplo, uma empresa farmacêutica que disponibiliza um sítio web especializado para médicos.
* Empresas que fornecem sítios Web que permitem ao seu cliente visualização de informações sobre a conta corrente e faturação; por exemplo, provedores de telefone.

**Site de vendas e distribuição**

* Os sites de vendas e distribuição, como o Amazon, podem combinar um perfil de usuário, o histórico de vendas do usuário e seu histórico de navegação para fazer sugestões sobre o que poderá interessar ao usuário a seguir.

**Pesquisar sites**

* Muitos dos principais sites de mecanismos de busca têm ferramentas analíticas muito poderosas que registram o comportamento do usuário, os termos de pesquisa que usam e os sites que realmente visitam. Isso é usado para personalizar o conteúdo fornecido - especialmente no que diz respeito à exibição de anúncios.

### Força de personalização e pontos a serem considerados {#strengths-of-personalization-and-points-to-consider}

A seguir estão as razões pelas quais a personalização deve ser usada:

* Um usuário pode experimentar um site confortável e focado.
* A personalização pode ser usada para propagar automaticamente o acesso à versão mais recente do conteúdo.
* Os recursos de colaboração social estão disponíveis para que os usuários se comuniquem entre si, pois podem ser identificados por seus perfis.
* Um usuário pode receber o conteúdo necessário para atender a uma tarefa específica. Dentro de uma empresa, isso pode fornecer uma ferramenta inestimável para a disseminação de informações.
* Um usuário pode receber o conteúdo que precisa/deseja, reduzindo o tempo necessário para executar operações de pesquisa.
* O provedor de conteúdo pode direcionar o conteúdo para ser visto por categorias específicas de usuários.
* As regras podem ser definidas para fornecer conteúdo com base em combinações de características e comportamento do usuário. Isso fornece um mecanismo sofisticado para personalizar sua experiência na Web.

Ao usar a personalização, considere o seguinte:

**Show**

* Naturalmente, a análise e a avaliação adicionais têm impacto no desempenho. No entanto, os métodos utilizados são altamente sofisticados e podem ser otimizados para minimizar o impacto.

**Autorização**

* A personalização requer um mecanismo de logon, pois o site deve ser capaz de identificar o usuário.

**Cache**

* O armazenamento em cache é um aspecto que o usuário verá em termos de desempenho e precisão - a rapidez com que o site fornece conteúdo personalizado e sempre é atual.
* O armazenamento em cache é uma consideração essencial ao configurar a personalização e o tempo deve ser considerado para garantir que a implementação correta seja usada. Esta questão será discutida mais pormenorizadamente mais tarde.

**Precisão das regras**

* A personalização realizada por meio do rastreamento do comportamento do usuário, ou da definição de regras baseadas no perfil do usuário, deve ser precisa e lógica.
* Não há nada mais frustrante para o usuário do que ter conteúdo forçado, ou negado a ele, por causa da lógica imprecisa de uma regra.
* Portanto, as regras devem ser bem pensadas - com os requisitos do usuário em primeiro plano. Isso pode levar muito esforço, e não deve ser subestimado. a definição das regras de negócios geralmente supera o esforço técnico ao implementar a personalização.

**Quando usar**

* Como muitos recursos na Web, a personalização deve ser usada com cuidado. A sua utilização beneficiará realmente o utilizador? deve ser sempre a primeira consideração - ou se o objetivo desejado pode ser alcançado com menos esforço por outro método. A personalização pode correr o risco de ser um recurso que os usuários configuram uma vez (para ver como funciona) e apenas uma vez - pois não traz vantagens reais.
* A personalização só é significativa quando o conteúdo é dinâmico - dependendo do usuário de alguma forma. Se todos os usuários visualizarem o mesmo conteúdo, a personalização será redundante.

**Confidencialidade**

* Muitos usuários estão preocupados com a proteção e segurança de dados. Em especial no que diz respeito aos dados recuperados ao rastrear o seu comportamento ao navegar na Web.

## Personalização e acesso {#personalization-and-access}

A personalização deve ser considerada separadamente do controle de acesso, mas elas se interrelacionam.

A personalização em si não cria nenhuma forma de controle de acesso. Trata-se simplesmente de um método de orientação do que o utilizador vê; não impede que o usuário acesse outro conteúdo e, como em qualquer conteúdo, precisa ter os controles de acesso corretos já atribuídos.

Entretanto, o controle de acesso pode ser usado para criar uma forma de personalização. Se você permitir ou negar o acesso de um usuário ao conteúdo, isso afetará inevitavelmente a escolha do conteúdo que ele tem disponível - personalizando sua experiência na Web.

## Componentes disponíveis para Personalização {#components-available-for-personalization}

Vários componentes são fornecidos com AEM para personalização. Alguns permitem que os usuários façam logon e editem seus perfis, outros (como Meus gadgets) permitem que os usuários configurem uma página específica:

| Título no Sidekick | Propósito |
|---|---|
| Campo de senha marcado | Solicita a senha e a confirmação da senha. |
| Logon combinado | Permite que o usuário faça logon em uma conta existente ou se inscreva para uma nova conta. |
| Campo de endereço Forms | Um campo complexo que permite a entrada de um endereço internacional. |
| Forms Begin | Start uma definição de formulário |
| Forms Captcha | Um campo que consiste em uma palavra alfanumérica que é atualizada automaticamente. O componente de captcha protege websites contra bots. |
| Grupo de caixa de seleção do Forms | Vários itens organizados em uma lista e precedidos por caixas de seleção. Os usuários podem selecionar várias caixas de seleção. |
| Lista suspensa Forms | Vários itens organizados em uma lista suspensa. A opção Multisselecionáveis especifica se vários elementos podem ser selecionados na lista. |
| Forms End | Encerra a definição do formulário. |
| Upload de arquivo Forms | Um elemento de carregamento que permite ao usuário carregar um arquivo no servidor. |
| Campo oculto do Forms | Este campo não é exibido para o usuário. Ele pode ser usado para transportar um valor para o cliente e de volta para o servidor. Esse campo não deve ter nenhuma restrição. |
| Botão Imagem do Forms | Um botão de envio adicional para o formulário que é renderizado como uma imagem. |
| Campo de senha do Forms | Igual ao campo de texto, mas somente uma única linha é permitida e a entrada de texto do usuário não fica visível no campo. |
| Grupo de opções Forms | Vários itens organizados em uma lista precedida por um botão de rádio. Os usuários devem selecionar somente um botão de rádio. |
| Botão Enviar da Forms | Um botão de envio adicional para o formulário, onde o título é exibido como texto no botão. |
| Campo de texto do Forms | Campo de texto que permite que os usuários insiram informações. |
| Meus gadgets | Permite incluir uma seleção de gadgets disponíveis. |
| Foto de avatar do perfil | Permite a entrada de uma foto de avatar. |
| Nome detalhado de perfil | Entrada de detalhes do nome, incluindo elementos como título, nome do meio e sufixo, se necessário. |
| Nome de exibição no perfil | O nome a ser exibido. |
| E-mail do perfil | Entrada de um endereço de e-mail. |
| Gênero do perfil | Permite a entrada de gênero. |
| Número de telefone principal do perfil | Permite a entrada de um número de telefone. |
| URL principal do perfil | Permite a entrada de um URL. |
| propriedade Texto geral do perfil | Propriedades do perfil. |
| Fazer logon | Permite enviar um nome de usuário e senha ao fazer logon. |
| Sair | Indica o usuário conectado no momento e fornece um link para fazer logoff. |
| Nuvem de tags | Uma nuvem de tags para mostrar uma seleção de tags apresentada graficamente em seu site |
| Teaser | Um conteúdo (geralmente uma imagem) exibido em uma página principal para &quot;incentivar&quot; os usuários a acessarem o conteúdo subjacente. |

## Personalização e conteúdo da comunidade {#personalization-and-community-content}

Recursos da comunidade, como blogs, fóruns e calendários, resultam na criação de conteúdo da comunidade, comumente conhecido como conteúdo gerado pelo usuário (UGC). Quando o UGC é inserido em um ambiente de publicação que consiste em várias instâncias de AEM (um [farm de publicação](/help/communities/topologies.md)), um problema importante foi como sincronizar o UGC em todas as instâncias.

Com a extensão [AEM Communities 6.1](/help/communities/overview.md), este problema é resolvido usando um repositório comum [para UGC](/help/communities/working-with-srp.md). No que diz respeito à personalização, as Comunidades incluem [Logon social](/help/communities/social-login.md) - a capacidade de fornecer a opção para que os visitantes do site façam logon com o Facebook e o Twitter.

Sem a extensão das Comunidades, vários métodos para explorar a questão da consistência do UGC são:

* sincronizar as várias instâncias de publicação quando necessário
* envie o UGC da instância de publicação para o ambiente do autor, de onde ele pode ser publicado de maneira semelhante ao conteúdo da página de publicação

O método usado para alcançar a consistência UGC em um ambiente de publicação que consiste em várias instâncias de publicação deve ser cuidadosamente projetado e testado para garantir o desempenho e a consistência.
