# CRD Configuration

The Kronos-Core Custom Resource Definition (CRD) allows users to define resource schedules for their Kubernetes clusters. The CRD manifest includes several fields that users can configure to customize their resource schedules. Here are the different fields in the manifest:

## startSleep
_type:_ `string` 

_usage:_ Specifies the start time for the sleep period in a 24-hour format (e.g., "13:02").

## endSleep
_type:_ `string` 

_usage:_ Specifies the end time for the sleep period in a 24-hour format (e.g., "22:41").
## weekdays
_type:_ `string` 

_usage:_ Specifies the weekdays on which the schedule should be applied using ISO8601 format. This field can contain individual weekdays, ranges (e.g., "2-5"), and lists (e.g., "2,5,7").

## timezone
_type:_ `string` 

_usage:_ Specifies the timezone for the schedule using the IANA Timezone Database format (e.g., "Africa/Tunis").

## holidays
_type:_ `array of objects` 

_usage:_ Specifies any holidays during which the schedule should be adjusted. Each holiday is represented as an object with the following fields:
### name
 _type:_ `string` 

_usage:_ The name of the holiday.
### date 
 _type:_ `string`

_usage:_ The date or range of dates for the holiday in the format `ISO8601` "YYYY-MM-DD" or "YYYY-MM-DD/DD/DD" if the holiday spans across multiple days.

## includedObjects 
_type:_ `array of objects` 
_usage:_ Specifies the Kubernetes objects to include in the schedule. Each included object is represented as an object with the following fields:

### apiVersion 
 _type:_ `string`
(string): The API version of the Kubernetes object (e.g., "apps/v1").
### kind 
 _type:_ `string`

_usage:_ The kind of Kubernetes object (e.g., "Deployment").
### namespace 
 _type:_ `string`

_usage:_ The namespace of the Kubernetes object.
### includeRef 
 _type:_ `string`

_usage:_ Optionally, the name of the specific object to include. If not defined, it will include all objects of the specified kind and namespace.
### excludeRef 
 _type:_ `string`

_usage:_ Optionally, the name of the specific object to exclude. If not defined, it will exclude no objects.
