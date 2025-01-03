---
title: Gerenciar certificados
description: Saiba como importar e exportar um certificado e editar suas configurações de confiança.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1fe0e7b4-6109-4f7a-8858-8237a1c5c93b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# Gerenciar certificados {#managing-certificates}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Usando o Gerenciamento de Armazenamento Confiável, você pode importar, editar e excluir certificados confiáveis no servidor para validação de assinaturas digitais e autenticação de certificado. É possível importar e exportar qualquer número de certificados. Após importar um certificado, você poderá editar as configurações de confiança e o tipo de armazenamento de confiança. Considere as seguintes opções ao combinar tipos de armazenamento de confiança:

* **Confiança para Autenticação de Certificado com CA:** Para validação de CRL, selecione também Confiança para Identidade.
* **Confiança para Autenticação de Certificado com ICA:** Selecione somente Confiança para Identidade. Um ICA não deve ser confiável para a Autenticação de Certificado. Se você confiar no ICA para autenticação de certificado, o ICA se tornará uma CA para construção de caminho. Se o ICA for confiável para a Autenticação de certificados e a Identidade, o certificado do fornecedor da CA será ignorado, pois o ICA se torna a CA.
* **Confiança para o Servidor OCSP com HTTPs:** Se o servidor do entrevistado OSCP residir em um local HTTPs, você também deverá selecionar Confiança para Conexões SSL. Se o entrevistado do OSCP exigir validação da CRL, certifique-se também de selecionar Confiança para identidade.
* **Raiz do Adobe:** Não selecione Conexões SSL ou Tipos de Repositório de Confiança de Servidor OCSP. A Raiz do Adobe não é confiável para Conexões SSL e Servidor OCSP. O Adobe não emite certificados OCSP e SSL. A Raiz Adobe é implicitamente confiável com um alias name=&quot;ADOBEROOT&quot;.

Somente os certificados X509v3 são suportados. Esse tipo de certificado pode ser fornecido em um arquivo binário codificado em DER (arquivo .cer) ou em um arquivo de texto que contenha uma versão codificada em Base64 do mesmo certificado codificado em DER (incluindo certificados X509 no formato Privacy Enhanced Mail (PEM)).

Os certificados necessários para concluir uma verificação de assinatura devem estar no mesmo armazenamento (HSM ou banco de dados).

Você também pode importar e excluir certificados usando a API do Gerenciador de Confiança. Para obter detalhes, consulte &quot;Importando certificados usando a API do Gerenciador de Confiança&quot; e &quot;Excluindo certificados usando a API do Gerenciador de Confiança&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importar um certificado {#import-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de Repositório Confiável > Certificados]**.
1. Clique em Importar e, em Tipo de armazenamento de confiança, selecione uma destas opções:

   * **Confiança para Conexões SSL:** especifica que os formulários AEM podem usar certificados para se conectar a sistemas externos via SSL.
   * **Confiança para certificar assinatura:** especifica que os certificados são confiáveis em operações de assinatura de documentos para certificar assinaturas digitais do autor.
   * **Confiança para assinatura:** especifica que os certificados são confiáveis em operações de assinatura de documentos para assinaturas digitais que não sejam de autoria.
   * **Confiança para Autenticação de Certificado:** especifica que os formulários AEM usam certificados para autenticar usuários usando autenticação de certificado ou cartão inteligente.
   * **Confiança para o Servidor OCSP:** especifica que os formulários AEM podem usar certificados para se conectar a respondentes OCSP externos
   * **Confiança da Identidade:** especifica que os certificados podem ser usados para confiar em informações diferentes dos tipos especificados acima.

   >[!NOTE]
   >
   >O armazenamento de confiança confia implicitamente em um Certificado Raiz de Adobe para autenticação de certificado, assinatura, assinatura de certificado e identidade.

1. Na caixa Alias, digite o identificador do certificado.
1. Clique em **[!UICONTROL Procurar]** para localizar o certificado e em **[!UICONTROL OK]**.

## Exportar um certificado {#export-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de Repositório Confiável > Certificados]**.
1. Clique no nome do alias do certificado a ser exportado. A página **[!UICONTROL Detalhes do Certificado]** é exibida.
1. Clique em **[!UICONTROL Exportar]**, siga as instruções para exportar o certificado e clique em **[!UICONTROL OK]**.

## Edite as configurações de confiança e o tipo de armazenamento de confiança de um certificado {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de Repositório Confiável > Certificados]**.
1. Clique no nome do alias do certificado para editar.
1. Clique em **[!UICONTROL Atualizar Certificado]**.
1. Para alterar o Nome do alias do certificado, digite um novo nome na caixa Alias.
1. Para atualizar o tipo de armazenamento de confiança para o certificado, selecione o tipo de armazenamento de confiança apropriado.
1. Para atualizar as restrições de política, na caixa Diretivas de Certificado, digite as informações da política e clique em **[!UICONTROL OK]**.

## Excluir um certificado {#delete-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de Repositório Confiável > Certificados]**.
1. Marque as caixas de seleção dos certificados a serem excluídos, clique em **[!UICONTROL Excluir]** e em **[!UICONTROL OK]**.
