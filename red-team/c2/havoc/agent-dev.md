# Agent dev

## 1: Understanding the interface

Before writing the agent and its handler, we need to understand how Havoc handles third party agents.

#### Callback specifications <a href="#callback-specifications" id="callback-specifications"></a>

Since we are handling our own custom agent's callbacks ourselves, there isn't a fixed callback data structure we have to follow. However, there is a fixed set of bytes that must be prepended to each callback that gives Havoc some basic information on how to handle the callback. These bytes are as such:

Copy

```
[4 bytes] size - this is the total size (in bytes) of the request (including the 12 byte header)
[4 bytes] magic value - this is the value that is used to identify the custom agent type. It has to be common between all agents of the same type.
[4 bytes] agent ID - this is a 4 byte agent ID. This can be any value, but it should be unique per agent, so randomly generating it during runtime is a good idea.
```

So the structure of a typical callback should be something like this:

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Callback structure</p></figcaption></figure>

#### The third party agent system <a href="#the-third-party-agent-system" id="the-third-party-agent-system"></a>

The way Havoc third party agents work, is that any data sent to a valid C2 listening interface (http/s, external c2 etc.) is checked for its magic value, and forwarded to the appropriate agent handler. For example:

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Havoc third party agent system</p></figcaption></figure>



That's pretty much all you need to understand about Havoc's third party agent interface.
