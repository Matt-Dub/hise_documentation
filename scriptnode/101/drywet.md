---
keywords: Chapter 3: Dry / Wet FX
summary:  A introduction to the split container and how to setup a dry/wet signal routing
author:   Matt_SF
modified: 18.11.2021
---

**1 - INTRO**

In this chapter we'll take a look at how to setup a dry/wet signal routing. Using the `container.split` node we'll be able to creates parallel signal chains to process only one chain and mix its level with the dry signal.

**The nodes we'll use :** 

 - 1 [`container.split`](/scriptnode/list/container/split)
 - 2 [`container.chain`](/scriptnode/list/container/chain)
 - 2 [`core.gain`](/scriptnode/list/core/gain)
 - 1 [`control.xfader`](/scriptnode/list/control/xfader)
 - 1 [`fx.reverb`](/scriptnode/list/fx/reverb)

**2 - SETUP A DRY / WET SIGNAL ROUTING**

Let's build a little reverb wit a Dry/Wet control : 

Add a `container.split` node to the graph and add 2 `container.chain` nodes. These will contain our stuff : 

![83dd2341-b9a1-4575-a683-b08494f2978f-image.png](https://i.imgur.com/JEGr9Dt.png) 
![image](https://user-images.githubusercontent.com/84969276/142740122-e504275e-d6b1-4cb3-a1b3-3c386c0cce81.png)

> See the signal cables ? You can see that the whole signal is send to both the DRY and WET containers and not split into left and right as in the previous example.

Add a `DryWet` parameter and the required nodes as shown on the picture : 1 `core.gain` for the DRY channel and a `core.gain` + a `fx.reverb` for the WET channel and a `control.xfader`. Set the crossfading menu to "RMS" and connect the crossfade sources to the gains :

![image](https://user-images.githubusercontent.com/84969276/142739740-d7e023f7-143a-40ef-a8ca-d05d0900a702.png)

Done ! How simple is that ? Now if you want to build you own reverb and manipulate it via your interface, just create parameters and connect everything : 

![image](https://user-images.githubusercontent.com/84969276/142739770-2398ca4a-93fb-437f-915d-8b2d2f0b041b.png)

> Keep in mind though to take care of the Main parameters's ranges, depending on whether you're controlling linear values, levels, frequencies, etc...
> Use the range editor !

```snippet
HiseSnippet 1345.3oc6Y0rbiTCDViik2MYyB6V.28wrUERYCgEphCwI9GJWfy5JSHK6oEkYjsU4YjlRibh8Rwctw48FOBbka4cfW.dD12.n0Lxdlw+j3XRxlp.eHkUqtG8ou9qaIOosT3PCCERj05GOJfhr1DaOhq5UsGgwQMqgr9.bKRnhJKFa5fQAjvPpKxxZsuQavZ87nnOuauCHdDtCMwDBchf4P+NlOSkXsckuk440f3ROl4mx6cqzzQvqJ7DC.7rFtDJf3zmzkdHQ6VNLxpPcWlRHsUDEMDYk+.g6H6dhy4w9eBKjcpGUOnLxFdPwlaH7b0HVaEUsGyys838cHBdJsSXg0hYgOF2h4xlXOgMdRzDEShHMeXkKK7VKC7JuH3MGHYkBR4igzSw1NRVfJYFMddDtIGRNcH.smFJw9hrt.WU.NvU63S5SaHgASBXqmWpz1Eg+7ruty.tihI3EE7CEJ5K3a8rM9oMVeiedihSOUmNycN8xHEddT4bmVmokWVfawG3eJUtcwyHdCnSbD19Y4zBKGm5DuqS4nf2jyTuHfZFe4hBjg1fu88MqQTDcRwXC7KfJULMbrpQOCT3won0w0ng8Uh.PiOS9CTNB2AdDUV4jtFxLAvGYxg5DEOjoFktFaZMV9EyGkV5RfkEtOE2lob5Me7laN3EXsaa7ZpXeLtdmNTGUBXyia7CWZ4Y9kSJk.kksTcCSoJr9ZfrA9H5YT4oMFN2RzeAmTNDHoADI8XQaOxnsBI9Adzi.ztcwS8DN8sYugNaMTPL.NP6wVN8HbN0KbUJ0JbC09BcjXfhw61hnjrgHK7gC7sgl5NzpFzA1rxoqxhGWROVqVrob2nA+M7wLYY8XKyjkGOYpBzCopyEx9QICy2gTQLyKiX9NCQ664INupvOfYTtPFHxVag2nfdBNyQaJ1iw3beew.XILf0J2gBWX6WnAwAnoQsIpd5ZBcuFPzQk63LQ7kZk0AM9Ps3cIrH9ZnqORKih.351DIbZGzgV2bIm0ZoZ1Dq0zifJrb5UYSbyvSzy5P7Pmnyl5fhVwvD7h0t9P7vNvItRTFv+jHvCZhcLyt7fM5XyDnkaJn8g5jdpMiAcwLIZJmKna1Pm3C9nV1HTRWliIxtTkVXYett+yjwV4RavzhlSiz6gYGhrdfdu0zU2ltKjlpczqPSvm1bgndwnVLtAGiah8pKZQFNkM.JJZftdzX62d6a+i8r6SOOleMVun6u+IUpODJqCCi.APhnUGyur9wumvbpLoVFNdDfvYWaH0MyZ+t8lZsiwyzqcjmZEwCvwOfYdz6OPI7g9StST5FA9iwgAdLkMqKGJFVXIZjSWGYdlJv4VZgwZszUzTXUWwqaMuUJfkHzy.tGAfSR2o60DV4xPDYDDqc4Bh+shw3VDQJ8qPOjBGEVJgYkesxRgie7ip8m6EegaaegP0CNdaZvrakqX8uI3gMgKSDRUKn5HSZAkQip6cbOQil8bo3CJmVh1Y3NlItSjn2D8rfq+CWXaNBi+ZuEpRu0Ze9RlKPju2ARAbjuWANlom0Lh0+um0+Q5YsvAv8MSAz3VG0jidIbGpado6Lgtb2RaxkrybIsw2k4lGlK7VZFFpPTGo6S7iomdF9Iou4cOCMtQ48bJ51ClWsDxt4an224GywL29zyABQeeRzKaX0dwf2EuZDehiT7ZyurWSkOLxBblGO5MouNtkdbwxnyF+KtKsSIjOyk8ZGG8aN6SKiPyOlOaEh4yWgX1cEh4KVgXd9JDyWtBw7UWZL5+oBlaEnkZfg10iDWVV04jS8huNC5e.AN0gxA
```