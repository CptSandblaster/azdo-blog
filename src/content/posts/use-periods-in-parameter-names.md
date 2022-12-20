---
title: "How to use parameters names with periods in Azure DevOps yaml pipelines"
date: 2020-12-20T21:30:03+00:00
# weight: 1
# aliases: ["/first"]
tags: []
author: "Sebastian"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "...which is common with .net developers"
canonicalURL: "https://canonical.url/to/page" # TODO
disableHLJS: true # to disable highlightjs
disableShare: true
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
editPost:
    URL: "https://github.com/<path_to_repo>/content" # TODO
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

## TL;DR

_If you have_

```yaml
parameters:
    - name: My.Period.Parameter
      type: string
      default: "A value"
```

_You can use_

```yaml
${{ parameters['My.Period.Parameter'] }}
```

## Details

Sometimes, you come across pipelines built by .net developers. In my experience, these developers loves periods in their variables. Not that there is anything wrong with that, but it does not play nice with Azure DevOps.

The typical way to reference a parameter is `${{ parameters.my-parameter }}`. However, if you are using a parameter with a period in it's name, like `${{ parameters.My.Period.Parameter }}`, Azure DevOps will throw and error when you try to compile the pipeline.

For these cases, using the lesser known syntax of `${{ parameters['PARAMETER'] }}` resolves the issue. It is a bit uglier, but it beats changing all parameter names everywhere.

From what I know, there is no limitation of where you can use this.