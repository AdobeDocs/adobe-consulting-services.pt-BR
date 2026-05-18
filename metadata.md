---
product: adobe experience manager
solution: Experience Manager
product_v2: id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
description: Consulta à documentação da Experience Manager
type: Documentation
git-repo: https://github.com/AdobeDocs/adobe-consulting-services.en
index: true
source-git-commit: 78d98fcb8f43f48cab7de480af1eac087526cec5
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 2%

---


# Metadados para uso interno

Os metadados no sistema de criação do GitHub são hierárquicos e definidos nos seguintes níveis crescentes de precedentes.

1. metadata.md
1. ToC
1. Artigo

Os metadados definidos no arquivo metadata.md se aplicam a todo o repositório, mas podem ser substituídos nos níveis de índice e artigo. Qualquer substituição dos metadados deve ser feita no nível mais baixo possível.

metadata.md

* `product`
* `git-repo`
* `index: y`

ToCs

* `sub-product`
* `user-guide-title`

Artigo

* `title`
* `description`

Informações adicionais sobre os metadados podem ser encontradas no [guia de criação interno](https://experienceleague.adobe.com/docs/authoring-guide-exl/using/authoring/metadata.html).
