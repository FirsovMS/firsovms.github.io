---
Title:  "Lindotnet Document Page"
Date:   2018-11-30 08:44:42 +0400
Category: opensource
Tags: lindotnet, sip, telephony, opensource
Summary: lindotnet brief docs
---

Hello! Welcome to the [Lindotnet](https://github.com/FirsovMS/lindotnet) documentation page repository.
I've prepared this quick step-by-step guide for people who want use my library, but doesn't know how to start working with it.

First
------------------

1. Each softphone instance requires account data, to create a connection between your softphone instance and SIP-Server.
```csharp
using lindotnet.Classes.Component.Implementation;
...
var testAccount = new Account(login: "test", password: "testpass",
                 host: "192.168.156.2", accountName:"TestUser");
```

2. Next you can create a softphone instance.
```csharp
using lindotnet.Classes.Component.Implementation;
...
var softphoneInstance = new Softphone(testAccount);
```
1. The **Softphone** instance have a multiple events. <br>Most of it can displaying connection status between server and your softphone, call status.

| Event                  | Description                                        |
| :--------------------- | :--------------------------------------------------|
| PhoneConnectedEvent    | registratoin on server succesfull                  |
| PhoneDisconnectedEvent | connection with server was closed                  |
| IncomingCallEvent      | you have incoming call                             |
| CallActiveEvent        | you have connected to call (incoming or outcoming) |
| CallCompletedEvent     | call completed, and connection with caller close   |
| MessageReceivedEvent   | you receive a message                              |
| ErrorEvent             | Some throuble with registration on server or smth  |
| CallHolded             | Active call was holded                             |

You can use this events as you wish. Like here:<br>
```csharp
/*Subscribe on the events */
softphoneInstancesoftphoneInstance.PhoneConnectedEvent += SoftphoneInstance_PhoneConnectedEvent;
softphoneInstance.MessageReceivedEvent += SoftphoneInstance_MessageReceivedEvent;
softphoneInstance.IncomingCallEvent += SoftphoneInstance_IncomingCallEvent;
softphoneInstance.CallActiveEvent += SoftphoneInstance_CallActiveEvent;

....

/* And Implement a handlers! */
private void SoftphoneInstance_PhoneConnectedEvent()
{
    Console.WriteLine("Connected to server sucessfully!");
}

private void SoftphoneInstance_IncomingCallEvent(Call call)
{
    Console.WriteLine($"You have a incoming call: {call.From}, {call.State}");
}

private void SoftphoneInstance_CallActiveEvent(Call call)
{
    Console.WriteLine($"Connect to call completed. Talk with uour opponent {call.From}.");
}

private void SoftphoneInstance_MessageReceivedEvent(string from, string message)
{
    Console.WriteLine($"Message from {from}:{Environment.NewLine}{message}");
}

```