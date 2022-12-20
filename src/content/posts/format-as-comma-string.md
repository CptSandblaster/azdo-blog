---
title: "How to format an object parameter as a comma-separated string in Azure DevOps yaml pipelines"
date: 2020-12-20T21:00:03+00:00
# weight: 1
# aliases: ["/first"]
tags: ["parameters"]
author: "Sebastian"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
description: "...which is useful for passing parameters to a script"
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
    - name: my-parameter
      type: object
      default:
        - first-item
        - second-item
        - third-item
```

_You can use_

```yaml
${{ join(','),parameters.my-parameter }}
```

_to get_

```yaml
first-item,second-item,third-item
```

Microsoft documentation [here](https://learn.microsoft.com/en-us/azure/devops/pipelines/process/expressions?view=azure-devops#join). 😊

## Details

I typically use a lot of object parameters in my yaml pipelines, especially as I work a lot with templates (since I have many pipelines consuming the same steps).

For simple object parameters (basically lists), it is possible to convert the parameter to a comma-separated string, which can be useful for passing the whole list to a script.

As you saw in the [TL;DR](#tldr), a simple `join()` statement can be used to convert the parameters to a comma-separated string. You can select which character(s) to use as the divider by specifying the first argument of the function. In my example, I specified `,`.

Be sure to encapsulate the expression in `""` to get `"first-item,second-item,third-item"`, like so: `"${{ join(','),parameters.my-parameter }}"`. In many cases, the script (or other) that you are passing the list to will need the quotes to properly understand the input values.