---
layout: post
title:  "Elasticstack"
date:   2021-09-08 14:00:00 +0700
categories: devops
tags: [devops]
---

## ElasticStack
Elastic Stack is group of open source projects that previously called ELK stack. The stack helps users to get Data from various sources in any form, gather then store and finally visualize information.
There are 4 major compoments of stack.

## Beat
Beat is component that used for gather logs or metric installed as agent in server. Beat type depends on what kind of component that it attached. For application, the preferred way is to deploy as side-car. Beat types example are Filebeat, Metricbeat. User can define how input, processor, output works.
```
Input -> Processor -> Output

Example
 ---------      ------------------      ------------------
| logfile | -> | - add metadata   | -> | push to logstash |
|         |    | - encode to json |    |                  |
 ---------      ------------------      ------------------
```

## Logstash
Logstash is data processing pipeline that support various format of input and help transform into common format that easy to be digested by downstream(in most cases Elasticsearch). Logstash can be customized by adding filters.

## ElasticSearch
ElasticSearch is text search and analytics engine that provide REST api interface for developer to interact with. In elasticstack, It serves as the main component that stores and computes data.

## Kibana
This is the last part of pipeline. Kibana provides web based GUI to user to visualize data that store in elasticsearch.

## Alternative
- Datadog
- Dynatrace
