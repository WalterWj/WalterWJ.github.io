---
title: TiDB region merge 功能介绍
date: 2019-08-13 00:00:00
categories:
- GitHub 学习
tags:
- TiDB
- Region Merge
typora-root-url: ../../WalterWJ.github.io
---

TiDB region merge 功能介绍

* TiDB 集群中，每个 TiKV 的 Region 数量推荐不超过超过 3w，否则就有可能会导致 tikv 的单线程进程成为瓶颈，影响使用，严重情况下，集群可能性能非常差，接近不可用。

# Region merge 功能配置

使用 pd-ctl 配置：

```shell
"region-schedule-limit": 28,
"replica-schedule-limit": 32,
"tolerant-size-ratio": 50,
"max-merge-region-size": 35,
"max-merge-region-keys": 350000,
"merge-schedule-limit": 24,
```