---
title: Propriedades de configuração do Interative Communications
seo-title: Propriedades de configuração do Interative Communication
description: Editar propriedades de configuração padrão para o Interative Communications
seo-description: Editar propriedades de configuração padrão para o Interative Communications
uuid: 4030078f-64a3-40bb-9892-49e22a8da561
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: interactive-communications
discoiquuid: acb61d37-cd22-422e-bbf3-a2979b13ad41
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3
workflow-type: tm+mt
source-wordcount: '625'
ht-degree: 7%

---


# Propriedades de configuração do Interative Communications{#interactive-communications-configuration-properties}

O Interative Communications inclui propriedades que são configuradas automaticamente após a instalação do pacote de complementos [AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md). Os autores do Interative Communication podem editar essas propriedades de configuração padrão usando a página **Configuração do Adobe Experience Manager Web Console**.

Abra a página **Configuração do Adobe Experience Manager Web Console** usando o seguinte URL:

`https:/[server]:[port]/<contextPath>/system/console/configMgr`

As propriedades de configuração incluem:

* [Configuração de fragmentos de documento](#document-fragments-configuration)
* [Criar configuração de correspondência](#create-correspondence-configuration)
* [Configuração de formulário adaptável e de Canal da Web de comunicação interativa](#adaptive-form-and-interactive-communication-web-channel-configuration)
* [Configuração do tema do Canal da Web de formulário adaptável e comunicação interativa](#adaptive-form-and-interactive-communication-web-channel-theme-configuration)

## Configuração de fragmentos de documento {#document-fragments-configuration}

Toque em **Configuração de fragmentos de Documento** na página **Configuração do Adobe Experience Manager Web Console** para visualização as propriedades de configuração dos fragmentos de documento.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Formatos de Exibição de Dados</td> 
   <td>O formato de exibição específico da localidade para campos, variáveis e elementos de modelo de dados de formulário está disponível ao criar uma Comunicação Interativa para canais da Web e Impressos.</td> 
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
   <td>A largura de uma unidade de recuo aplicada ao texto em fragmentos de documento de lista.</td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Largura mínima dos números romanos</td> 
   <td>Largura mínima a ser aplicada ao campo de marcador ou número, ao usar números romanos em fragmentos de documento de lista. </td> 
   <td>12,7 mm</td> 
   <td>Número</td> 
  </tr> 
  <tr> 
   <td>Largura mínima do número</td> 
   <td>Largura mínima a ser aplicada ao campo de marcador ou número, ao usar listas numeradas além de números romanos em fragmentos de documento de lista.</td> 
   <td>8,0 mm</td> 
   <td>Número</td> 
  </tr> 
 </tbody> 
</table>

## Criar Configuração de Correspondência {#create-correspondence-configuration}

Toque em **Criar configuração de correspondência** na página **Configuração do Adobe Experience Manager Web Console** para visualização das propriedades de configuração da interface do agente.

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
   <td>Aplicar marca d'água durante a pré-visualização</td> 
   <td>Marque a caixa de seleção para aplicar a marca d'água ao Imprimir canal de comunicação interativa no modo de Pré-visualização.</td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
  <tr> 
   <td>Ativar incorporação de fonte no PDF</td> 
   <td><p>Marque a caixa de seleção para ativar a incorporação de fontes nos documentos PDF. Após selecionar essa opção, é possível incorporar novas fontes depois de gerar ou visualizar os documentos PDF usando a interface do usuário do agente. Use o canal Imprimir de comunicação interativa para gerar e pré-visualização de documentos PDF.</p> <p>A incorporação de fontes em um documento PDF é útil se uma fonte estiver disponível em um computador usado para gerar o PDF e não estiver disponível no computador cliente que acessa o PDF.</p> <p>Para obter mais informações sobre como incorporar fontes, consulte <a href="../../forms/using/customize-text-editor.md" target="_blank">Personalizar editor de texto</a>.</p> </td> 
   <td>Não selecionado</td> 
   <td>Não aplicável</td> 
  </tr> 
 </tbody> 
</table>

## Configuração de Canal da Web de Formulário Adaptável e Comunicação Interativa {#adaptive-form-and-interactive-communication-web-channel-configuration}

Toque em **Configuração do Canal Web de Formulário Adaptável e Comunicação Interativa** na página **Configuração do Console Web Adobe Experience Manager** para visualização das propriedades de configuração do canal Web Adaptive Forms e Interative Communications. A tabela a seguir descreve as propriedades relacionadas ao Interative Communications:

| Propriedade | Descrição | Padrão | Valores aceitáveis |
|---|---|---|---|
| Mostrar espaço reservado | Marque a caixa de seleção para ativar a exibição de espaços reservados para campos incluídos em formulários adaptáveis e Comunicações interativas. | Selecionado | Não aplicável |
| Máximo de entradas de cache | Defina o número máximo de formulários adaptáveis e de Comunicações interativas que podem ser recuperados usando a memória cache. | 100 | Número |
| Tornar o nome do arquivo único | Marque a caixa de seleção para ter nomes exclusivos para arquivos incluídos como anexos no Adaptive Forms e no Interative Communications. | Não selecionado | Não aplicável |

## Configuração do Tema de Formulário Adaptável e Comunicação Interativa de Canais da Web {#adaptive-form-and-interactive-communication-web-channel-theme-configuration}

Toque em **Configuração do Tema de Canal da Web de Formulário Adaptável e Comunicação Interativa** na página **Configuração do Console da Web da Adobe Experience Manager** para visualização das propriedades de configuração dos temas de canal da Web Adaptive Forms e Interative Communications.

<table>
 <tbody> 
  <tr> 
   <td>Propriedade</td> 
   <td>Descrição</td> 
   <td>Padrão</td> 
   <td>Valores aceitáveis</td> 
  </tr> 
  <tr> 
   <td>Nome da Lista da fonte</td> 
   <td>Lista de fontes disponíveis para uso ao criar o Forms adaptativo e o Interative Communications.</td> 
   <td><p>Geórgia</p> <p>Livro Antiqua</p> <p>Times New Roman</p> <p>Arial</p> <p>Arial Black</p> <p>Impacto</p> <p>Linotipo de Palatino</p> </td> 
   <td>Todas as fontes válidas do servidor de Adobe</td> 
  </tr> 
 </tbody> 
</table>

