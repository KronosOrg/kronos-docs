# Examples
Welcome to the KronosApp CR Examples Page! Here, we provide various examples to demonstrate how you can configure the KronosApp Custom Resource (CR) for different scenarios. 

The KronosApp CR allows you to define resource schedules for your Kubernetes cluster, specifying sleep and wake times, weekdays, timezone, holidays, and included objects. Below are some example configurations:

## Basic Configuration
**Scenario:** You want to schedule `all Resources` in the default namespace to sleep from 6 pm to 8 am every day and sleep in the weekends.

**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: sleep-at-weekend
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1..5"
  timezone: "Africa/Tunis"
  includedObjects: 
    - apiVersion: ""
      kind: ""
      namespace: "default"
      includeRef: ""
      excludeRef: ""
```

## Intermediate Configuration: Using inclusion and exclusion
**Scenario:** You want to schedule `Deployments` , except those who has `prod` in their name, in the default namespace to sleep from 6 pm to 8 am every day.
**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: do-not-sleep-prod-deploy
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1..7"
  timezone: "Africa/Tunis"
  includedObjects: 
    - apiVersion: "apps/v1"
      kind: "Deployments"
      namespace: "default"
      includeRef: ""
      excludeRef: ".*prod.*"
```

## Intermediate Configuration: Selective Object Scheduling
**Scenario:** You want to schedule `Deployments` and `StatefulSets` in the default namespace to sleep from 6 pm to 8 am every day.
**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: sleep-only-deploy-sts
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1..7"
  timezone: "Africa/Tunis"
  includedObjects: 
    - apiVersion: "apps/v1"
      kind: ""
      namespace: "default"
      includeRef: ""
      excludeRef: ""
```
## Intermediate Configuration: Registering Holidays
**Scenario:** You want to schedule `Deployments` and `StatefulSets` in the default namespace to sleep from 6 pm to 8 am every day in `New York` timezone and automatically sleep resources in the `Thanks Giving` and `Christmas` holiday.

**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: sleep-on-holidays
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1..7"
  timezone: "America/New_York"
  holidays:
    - name: "Thanksgiving"
      date: "2024-11-28/29"
    - name: "Christmas"
      date: "2024-12-25"
  includedObjects: 
    - apiVersion: "apps/v1"
      kind: ""
      namespace: "default"
      includeRef: ""
      excludeRef: ""
```

## Intermediate Configuration: Selective Weekdays
**Scenario:** You want to schedule `all resources` in the default namespace to sleep from 6 pm to 8 am but only on `Monday`, `Wednesday` and from `Friday` to `Saturday`.

**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: selective-weekdays
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1-3-5..7"
  timezone: "Africa/Tunis"
  includedObjects: 
    - apiVersion: ""
      kind: ""
      namespace: "default"
      includeRef: ""
      excludeRef: ""
```

## Advanced Configuration: Selective Object Scheduling with Inclusion and Exclusion
**Scenario:** You want to schedule `Deployments` and `StatefulSets`, except those who has `prod` in their name, and `CronJobs` except a CronJob that is called "prod-health-check" in the default namespace to sleep from 6 pm to 8 am every day.

**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: sleep-only-deploy-sts-regex
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1-3-5..7"
  timezone: "America/New_York"
  holidays:
    - name: "Thanksgiving"
      date: "2024-11-28/29"
    - name: "Christmas"
      date: "2024-12-25"
  includedObjects: 
    - apiVersion: "apps/v1"
      kind: ""
      namespace: "default"
      includeRef: ""
      excludeRef: ".*prod.*"
    - apiVersion: "batch/v1"
      kind: "CronJobs"
      namespace: "default"
      includeRef: ""
      excludeRef: "prod-health-check"
```

## Legendary Configuration: 
**Scenario:** Honestly, too legendary for me to explain. Just know that you can define the `KronosApp` like the following:
**Configuration:**
```yaml
apiVersion: core.wecraft.tn/v1alpha1
kind: KronosApp
metadata:
  labels:
  name: legendary-scheduling
spec:
  startSleep: "18:00"
  endSleep: "08:00"
  weekdays: "1-3-5..7"
  timezone: "America/New_York"
  holidays:
    - name: "Thanksgiving"
      date: "2024-11-28/29"
    - name: "Christmas"
      date: "2024-12-25"
  includedObjects: 
    - apiVersion: "apps/v1"
      kind: "Deployments"
      namespace: "default"
      includeRef: ".*v1.*"
      excludeRef: ".*prod.*"
    - apiVersion: "apps/v1"
      kind: "StatefulSets"
      namespace: "default"
      includeRef: ""
      excludeRef: ".*db.*"
    - apiVersion: "batch/v1"
      kind: "CronJobs"
      namespace: "default"
      includeRef: ".*health-check.*"
      excludeRef: "prod-health-check|staging-health-check"
```