+++ 
draft = false
date = 2021-12-14T19:33:26+08:00
title = "史诗级apache log4j2漏洞"
description = "史诗级apache log4j2漏洞,影响数百万项目"
slug = ""
authors = ["nebula"]
tags = []
categories = []
externalLink = ""
series = []
+++

2021年末大事无疑是apache log4j2漏洞，影响数以万计的项目,其中包括一些著名的开源和商务用组件和项目。
估计没有这次的漏洞，好多人应该都忘了JNDI(Java Naming and Directory Interface)了吧。

[CVE-2021-44228](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2021-44228):
```
Apache Log4j2 JNDI features do not protect against attacker controlled LDAP and other JNDI related endpoints
攻击者利用LDAP和JNDI进行漏洞攻击

Descripton: Apache Log4j2 <=2.14.1 JNDI features used in configuration, log messages, 
and parameters do not protect against attacker controlled LDAP and other JNDI related endpoints. 
An attacker who can control log messages or log message parameters can execute arbitrary code loaded from LDAP servers 
when message lookup substitution is enabled. From log4j 2.15.0, this behavior has been disabled by default.
```
## 影响版本范围
```text
Versions Affected: all versions from 2.0-beta9 to 2.14.1
```

## 解决方案

- 临时修复方案
```text
Mitigation: In releases >=2.10, this behavior can be mitigated by setting either the system property log4j2.formatMsgNoLookups or the environment variable LOG4J_FORMAT_MSG_NO_LOOKUPS to true. 
For releases from 2.7 through 2.14.1 all PatternLayout patterns can be modified to specify the message converter as %m{nolookups} instead of just %m. 
For releases from 2.0-beta9 to 2.7, the only mitigation is to remove the JndiLookup class from the classpath: zip -q -d log4j-core-*.jar org/apache/logging/log4j/core/lookup/JndiLookup.class.
```
- 升级log4j2组件包到2.15.0以上

## 漏洞原因解析


[![Log4j高危漏洞](https://logging.apache.org/log4j/2.x/images/logo.png)](https://player.bilibili.com/player.html?aid=464689876&bvid=BV1FL411E7g3&cid=458389126&page=1 "Log4j高危漏洞")

    Log4j高危漏洞 (补充视频)
[![Log4j高危漏洞 (补充视频)](https://logging.apache.org/log4j/2.x/images/logo.png)](https://player.bilibili.com/player.html?aid=677331278&bvid=BV18U4y1K72L&cid=458847554&page=1 "Log4j高危漏洞 (补充视频)")

