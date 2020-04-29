---
title: Refatoração de SocialUtils
seo-title: Refatoração de SocialUtils
description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
seo-description: The package com.adobe.cq.social.ugcbase.SocialUtils was deprecated in AEM 6.1
uuid: 54a0d98e-5ead-4c12-850f-8252ea9b3263
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 4ade0d6b-041e-4a2f-98f8-3b8fcae0fb29
translation-type: tm+mt
source-git-commit: 3296db289b2e2f4ca0d1981597ada6ca1310bd46

---


# Refatoração de SocialUtils {#socialutils-refactoring}

## Pacote SocialUtils obsoleto {#socialutils-package-deprecated}

O pacote `com.adobe.cq.social.ugcbase.SocialUtils` foi substituído no AEM 6.1.

The following tables list the methods to use in place of SocialUtils methods.

## SocialResourceUtilities Package  {#socialresourceutilities-package}

| Methods in com.adobe.cq.social.srp.utilities.api.SocialResourceUtilities |
|---|
| Boolean checkPermission(ResourceResolver resolver, String path, String action) |  |
| SocialResourceProvider getSocialResourceProvider(Resource resource) |  |
| SocialResourceConfiguration getStorageConfig(Resource resource) |  |
| Resource getUGCResource(Resource userResource) |  |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrf) | novo |
| Resource getUGCResource(Resource userResource, ResourceResolverFactory rrf, String resourceTypeHint) | novo |
| Resource getUGCResource(Resource userResource, String resourceTypeHint) |  |
| booleano hasModeratePermissions(recurso de recurso) |  |
| String resourceToACLPath(Resource) |  |
| String resourceToUGCStoragePath (recurso) | replaces String resourceToUGCPath(Resource resource) |
| String UGCToResourcePath(Resource resource) |  |
| String UGCToResourcePath(String ugcPath) | method signature changed |
| String UGCToResourcePath(String ugcPath, ResourceResolver resolver) | novo |

| Métodos em `com.adobe.cq.social.`utilities.resource.api.SocialResourceUtilities |
|---|
| SocialResourceProvider getSocialResourceProvider(Resource resource) | replaces SocialResourceProvider getConfiguredProvider(Resource resource) |

## SCFUtilities Package {#scfutilities-package}

| Methods in `com.adobe.cq.social.`utilities.scf.api.SCFUtilites |
|---|
| String getAvatar(UserProperties userProperties) |
| String getAvatar(UserProperties userProperties, int size) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar) |
| String getAvatar(UserProperties userProperties, String absoluteDefaultAvatar, SocialUtils.AVATAR_SIZE size) |
| Page getContainingPage(Resource resource) |
| String getSocialProfileURL(String username, ResourceResolver resolver, Page page) |
| UserProperties getUserProperties(ResourceResolver resolver, String userId) |

## For Internal Use Only {#for-internal-use-only}

| booleano canAddNode(Session session, String path) |
|---|
| String createUniqueNameHint(mensagem String) |
| String createUniqueNameHint(mensagem String, int numRandomChars) |
| String generateRandomString(int length) |
| SocialResourceConfiguration getDefaultStorageConfig() |
| Page getPage(String path, ResourceResolver resolver) |
| String getPagePath(Resource resource) |
| String getPagePath(String path) |
| String getResourceTypeForIncludedResource(Componente de recurso, String defaultResourceType, String designPropertyName) |
| String getResourceTypeFromDesign(Recurso, String styleProperty, String defaultValue) |
| boolean isResourceOwner(Recurso) |
| String mapUGCPath(Recurso) |
| String mapUGCPath(String ugcPath, ResourceResolver resolvedor) |
| boolean mayPost(ResourceResolver resolver, Resource resource) |
| String prepareUserGeneratedContent(ResourceResolver resolver, String path) |

## Methods No Longer Available {#methods-no-longer-available}

| Node createNode(ResourceResolver resolver, String path, String nodeType) |
|---|
| Resource getResourceAtPath(ResourceResolver resolver, String path) |
| Resource getResourceAtPath(ResourceResolver resolver, String path, String resourceType) |
| Configuração getStorageCloudServiceConfig (recurso de recurso) |
| TranslationManager getTranslationManager() |
| TranslationSaveQueue getTranslationSaveQueue() |
| booleano mayAccessUGC(ResourceResolver resolver) |

