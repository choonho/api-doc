---
title: "UserChannel"
linkTitle: "UserChannel"
weight: 3
bookFlatSection: true
---
# [UserChannel](#UserChannel)
A UserChannel is a destination where Notifications are delivered. Notifications are generated via the Protocol set by each User.


>  **Package : spaceone.api.notification.v1**

<br>
<br>

## UserChannel





**UserChannel Methods:**


| Method | Request | Response |
| :----- | :-------- | :-------- |
| [**create**](./UserChannel#create) | [CreateUserChannelRequest](UserChannel#createuserchannelrequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**update**](./UserChannel#update) | [UpdateUserChannelRequest](UserChannel#updateuserchannelrequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**set_schedule**](./UserChannel#set_schedule) | [UpdateUserChannelScheduleRequest](UserChannel#updateuserchannelschedulerequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**set_subscription**](./UserChannel#set_subscription) | [UpdateUserChannelSubscriptionRequest](UserChannel#updateuserchannelsubscriptionrequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**enable**](./UserChannel#enable) | [UserChannelRequest](UserChannel#userchannelrequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**disable**](./UserChannel#disable) | [UserChannelRequest](UserChannel#userchannelrequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**delete**](./UserChannel#delete) | [UserChannelRequest](UserChannel#userchannelrequest) | [Empty](UserChannel#empty) |
| [**get**](./UserChannel#get) | [GetUserChannelRequest](UserChannel#getuserchannelrequest) | [UserChannelInfo](UserChannel#userchannelinfo) |
| [**list**](./UserChannel#list) | [UserChannelQuery](UserChannel#userchannelquery) | [UserChannelsInfo](UserChannel#userchannelsinfo) |
| [**stat**](./UserChannel#stat) | [UserChannelStatQuery](UserChannel#userchannelstatquery) | [Struct](UserChannel#struct) |



    
<br>

### create

Creates a new UserChannel. A UserChannel is a channel that delivers a Notification to users when the Notification is created. When creating a UserChannel, one Protocol must be selected, and an Notification is dispatched via the selected Protocol.



> **POST** /notification/v1/user-channel/create
>





 {{< tabs " create " >}}

 {{< tab "Request Example" >}}



[CreateUserChannelRequest](./UserChannel#createuserchannelrequest)

* **protocol_id** (string)   `Required` 

  *The ID of protocol that will be set in user channel.*


* **name** (string)   `Required` 

  *The name of User Channel. It can have a maximum of 255 characters.*


* **data** (Struct)   `Required` 

  *The data for using user channel.
This data is encrypted and stored in the Secret service if JSON schema in the protocol's metadata is set to SECRET type.
In this case, the secret ID that is stored in the security service will be returned and the data value will be empty.
if JSON schema in the protocol's metadata is set to PLAIN_TEXT type, This data is not encrypted and stored directly in the DB.*


* **is_subscribe** (bool)  

  *Indicates whether subscriptions will be used.*


* **subscriptions** (string)  `Repeated`   

  *When using subscriptions, it indicates the topic list to subscription.
If is_subscribe is set to false, this value is ignored.*


* **is_scheduled** (bool)  

  *Indicates whether schedule will be used.*


* **schedule** (UserChannelSchedule)  

  *Schedule for which you want to receive notifications through the user channel.*


* **tags** (Struct)  

  *The tags for user channel.*





{{< highlight json >}}
{
   "protocol_id": "protocol-123456789012",
   "name": "Email",
   "data": {
       "email": "user1@email.com"
   },
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### update

Updates a specific UserChannel. A UserChannel that has already been configured cannot be changed. Instead, the data required for dispatching Notifications to a UserChannel can be updated.



> **POST** /notification/v1/user-channel/update
>





 {{< tabs " update " >}}

 {{< tab "Request Example" >}}



[UpdateUserChannelRequest](./UserChannel#updateuserchannelrequest)

* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*


* **name** (string)  

  *The name of user channel. It can have a maximum of 255 characters.*


* **data** (Struct)  

  *The data for using user channel.
This data is encrypted and stored in the Secret service if JSON schema in the protocol's metadata is set to SECRET type.
In this case, the secret ID that is stored in the security service will be returned and the data value will be empty.
if JSON schema in the protocol's metadata is set to PLAIN_TEXT type, This data is not encrypted and stored directly in the DB.*


* **schedule** (UserChannelSchedule)  

  *Set the level of notification.
If a notification has a level and a notification level that this channel can receive is set, a notification is dispatched only if the notification level is the same.*


* **tags** (Struct)  

  *The tags for user channel.*





{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email2",
   "data": {
       "email": "user1@gmail.com"
   },
   "tags": {
       "type": "test"
   }
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### set_schedule

Sets a schedule for a UserChannel. A schedule defines the time to receive a Notification. When a Notification is created, you can set the day of the week and time you want to receive it. When you set the day of the week, you can receive a notification only on the day of the week you set. If you also set the start time and end time with the day of the week, you can receive a Notification only at the scheduled time on the day of the week you set. If there is no schedule set in a UserChannel, Notifications will be dispatched at all times via the UserChannel.



> **POST** /notification/v1/user-channel/set-schedule
>





 {{< tabs " set_schedule " >}}

 {{< tab "Request Example" >}}



[UpdateUserChannelScheduleRequest](./UserChannel#updateuserchannelschedulerequest)

* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*


* **is_scheduled** (bool)   `Required` 

  *Indicates whether schedule will be used.*


* **schedule** (UserChannelSchedule)  

  *Schedule for which you want to receive notifications through the user channel.*





{{< highlight json >}}
{
   "user_channel_id": "user-ch-28097e8d5d59",
   "is_scheduled": true,
   "schedule": {
       "day_of_week": [
           "MON",
           "TUE",
           "WED",
           "THU",
           "FRI"
       ],
       "end_hour": 9
   },
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### set_subscription

Sets a subscription for a UserChannel. A subscription is a topic for channels to subscribe to and get notified about. If a UserChannel has subscriptions, a Notification is dispatched only if the topic of the Notification is the same as the one set in the subscriptions. If there is no subscription in a UserChannel, all Notifications will be dispatched.



> **POST** /notification/v1/user-channel/set-subscription
>





 {{< tabs " set_subscription " >}}

 {{< tab "Request Example" >}}



[UpdateUserChannelSubscriptionRequest](./UserChannel#updateuserchannelsubscriptionrequest)

* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*


* **is_subscribe** (bool)   `Required` 

  *Indicates whether subscriptions will be used.*


* **subscriptions** (string)  `Repeated`   

  *If is_subscribe is set to false, this value is ignored.*





{{< highlight json >}}
{
   "user_channel_id": "user-ch-28097e8d5d59",
   "is_subscribe": true,
   "subscriptions": [
       "monitoring.Alert"
   ],
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### enable

Enables a specific UserChannel. If a UserChannel is enabled, the UserChannel can be used and the Notification can be dispatched. Even if a UserChannel is enabled, if the Protocol used in the UserChannel is disabled, the Notification is not dispatched.



> **POST** /notification/v1/user-channel/enable
>





 {{< tabs " enable " >}}

 {{< tab "Request Example" >}}



[UserChannelRequest](./UserChannel#userchannelrequest)

* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*





{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012"
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### disable

Disables a specific UserChannel. If a UserChannel is disabled, the Notification is not dispatched, even if it is created.



> **POST** /notification/v1/user-channel/disable
>





 {{< tabs " disable " >}}

 {{< tab "Request Example" >}}



[UserChannelRequest](./UserChannel#userchannelrequest)

* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*





{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012"
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### delete

Deletes a specific UserChannel. You must specify the `user_channel_id` of the UserChannel to delete.



> **POST** /notification/v1/user-channel/delete
>





 {{< tabs " delete " >}}

 {{< tab "Request Example" >}}



[UserChannelRequest](./UserChannel#userchannelrequest)

* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*





{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012"
}
{{< /highlight >}}
{{< /tab >}}



{{< /tabs >}}


    
<br>

### get

Gets a specific UserChannel. Prints detailed information about the UserChannel, including the Protocol configured and the Notification settings.



> **POST** /notification/v1/user-channel/get
>





 {{< tabs " get " >}}



 {{< tab "Response Example" >}}

[UserChannelInfo](#USERCHANNELINFO)
* **user_channel_id** (string)   `Required` 

  The ID of user channel.

* **name** (string)   `Required` 

  The name of user channel

* **state** (UserChannelState)   `Required` 

  The state of user channel. ENABLED or DISABLED only.

* **data** (Struct)   `Required` 

  The data for using user channel.

* **secret_id** (string)   `Required` 

  The ID of secret encrypted data in the security service

* **is_subscribe** (bool)   `Required` 

  Indicates whether subscriptions will be used.

* **subscriptions** (string)  `Repeated`   `Required` 

  The topic list to subscription.

* **is_scheduled** (bool)   `Required` 

  Indicates whether schedule will be used.

* **schedule** (UserChannelSchedule)   `Required` 

  Schedule for which you want to receive notifications through the user channel.

* **tags** (Struct)   `Required` 

  The tags for user channel.

* **protocol_id** (string)   `Required` 

  The ID of protocol set in the user channel.

* **user_id** (string)   `Required` 

  The ID of user using the user channel.

* **domain_id** (string)   `Required` 

  The ID of domain.

* **created_at** (string)   `Required` 

  User channel creation time.



{{< highlight json >}}
{
   "user_channel_id": "user-ch-123456789012",
   "name": "Email",
   "state": "ENABLED",
   "data": {
       "email": "user1@email.com"
   },
   "protocol_id": "protocol-123456789012",
   "user_id": "user1@email.com",
   "domain_id": "domain-123456789012",
   "created_at": "2022-01-01T08:28:49.108Z"
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### list

Gets a list of all UserChannels. You can use a query to get a filtered list of UserChannels.



> **POST** /notification/v1/user-channel/list
>





 {{< tabs " list " >}}

 {{< tab "Request Example" >}}



[UserChannelQuery](./UserChannel#userchannelquery)

* **query** (Query)  

  *Query format provided by SpaceONE. Please check the link for more information.*


* **user_channel_id** (string)  

  *The ID of user channel.*


* **name** (string)  

  *The name of user channel. It can have a maximum of 255 characters.*


* **state** (UserChannelState)  

  *The state of user channel. ENABLED or DISABLED only.*


* **secret_id** (string)  

  *The ID of secret encrypted data in the security service*


* **protocol_id** (string)  

  *The ID of protocol set in the user channel.*





{{< highlight json >}}
{
   "query": {}
}
{{< /highlight >}}
{{< /tab >}}


 {{< tab "Response Example" >}}

[UserChannelsInfo](#USERCHANNELSINFO)
* **results** (UserChannelInfo)  `Repeated`   `Required` 

  List of queried user channels.

* **total_count** (int32)   `Required` 

  Total counts of queried user channels.



{{< highlight json >}}
{
   "results": [
       {
           "user_channel_id": "user-ch-123456789012",
           "name": "Email",
           "state": "ENABLED",
           "data": {
               "email": "user1@email.com"
           },
           "protocol_id": "protocol-123456789012",
           "user_id": "user1@email.com",
           "domain_id": "domain-123456789012",
           "created_at": "2022-01-01T08:28:49.108Z"
       },
       {
           "user_channel_id": "user-ch-98765432109",
           "name": "Email",
           "state": "ENABLED",
           "data": {
               "email": "user2@email.com"
           },
           "is_scheduled": true,
           "schedule": {
               "day_of_week": [
                   "MON",
                   "TUE",
                   "WED",
                   "THU",
                   "FRI"
               ],
               "start_hour": 3,
               "end_hour": 23
           },
           "protocol_id": "protocol-123456789012",
           "user_id": "user2@email.com",
           "domain_id": "domain-123456789012",
           "created_at": "2022-01-01T06:45:57.260Z"
       }
   ],
   "total_count": 2
}
{{< /highlight >}}
{{< /tab >}}


{{< /tabs >}}


    
<br>

### stat





> **POST** /notification/v1/user-channel/stat
>






    


<br>
<br>

## Message



### CreateUserChannelRequest
* **protocol_id** (string)   `Required` 

  *The ID of protocol that will be set in user channel.*

    
* **name** (string)   `Required` 

  *The name of User Channel. It can have a maximum of 255 characters.*

    
* **data** (Struct)   `Required` 

  *The data for using user channel.
This data is encrypted and stored in the Secret service if JSON schema in the protocol's metadata is set to SECRET type.
In this case, the secret ID that is stored in the security service will be returned and the data value will be empty.
if JSON schema in the protocol's metadata is set to PLAIN_TEXT type, This data is not encrypted and stored directly in the DB.*

    
* **is_subscribe** (bool)  

  *Indicates whether subscriptions will be used.*

    
* **subscriptions** (string)  `Repeated`   

  *When using subscriptions, it indicates the topic list to subscription.
If is_subscribe is set to false, this value is ignored.*

    
* **is_scheduled** (bool)  

  *Indicates whether schedule will be used.*

    
* **schedule** (UserChannelSchedule)  

  *Schedule for which you want to receive notifications through the user channel.*

    
* **tags** (Struct)  

  *The tags for user channel.*

    <br>

### GetUserChannelRequest
* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*

    <br>

### UpdateUserChannelRequest
* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*

    
* **name** (string)  

  *The name of user channel. It can have a maximum of 255 characters.*

    
* **data** (Struct)  

  *The data for using user channel.
This data is encrypted and stored in the Secret service if JSON schema in the protocol's metadata is set to SECRET type.
In this case, the secret ID that is stored in the security service will be returned and the data value will be empty.
if JSON schema in the protocol's metadata is set to PLAIN_TEXT type, This data is not encrypted and stored directly in the DB.*

    
* **schedule** (UserChannelSchedule)  

  *Set the level of notification.
If a notification has a level and a notification level that this channel can receive is set, a notification is dispatched only if the notification level is the same.*

    
* **tags** (Struct)  

  *The tags for user channel.*

    <br>

### UpdateUserChannelScheduleRequest
* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*

    
* **is_scheduled** (bool)   `Required` 

  *Indicates whether schedule will be used.*

    
* **schedule** (UserChannelSchedule)  

  *Schedule for which you want to receive notifications through the user channel.*

    <br>

### UpdateUserChannelSubscriptionRequest
* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*

    
* **is_subscribe** (bool)   `Required` 

  *Indicates whether subscriptions will be used.*

    
* **subscriptions** (string)  `Repeated`   

  *If is_subscribe is set to false, this value is ignored.*

    <br>

### UserChannelInfo
* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*

    
* **name** (string)   `Required` 

  *The name of user channel*

    
* **state** (UserChannelState)   `Required` 

  *The state of user channel. ENABLED or DISABLED only.*

    
* **data** (Struct)   `Required` 

  *The data for using user channel.*

    
* **secret_id** (string)   `Required` 

  *The ID of secret encrypted data in the security service*

    
* **is_subscribe** (bool)   `Required` 

  *Indicates whether subscriptions will be used.*

    
* **subscriptions** (string)  `Repeated`    `Required` 

  *The topic list to subscription.*

    
* **is_scheduled** (bool)   `Required` 

  *Indicates whether schedule will be used.*

    
* **schedule** (UserChannelSchedule)   `Required` 

  *Schedule for which you want to receive notifications through the user channel.*

    
* **tags** (Struct)   `Required` 

  *The tags for user channel.*

    
* **protocol_id** (string)   `Required` 

  *The ID of protocol set in the user channel.*

    
* **user_id** (string)   `Required` 

  *The ID of user using the user channel.*

    
* **domain_id** (string)   `Required` 

  *The ID of domain.*

    
* **created_at** (string)   `Required` 

  *User channel creation time.*

    <br>

### UserChannelQuery
* **query** (Query)  

  *Query format provided by SpaceONE. Please check the link for more information.*

    
* **user_channel_id** (string)  

  *The ID of user channel.*

    
* **name** (string)  

  *The name of user channel. It can have a maximum of 255 characters.*

    
* **state** (UserChannelState)  

  *The state of user channel. ENABLED or DISABLED only.*

    
* **secret_id** (string)  

  *The ID of secret encrypted data in the security service*

    
* **protocol_id** (string)  

  *The ID of protocol set in the user channel.*

    <br>

### UserChannelRequest
* **user_channel_id** (string)   `Required` 

  *The ID of user channel.*

    <br>

### UserChannelSchedule
* **day_of_week** (DayOfWeek)  `Repeated`    `Required` 

  *Day of the week to be notified.
As a list type, only types that can be specified from MON to SUN can be set.*

    
* **start_hour** (int32)   `Required` 

  *Start time to receive notifications.
Only integer type can be set, and 0 to 23 can be.*

    
* **end_hour** (int32)   `Required` 

  *End time to receive notifications.
Only integer type can be set, and 1 to 24 can be.*

    <br>

### UserChannelStatQuery
* **query** (StatisticsQuery)   `Required` 

  *Statistics Query format provided by SpaceONE. Please check the link for more information.*

    <br>

### UserChannelsInfo
* **results** (UserChannelInfo)  `Repeated`    `Required` 

  *List of queried user channels.*

    
* **total_count** (int32)   `Required` 

  *Total counts of queried user channels.*

    <br>
