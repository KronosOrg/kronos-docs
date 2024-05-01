---
sidebar_position: 1
---

# Getting Started
## Overview
In today's rapidly evolving digital landscape, software deployments have become increasingly demanding in terms of compute power, requiring substantial resources such as RAM, CPU, and storage.

The surge in cloud-native applications has propelled the need for extensive data centers to meet this demand. However, this rapid growth comes with its challenges, particularly in resource management and sustainability.

### Resource Liberation for Sustainability:
One critical aspect of addressing the resource demand is the need to liberate resources when they are not actively utilized. This approach not only optimizes resource allocation but also reduces the carbon footprint associated with excessive resource consumption. 
By dynamically allocating resources based on real-time demand, organizations can significantly enhance their sustainability efforts while also achieving cost savings.

## What is Kronos ?

Kronos is a kubernetes Operator designed to facilitate the scheduling of resource wake and sleep cycles in a Kubernetes environment. It boasts a comprehensive set of features that allow users to selectively choose which resources to schedule, offering a high level of flexibility and control. 
Kronos also has the ability to integrate seamlessly with the command-line interface (CLI) Kronos-CLI, enabling users to instantly wake or sleep resources as needed.

### Cherry Picking 

Kronos introduces a highly flexible approach to resource scheduling through its Custom Resource Definition (CRD), KronosApp. This CRD empowers users to finely tune resource selection using regex support, enabling them to target specific resources based on their unique identifiers or characteristics.

The inclusion and exclusion mechanisms within KronosApp allow users to precisely define which resources should be considered for scheduling and which should be excluded. This level of granularity ensures that resources are selected based on specific criteria, such as ApiVersion or Kinds, providing a highly customizable scheduling solution.

Kronos is designed with an "All if Nothing" approach, ensuring that if a specific field is not explicitly specified, it will default to including all targets of that field.

### Eco-System 

Kronos is not just an operator; it is a comprehensive suite of software components that work together to provide a solution for resource scheduling in Kubernetes environments. This suite of software is designed to integrate with each other, offering ease of use and a robust ecosystem that enhances the overall user experience.

#### Kronos-Core
At its core, Kronos includes the operator itself aka Kronos-Core, which manages the scheduling of resource wake and sleep cycles. This operator is responsible for interpreting user-defined schedules and interacting with the Kubernetes API to execute them.

#### Kronos-CLI 

Kronos' CLI component provides a convenient interface for users to interact with the system from the command line. In addition to standard operations, such as scheduling resource wake and sleep cycles, the CLI includes predefined schedules like forceWake and forceSleep for emergency situations.

The forceWake schedule can be used to immediately wake up resources that are scheduled to be asleep. This is particularly useful for debugging or troubleshooting scenarios that require immediate access to resources, even outside of regular operating hours.

Conversely, the forceSleep schedule allows users to force resources to enter sleep mode, overriding any existing schedules. This can be helpful in situations where resources need to be shut down quickly to conserve energy or address security concerns.

### Why the name Kronos ?
The name "Kronos" or Κρονος for the operator was inspired by the Greek god of time, Cronos, whose primary functions in Greek mythology included being the god of time and the controller of that domain. According to ancient philosopher Cicero, Cronos was responsible for monitoring the change of seasons and the duration of time, essentially setting how long the seasons and a year would last.

This association with the god Cronos is fitting for the Kronos operator, as it similarly controls the scheduling of resources in a Kubernetes environment. Like the god Cronos, who monitored and set the duration of seasons and time, the Kronos operator monitors and controls the scheduling of resources, ensuring that they are awake or asleep according to predefined schedules. Just as Cronos was a master of time, the Kronos operator is a master of resource scheduling, providing users with precise control over resource allocation and utilization.