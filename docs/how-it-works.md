---
sidebar_position: 2
---

# How It Works

To use Kronos, users first define their resource scheduling requirements using a Custom Resource Definition (CRD) provided by Kronos called **KronosApp**. The CRD allows users to specify their schedules in a structured format that Kronos understands and can act upon. Here's a simple example of how a CRD for Kronos might look:

```yaml 
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: sleep-at-weekend
spec:
  startSleep: "18:00"
  endSleep: "07:00"
  weekdays: "1..5"
  timezone: "Africa/Tunis"
  includedObjects: 
    - apiVersion: "apps/v1"
      kind: "Deployment"
      namespace: "default"
      includeRef: ""
      excludeRef: ""
```

This schedule will put all included resources, in this case, all deployments in the default namespace, to sleep at 6 pm CET and wake them up at 7 am CET. For more advanced use cases, please consult the **[Examples](./examples.md)** page.

To learn more about the fields and the available customization options for the CRD, please refer to this **[CRD Configuration](./crd-configuration.md)** page, where we explain how to configure your schedule correctly based on your requirements.

## Under The Hood 

Kronos operates by continuously listening for changes in the KronosApp CRD (Custom Resource Definition) within the Kubernetes cluster. When a new KronosApp resource is created or updated, Kronos retrieves the user-defined configuration from the CRD and attempts to apply it to the cluster.

One of Kronos' key features is its custom logic for determining when to make resources go to sleep or wake them up. Kronos uses the current time, obtained from the system clock, to compare against the scheduled sleep and wake times specified in the KronosApp CRD. Based on this comparison, Kronos determines whether resources should be put to sleep or awakened.

## Definition of Sleep and Wake 

In the context of Kronos, the definition of sleep and wake varies based on the type of resource being managed. Kronos categorizes resources into two main types: replica-based resources and status-based resources.

### Replica-based resources:

Sleeping a **Replica-Based** resource involves setting its replicas to *0*, effectively shutting down all instances of that resource.
Waking up a **Replica-Based** resource means resetting the replicas of the resource to their *original number*, allowing instances to start running again.

### Status-based resources:

Sleeping a **Status-based** resource can be achieved through various methods, but in the current version of Kronos, it involves suspending the resource. This suspension is typically done by setting a specific field (e.g., `suspended`) to *true*, indicating that the resource is inactive.
Waking up a **Status-based** resource involves reversing the action taken during sleep. In this version of Kronos, waking up a status-based resource is done by setting the aforementioned field (e.g., `suspended`) to *false*, indicating that the resource is now active again.

## Supported Resources:


In its current version, Kronos supports three main types of resources: Deployments, StatefulSets, and CronJobs. Each of these resource types has specific characteristics and requirements for scheduling sleep and wake cycles.

### Deployments
Deployments are used to manage a replicated application, typically with multiple instances (pods) running concurrently.
Kronos supports deployments by managing the replicas field in the Deployment spec. Sleeping a Deployment involves setting the replicas to 0, effectively stopping all instances of the application. Waking up a Deployment resets the replicas to their original number, allowing the application to start running again.
### StatefulSets
StatefulSets are similar to Deployments but are used for stateful applications that require stable and unique network identifiers.
Kronos supports StatefulSets by managing the replicas field in the StatefulSet spec. Sleeping a StatefulSet involves setting the replicas to 0, stopping all instances of the application. Waking up a StatefulSet resets the replicas to their original number, allowing the application to resume its stateful operations.
### CronJobs
CronJobs are used to run scheduled tasks in a Kubernetes cluster, similar to cron jobs in a Unix-like environment.
Kronos supports CronJobs by managing the schedule field in the CronJob spec. Sleeping a CronJob involves pausing the execution of scheduled tasks. Waking up a CronJob resumes the execution of tasks according to the defined schedule.

Kronos is designed for extensibility, meaning it can support any type of resource that is replica-based (e.g., `Deployment`) or status-based (e.g., `CronJob`). This design allows Kronos to adapt to different types of applications and workload patterns, making it a versatile solution for resource scheduling in Kubernetes environments.