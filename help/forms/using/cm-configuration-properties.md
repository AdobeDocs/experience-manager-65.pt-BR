---
title: Propriedades de configuração do gerenciamento de correspondência
description: Este tópico explica como modificar o Asset Composer com configurações específicas da solução. Este tópico detalha as propriedades que você pode editar, com sua descrição, valores padrão e valores aceitáveis.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: c9c007d0-c545-4738-b11b-4c50986342ee
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 3%

---

# Propriedades de configuração do gerenciamento de correspondência {#correspondence-management-configuration-properties}

Para configurar essas propriedades, abra o seguinte URL em um navegador: `https://<server>:<port>/<contextPath>/system/console/configMgr` e selecione **Configurações do gerenciamento de correspondência**.

O Gerenciamento de correspondências tem as seguintes propriedades de configuração:

<table>
 <tbody>
  <tr>
   <th><p><strong>Propriedade</strong></p> </th>
   <th><p><strong>Descrição</strong></p> </th>
   <th><p><strong>Padrão</strong></p> </th>
   <th><p><strong>Valores aceitáveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Recuo</p> </td>
   <td>Recuo nos módulos<p> </p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualquer número</p> </td>
  </tr>
  <tr>
   <td>Largura mínima do número</td>
   <td>Largura mínima a ser aplicada ao campo de marcador/número ao usar Listas numeradas além dos números romanos</td>
   <td>8,0 mm</td>
   <td>Qualquer número</td>
  </tr>
  <tr>
   <td><p>Largura mínima de números romanos</p> </td>
   <td><p>Largura mínima a ser aplicada ao campo de marcador/número ao usar números romanos</p> </td>
   <td><p>12,7 mm</p> </td>
   <td><p>Qualquer número</p> </td>
  </tr>
  <tr>
   <td>Tipo de representação</td>
   <td>O tipo de representação que o aplicativo Criar correspondência usa para renderizar a pré-visualização de correspondência. </td>
   <td>Representação do HTML</td>
   <td>Representação de HTML / Representação de PDF</td>
  </tr>
  <tr>
   <td><p>Ativar CCR PDF highlight</p> </td>
   <td><p>Habilita o realce de PDF no aplicativo Criar correspondência</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de realce do público alvo</p> </td>
   <td><p>Tipo de destaque do Target no aplicativo Criar correspondência</p> </td>
   <td><p>borda</p> </td>
   <td><p>borda / preenchimento / nenhum</p> </td>
  </tr>
  <tr>
   <td><p>Cor de realce do público alvo</p> </td>
   <td><p>Cor de destaque do Target no aplicativo Criar correspondência</p> </td>
   <td><p>90;155;245</p> </td>
   <td><p>Qualquer cor de RGB no formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de realce de conteúdo</p> </td>
   <td><p>Tipo de destaque de conteúdo no aplicativo Criar correspondência</p> </td>
   <td><p>Preenchimento</p> </td>
   <td><p>borda / preenchimento / nenhum</p> </td>
  </tr>
  <tr>
   <td><p>Cor de realce do conteúdo</p> </td>
   <td><p>Cor de destaque do conteúdo no aplicativo Criar correspondência</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualquer cor de RGB no formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de realce de campo</p> </td>
   <td><p>Tipo de destaque de campo no aplicativo Criar correspondência</p> </td>
   <td><p>preenchimento</p> </td>
   <td><p>borda / preenchimento / nenhum</p> </td>
  </tr>
  <tr>
   <td><p>Cor de realce do campo</p> </td>
   <td><p>Cor de destaque do campo no aplicativo Criar correspondência</p> </td>
   <td><p>210;225;245</p> </td>
   <td><p>Qualquer cor de RGB no formato R;G;B</p> </td>
  </tr>
  <tr>
   <td><p>Tempo limite do aplicativo</p> </td>
   <td><p>Tempo limite do aplicativo em segundos</p> </td>
   <td><p>1200</p> </td>
   <td><p>Qualquer número</p> </td>
  </tr>
  <tr>
   <td><p>nome do parâmetro do documento PDF</p> </td>
   <td><p>Nome do parâmetro para o documento PDF em pós-processamento</p> </td>
   <td><p>inPDFDoc</p> </td>
   <td><p>Qualquer nome de variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro de dados XML</p> </td>
   <td><p>Nome do parâmetro para o documento XML (dados) em pós-processamento</p> </td>
   <td><p>inXMLDoc</p> </td>
   <td><p>Qualquer nome de variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro do documento XDP</p> </td>
   <td><p>Nome do parâmetro para o documento XDP enviado para o pós-processo</p> </td>
   <td><p>inXDPDoc</p> </td>
   <td><p>Qualquer nome de variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro de URL de redirecionamento</p> </td>
   <td><p>Nome do parâmetro para o URL de redirecionamento enviado do pós-processo. Esse valor pode ser qualquer nome de variável de string</p> </td>
   <td><p>redirectURL</p> </td>
   <td><p>Qualquer nome de variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Tipo de envio de PDF</p> </td>
   <td><p>Tipo de Envio de PDF (tipo de PDF gerado ao enviar a partir do aplicativo Criar Correspondência)</p> </td>
   <td><p>nonInterative</p> </td>
   <td><p>interativo / não interativo</p> </td>
  </tr>
  <tr>
   <td><p>Otimizar instância do dicionário de dados</p> </td>
   <td><p>Permite a transferência otimizada da instância do dicionário de dados por servidor e cliente</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Inconsistências de correção automática </p> </td>
   <td><p>Quando habilitado, ele manipula automaticamente as possíveis inconsistências nas Atribuições de cartas</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Usar formatos de dados configurados</p> </td>
   <td><p>Controla se os dados configurados devem ser usados no formato de edição e no formato de exibição de dados</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Formatos de Exibição de Dados</p> </td>
   <td><p>Especifica o formato de exibição específico da localidade para dados</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=truelocale=de_DE; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator=.; numberUseGroupSeparator=truelocale=fr_FR; dateFormat=dd-MM-yyyy; numberDecimalSeparator=,; numberGroupSeparator= ; numberUseGroupSeparator=truelocale=ja_JP; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td><p>—</p> </td>
  </tr>
  <tr>
   <td><p>Formato de Edição de Dados</p> </td>
   <td><p>Editar formato dos dados. Isso é usado ao gravar dados como string ou analisar dados de string</p> </td>
   <td><p>locale=en_US; dateFormat=dd-MM-yyyy; numberDecimalSeparator=.; numberGroupSeparator=,; numberUseGroupSeparator=true</p> </td>
   <td>—<p> </p> </td>
  </tr>
  <tr>
   <td><p>Gerenciar instâncias de carta ao publicar</p> </td>
   <td><p>Habilitar/desabilitar a funcionalidade Gerenciar carta (aplicável somente para o Servidor de publicação)</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Ativar auditoria</p> </td>
   <td><p>Ativar/desativar funcionalidade de auditoria. Quando for falso, os logs de auditoria para todas as ações serão desabilitados</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Ativar auditoria de leitura</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para leituras de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Criar Auditoria</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para criar ativo</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Auditoria de Atualização</p> </td>
   <td><p>Ativar/desativar funcionalidade de auditoria para atualização de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Ativar Reverter auditoria</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para reversão de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Publicar Auditoria</p> </td>
   <td><p>Ativar/desativar a funcionalidade de auditoria para publicação de ativos</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Salvar como Auditoria de Rascunho</p> </td>
   <td><p>Habilitar/desabilitar a funcionalidade de auditoria para salvar rascunhos de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Ativar Enviar auditoria</p> </td>
   <td><p>Habilitar/desabilitar a funcionalidade de auditoria para envio de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Ativar auditoria de e-mail</p> </td>
   <td><p>Habilitar/desabilitar a funcionalidade de auditoria para cartas enviadas por email</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar Auditoria de Impressão</p> </td>
   <td><p>Habilitar/desabilitar a funcionalidade de auditoria para impressão de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Habilitar auditoria de entrega personalizada</p> </td>
   <td><p>Habilitar/desabilitar a funcionalidade de auditoria para entrega personalizada de cartas</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Nome do parâmetro dos documentos de anexo</p> </td>
   <td><p>Nome do parâmetro para documentos de anexo enviados para o pós-processo</p> </td>
   <td><p>inAttachmentDocs</p> </td>
   <td><p>Qualquer nome de variável de string</p> </td>
  </tr>
  <tr>
   <td><p>Raiz do usuário do CM</p> </td>
   <td><p>URL da pasta que contém todos os ativos de usuário do Gerenciamento de correspondências</p> </td>
   <td><p>—</p> </td>
   <td><p>Local de pasta válido</p> </td>
  </tr>
  <tr>
   <td><p>Tamanho do Cache de Carta</p> </td>
   <td><p>Especifique o Número máximo de letras a serem mantidas no cache.</p> <p>Alterar esse valor resultará na limpeza de <code>in-memory</code> cache.</p> </td>
   <td><p>100</p> </td>
   <td><p>Qualquer valor numérico</p> </td>
  </tr>
  <tr>
   <td><p>Ativar cache de cartas</p> </td>
   <td><p>Ativar/desativar o cache de letras.</p> <p>Alterar esse valor resultará na limpeza de <code>in-memory </code> cache.</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Ordem dos elementos de dados</p> </td>
   <td><p>Mantém a ordem dos elementos de dados na interface de criação de correspondência de acordo com a sequência na Carta</p> </td>
   <td><p>verdadeiro</p> </td>
   <td><p>verdadeiro / falso</p> </td>
  </tr>
  <tr>
   <td><p>Recarga de suporte</p> </td>
   <td><p>Ativar/desativar o suporte de recarregamento em cartas renderizadas no lado do servidor.</p> <p>Desativar essa opção melhorará o desempenho de renderização da correspondência.</p> </td>
   <td><p>falso</p> </td>
   <td><p>verdadeiro / falso</p> <p> </p> </td>
  </tr>
  <tr>
   <td>Pasta temporária</td>
   <td>Local da pasta temporária.</td>
   <td>acm.tpmFolder</td>
   <td> </td>
  </tr>
  <tr>
   <td>Salvamento remoto</td>
   <td>Salva as Instâncias de Letra no autor de processamento especificado.</td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Opções de compatibilidade</td>
   <td>Opções de compatibilidade do formato configname:configvalue separadas por vírgula.</td>
   <td>acm.compatibilityOptions</td>
   <td> </td>
  </tr>
  <tr>
   <td><p>Diretório de depuração </p> <p> </p> </td>
   <td>Local da pasta do sistema de arquivos para depuração. Se o diretório não <code>exists</code>, nenhum despejo de depuração será gerado.</td>
   <td>acm.debugDirectory</td>
   <td> </td>
  </tr>
 </tbody>
</table>
