---
layout:     post
title:      bundletool dump命令使用守则
subtitle:   bundletool dump命令使用守则
date:       2021-09-01
author:     坏人
header-img: img/the-first.png
catalog: false
tags:
    - 安卓
---

### 谷歌最新的aab文件需要获取信息 可以用bundletool的dump命令来获取。下列是相关的命令行指令

Description:
    Prints files or extract values from the bundle in a human-readable form.

    Examples:

    1. Prints the AndroidManifest.xml of the base module:
    $ bundletool dump manifest --bundle=/tmp/app.aab

    2. Prints the versionCode of the bundle of the base module:
    $ bundletool dump manifest --bundle=/tmp/app.aab --
    xpath=/manifest/@versionCode

    3. Prints all the resources present in the bundle:
    $ bundletool dump resources --bundle=/tmp/app.aab

    4. Prints a resource's configs from its resource ID:
    $ bundletool dump resources --bundle=/tmp/app.aab --resource=0x7f0e013a

    5. Prints a resource's configs and values from its resource type & name:
    $ bundletool dump resources --bundle=/tmp/app.aab --resource=drawable/icon
    --values

    6. Prints the content of the bundle configuration file:
    $ bundletool dump config --bundle=/tmp/app.aab

Synopsis:
    bundletool dump <manifest|resources|config>
        --bundle=<app.aab>
        [--module=<base>]
        [--resource=<0x7f030001>]
        [--values]
        [--xpath=</manifest/@android:versionCode>]

Flags:
    --bundle: Path to the Android App Bundle.

    --module: (Optional) Name of the module to apply the dump for. Only applies
        when dumping the manifest. Defaults to 'base'.

    --resource: (Optional) Name or ID of the resource to lookup. Only applies
        when dumping resources. If a resource ID is provided, it can be
        specified either as a decimal or hexadecimal integer. If a resource name

        is provided, it must follow the format '<type>/<name>', e.g.
        'drawable/icon'

    --values: (Optional) When set, also prints the values of the resources.
        Defaults to false. Only applies when dumping the resources.

    --xpath: (Optional) XPath expression to extract the value of attributes from

        the XML file being dumped. Only applies when dumping the manifest.