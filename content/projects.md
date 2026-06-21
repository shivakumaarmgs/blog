+++
title = "Projects"
date = 2024-01-01
draft = false
layout = "projects"
hideMeta = true

[[projects]]
name = "Async Fraud Response System"
company = "Solaris Group"
period = "2022–Present"
stack = ["Java", "SpringBoot", "AWS (SQS/SNS, Lambda, ECS)", "PostgreSQL", "Terraform"]
problem = "Fraud events were being detected but responses were slow and manual — blocking a card or locking an account required human intervention, and every second of delay meant potential financial loss for customers."
solution = "A fully async fraud-response system with a pluggable remediation framework. When a fraud signal fires, the system automatically evaluates the event and dispatches the right action — blocking card bindings, locking accounts, or triggering partner webhooks — without human involvement. Each remediation action is a self-contained plugin, making it easy to add new response types without touching core logic.\n\nSubsequently evolved this into a hybrid model: layering in synchronous fraud checks at critical moments — transaction authorization and web login — so fraud can be blocked *before* it completes, not just cleaned up after."
outcome = [
  "Automated remediation running end to end in **under 10 seconds**",
  "Zero manual intervention required for standard fraud event types",
  "Synchronous checks at transaction and login touchpoints closing the gap between detection and prevention"
]

[[projects]]
name = "JobsPikr — Jobs Data Platform"
company = "PromptCloud"
period = "2016–2022"
stack = ["Ruby", "Ruby on Rails", "React", "ElasticSearch", "ELK", "Redis", "Resque", "MySQL", "RSpec", "Shell"]
problem = "PromptCloud had strong web-scraping infrastructure but no product targeting the jobs data market. The opportunity was to build a reliable, queryable feed of job postings at a scale that enterprises and ML teams could actually depend on."
solution = "Took JobsPikr from concept to a production-grade distributed platform. Built the ingestion pipeline to collect and normalize job postings from across the web, a distributed ElasticSearch cluster to store and index them, and a query layer serving both internal teams and external customers via API. Also built real-time monitoring and alerting on ELK to surface pipeline health and capacity signals. Led the Ruby on Rails team directly and coordinated the leads of the JobsPikr platform and ML teams throughout."
outcome = [
  "**1M+ job postings** processed through the pipeline",
  "**20M ingestions** and ~**1M real-time queries** handled daily",
  "Grew into a standalone product serving internal analytics and external enterprise customers",
  "Monitoring stack driving infrastructure and capacity decisions in real time"
]
+++

A few projects I'm proud of — systems built at scale, in production, with real stakes.
