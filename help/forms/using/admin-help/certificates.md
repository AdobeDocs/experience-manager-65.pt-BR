---
title: Gerenciamento de certificados
seo-title: Gerenciamento de certificados
description: Saiba como importar e exportar um certificado e editar suas configurações de confiança.
seo-description: Saiba como importar e exportar um certificado e editar suas configurações de confiança.
uuid: 46b1dbe5-517c-4294-bb52-cc6700a768e8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9fd531c0-5206-4be0-a450-13e0dc806068
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---


# Gerenciamento de certificados {#managing-certificates}

Usando o Gerenciamento de armazenamento de confiança, você pode importar, editar e excluir certificados confiáveis no servidor para a validação de assinaturas digitais e autenticação de certificado. É possível importar e exportar qualquer número de certificados. Depois que um certificado é importado, você pode editar as configurações de confiança e o tipo de armazenamento de confiança. Considere as seguintes opções ao combinar tipos de armazenamento confiável:

* **Confiança para autenticação de certificado com CA:** Para validação de CRL, também selecione Confiança para identidade.
* **Confiança para Autenticação de Certificado com ICA:** Selecione somente Confiar para Identidade. Uma ICA não deve ser confiável para autenticação de certificado. Se você confia no ICA para autenticação de certificado, o ICA se torna uma CA para construção de caminho. Se a ICA for confiável para Autenticação de certificado e Identidade, o certificado do fornecedor da CA será ignorado porque a ICA se torna a CA.
* **Confiança para o OCSP Server com HTTPs:** Se o servidor do OSCP entrevistado residir em um local HTTPs, você também deverá selecionar Confiança para conexões SSL. Se o entrevistado OSCP exigir validação de CRL, certifique-se de selecionar Confiança para a identidade.
* **Raiz do Adobe:** Não selecione Conexões SSL ou Tipos de Armazenamento de Confiança do Servidor OCSP. Adobe Root não é confiável para Conexões SSL e Servidor OCSP. O Adobe não emite certificados OCSP e SSL. Adobe Root é implicitamente confiável com um alias name=&quot;ADOBEROOT&quot;.

Somente certificados X509v3 são suportados. Este tipo de certificado pode ser fornecido em um arquivo binário codificado por DER (arquivo .cer) ou em um arquivo de texto que contenha uma versão codificada em Base64 do mesmo certificado codificado por DER (incluindo certificados X509 no formato PEM (Privacy Enhanced Mail)).

Os certificados necessários para concluir uma verificação de assinatura devem estar na mesma loja (HSM ou banco de dados).

Também é possível importar e excluir certificados usando a API do Trust Manager. Para obter detalhes, consulte &quot;Importar certificados usando a API do Trust Manager&quot; e &quot;Excluir certificados usando a API do Trust Manager&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).

## Importar um certificado {#import-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Clique em Importar e, em Tipo de armazenamento confiável, selecione uma destas opções:

   * **Confiança para conexões SSL:** Especifica que os formulários AEM podem usar certificados para se conectar a sistemas externos por SSL.
   * **Confiança para assinatura de certificação:** especifica que os certificados são confiáveis em operações de assinatura de documento para certificar assinaturas digitais de autor.
   * **Confiança para assinatura:** especifica que os certificados são confiáveis em operações de assinatura de documentos para assinaturas digitais de não autor.
   * **Confiança para autenticação de certificado:** especifica AEM formulários que usam certificados para autenticar usuários usando autenticação de certificado ou smart card.
   * **Confiança no OCSP Server:** especifica que os formulários AEM podem usar certificados para se conectar a respondedores OCSP externos
   * **Confiança na identidade:** especifica que os certificados podem ser usados para confiar em informações diferentes dos tipos especificados acima.

   >[!NOTE]
   >
   >O repositório confiável confia implicitamente em um Certificado raiz Adobe para autenticação de certificado, assinatura, assinatura de certificação e identidade.

1. Na caixa Alias, digite o identificador do certificado.
1. Clique em **[!UICONTROL Procurar]** para localizar o certificado e clique em **[!UICONTROL OK]**.

## Exportar um certificado {#export-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Clique no nome do alias do certificado a ser exportado. A página **[!UICONTROL Detalhes do Certificado]** é exibida.
1. Clique em **[!UICONTROL Exportar]**, siga as instruções para exportar o certificado e clique em **[!UICONTROL OK]**.

## Editar as configurações de confiança de um certificado e o tipo de armazenamento de confiança {#edit-a-certificate-s-trust-settings-and-trust-store-type}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Clique no nome do alias do certificado a ser editado.
1. Clique em **[!UICONTROL Atualizar Certificado]**.
1. Para alterar o nome do Alias do certificado, digite um novo nome na caixa Alias.
1. Para atualizar o tipo de armazenamento confiável para o certificado, selecione o tipo de armazenamento confiável apropriado.
1. Para atualizar as restrições de política, na caixa Políticas de Certificado, digite as informações de política e clique em **[!UICONTROL OK]**.

## Excluir um certificado {#delete-a-certificate}

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de armazenamento de confiança > Certificados]**.
1. Marque as caixas de seleção dos certificados a serem excluídos, clique em **[!UICONTROL Excluir]** e, em seguida, clique em **[!UICONTROL OK]**.

