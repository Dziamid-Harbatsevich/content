---
title: MessageChannel()
slug: Web/API/MessageChannel/MessageChannel
tags:
  - API
  - Channel messaging
  - Constructor
  - MessageChannel
  - Reference
browser-compat: api.MessageChannel.MessageChannel
---
{{APIRef("HTML DOM")}}

The `MessageChannel()` constructor of the {{domxref("MessageChannel")}}
interface returns a new {{domxref("MessageChannel")}} object with two new
{{domxref("MessagePort")}} objects.

{{AvailableInWorkers}}

## Syntax

```js
new MessageChannel();
```

### Returns

A newly created {{domxref("MessageChannel")}} object.

## Example

In the following code block, you can see a new channel being created using the
{{domxref("MessageChannel()", "MessageChannel.MessageChannel")}} constructor. When the
IFrame has loaded, we pass `port2` to the IFrame using
{{domxref("MessagePort.postMessage")}} along with a message. The
`handleMessage` handler then responds to a message being sent back from the
IFrame (using {{domxref("MessagePort.message_event", "onmessage")}}), putting it into a paragraph.
{{domxref("MessageChannel.port1")}} is listened to, to check when the message arrives.

```js
var channel = new MessageChannel();
var para = document.querySelector('p');

var ifr = document.querySelector('iframe');
var otherWindow = ifr.contentWindow;

ifr.addEventListener("load", iframeLoaded, false);

function iframeLoaded() {
  otherWindow.postMessage('Hello from the main page!', '*', [channel.port2]);
}

channel.port1.onmessage = handleMessage;
function handleMessage(e) {
  para.innerHTML = e.data;
}
```

For a full working example, see our [channel
messaging basic demo](https://github.com/mdn/dom-examples/tree/master/channel-messaging-basic) on GitHub ([run it live
too](https://mdn.github.io/dom-examples/channel-messaging-basic/)).

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Using
  channel messaging](/en-US/docs/Web/API/Channel_Messaging_API/Using_channel_messaging)
