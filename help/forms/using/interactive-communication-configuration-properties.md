---
title: Propriedades de configuração do Interative Communications
seo-title: Interactive Communication configuration properties
description: Editar propriedades de configuração padrão para Comunicações interativas
seo-description: Edit default configuration properties for Interactive Communications
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
feature: Interactive Communication
exl-id: 09eeade6-e16d-4159-b26a-803c7201097a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 7%

---

# Propriedades de configuração do Interative Communications{#interactive-communications-configuration-properties}

O Interative Communications inclui propriedades configuradas automaticamente após a instalação do [Complemento do AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) pacote. Os autores do Interative Communication podem editar essas propriedades de configuração padrão usando o **Configuração do Console da Web do Adobe Experience Manager** página.

Abra o **Configuração do Console da Web do Adobe Experience Manager** página usando o seguinte URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

As propriedades de configuração incluem:

* [Configuração de fragmentos de documento](#document-fragments-configuration)
* [Criar configuração de correspondência](#create-correspondence-configuration)
* [Configuração do canal Web de comunicação interativa e formulário adaptável](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuração de Tema de Canal da Web de Comunicação Adaptável e Interativa](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuração de fragmentos de documento {#document-fragments-configuration}

Toque **Configuração dos Fragmentos de documento** no **Configuração do Console da Web do Adobe Experience Manager** para exibir as propriedades de configuração dos fragmentos de documento.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Formatos de exibição de dados</td> 
   <td>Formato de exibição específico de localidade para campos, variáveis e elementos de modelo de dados de formulário disponíveis ao criar uma Comunicação interativa para canais de impressão e da Web.</td> 
   <td> 
    <ul> 
     <li>locale = en_US, de_DE, fr_FR e ja_JP</li> 
     <li>dateFormat = dd-MM-aaaa</li> 
     <li>numberDecimalSeparator = .</li> 
     <li>numberGroupSeparator = ,</li> 
     <li>numberUseGroupSeparator = true</li> 
    </ul> </td> 
   <td><p>—</p> </td> 
  </tr> 
  <tr> 
   <td>Recuo</td> 
   <td>A largura de uma única unidade de recuo aplicada ao texto em fragmentos de documento de lista.</td> 
   <td>12.7mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Largura mínima dos números romanos</td> 
   <td>Largura mínima a ser aplicada ao campo de marcador ou número, ao usar números romanos em fragmentos de documento de lista. </td> 
   <td>12.7mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Largura mínima do número</td> 
   <td>Largura mínima a ser aplicada ao campo de marcador ou número, ao usar listas numeradas além de números romanos em fragmentos de documento de lista.</td> 
   <td>8.0mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Criar configuração de correspondência {#create-correspondence-configuration}

Toque **Criar configuração de correspondência** no **Configuração do Console da Web do Adobe Experience Manager** para exibir as propriedades de configuração da interface do usuário do agente.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Mostrar conteúdo resolvido para edição</td> 
   <td>Marque a caixa de seleção para mostrar o conteúdo resolvido (valores reais em vez de espaços reservados) enquanto edita o módulo de texto na interface do agente.</td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
  <tr> 
   <td>Aplicar marca d'água durante a visualização</td> 
   <td>Marque a caixa de seleção para aplicar marca d'água ao Canal de impressão de comunicação interativa no modo de Visualização.</td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
  <tr> 
   <td>Habilitar incorporação de fonte no PDF</td> 
   <td><p>Marque a caixa de seleção para habilitar a incorporação de fontes nos documentos do PDF. Após selecionar essa opção, você pode incorporar novas fontes após gerar ou visualizar os documentos do PDF usando a interface do agente. Use o Canal de impressão de comunicação interativa para gerar e visualizar documentos de PDF.</p> <p>A incorporação de fontes em um documento PDF é útil se uma fonte estiver disponível em uma máquina usada para gerar o PDF e não estiver disponível na máquina cliente que acessa o PDF.</p> <p>Para obter mais informações sobre incorporação de fontes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor de texto</a>.</p> </td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
 </tbody> 
</table>

## Configuração do canal Web de comunicação interativa e formulário adaptável {#adaptive-form-and-interactive-communication-web-channel-configuration}

Toque **Configuração do canal Web de comunicação interativa e formulário adaptável** no **Configuração do Console da Web do Adobe Experience Manager** para exibir as propriedades de configuração do canal da Web Adaptive Forms e Interative Communications. A tabela a seguir descreve as propriedades relacionadas às Comunicações interativas:

| Propriedade | Descrição | Padrão | Valores aceitáveis |
|---|---|---|---|
| Mostrar espaço reservado | Marque a caixa de seleção para ativar a exibição de espaços reservados para campos incluídos em formulários adaptáveis e Comunicações interativas. | Selecionado | Não aplicável |
| Máximo de entradas de cache | Defina o número máximo de formulários adaptáveis e Comunicações interativas que podem ser recuperadas usando a memória cache. | 100 | Número |
| Tornar o nome do arquivo exclusivo | Marque a caixa de seleção para ter nomes exclusivos para arquivos incluídos como anexos no Adaptive Forms e nas Comunicações interativas. | Não selecionado | Não aplicável |

## Configuração de Tema de Canal da Web de Comunicação Adaptável e Interativa {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Toque **Configuração de Tema de Canal da Web de Comunicação Adaptável e Interativa** no **Configuração do Console da Web do Adobe Experience Manager** para visualizar as propriedades de configuração dos temas do canal da Web Adaptive Forms e Interative Communications.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Nome da lista de fontes</td> 
   <td>Lista de fontes disponíveis para uso ao criar o Adaptive Forms e o Interative Communications.</td> 
   <td><p>Geórgia</p> <p>Livro Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Linotipo de Palatino</p> </td> 
   <td>Todas as fontes válidas do servidor Adobe</td> 
  </tr> 
 </tbody> 
</table>
