---
sidebar_position: 5
---

# Supported Resources

## Overview

In its current version, Kronos supports four main types of resources: Deployments, StatefulSets, ReplicaSets, and CronJobs. Each of these resource types has specific characteristics and requirements for scheduling sleep and wake cycles.

- **apps/v1**
    - *Deployments*
    - *StatefulSets*
    - *ReplicaSets*
- **batch/v1**
    - *CronJobs*


### Deployments
**release:** `v0.2.0`

Deployments are used to manage a replicated application, typically with multiple instances (pods) running concurrently.
Kronos supports deployments by managing the replicas field in the Deployment spec. Sleeping a Deployment involves setting the replicas to 0, effectively stopping all instances of the application. Waking up a Deployment resets the replicas to their original number, allowing the application to start running again.
### StatefulSets
**release:** `v0.2.0`

StatefulSets are similar to Deployments but are used for stateful applications that require stable and unique network identifiers.
Kronos supports StatefulSets by managing the replicas field in the StatefulSet spec. Sleeping a StatefulSet involves setting the replicas to 0, stopping all instances of the application. Waking up a StatefulSet resets the replicas to their original number, allowing the application to resume its stateful operations.
### ReplicaSets 
**release:** `v0.3.0`

ReplicaSets are used to ensure a specified number of pod replicas are running at any given time. Kronos supports ReplicaSets by managing the replicas field in the ReplicaSet spec. Sleeping a ReplicaSet involves setting the replicas to 0, effectively stopping all instances of the pods managed by the ReplicaSet. Waking up a ReplicaSet resets the replicas to their original number, allowing the pods to start running again.
### CronJobs
**release:** `v0.2.0`

CronJobs are used to run scheduled tasks in a Kubernetes cluster, similar to cron jobs in a Unix-like environment.
Kronos supports CronJobs by managing the schedule field in the CronJob spec. Sleeping a CronJob involves pausing the execution of scheduled tasks. Waking up a CronJob resumes the execution of tasks according to the defined schedule.