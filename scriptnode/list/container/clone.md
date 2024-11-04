---
keywords: clone
summary:  An array of nodes that are processed simultaneously
author:   Christoph Hart
modified: 24.09.2021
parameters: 
- NumClones: The number of active clones.
- SplitSignal: The process mode for the signal
---
  
There are a lot of DSP concepts that require some sort of duplication of certain elements, for example:

- Additive synthesis
- Unisono synthesiser voices
- Cascading filters
- Feedback delay networks
- Multistage effects (phasers, etc)

which are usually implemented by duplicating a certain part of the signal path. In scriptnode you can implement them naively by copy & pasting the required nodes and connect all parameters manually. However this is super tedious and you don't have the ability to dynamically change the amount of duplicates without getting into complicated hacks.

The **container.clone** node offers a quick and intuitive way to implement those DSP applications. It's supposed to be populated with nodes that can be duplicated. There are a few requirements for the child nodes:

1. They must have the same structure (hence the name **clone**)
2. They immediate child node must be a container (this is required for the C++ code generation)
3. They cannot have any modulation / parameter connections to anywhere outside of the clone (as well as with each other).
4. Their parameters (and complex data) will be synced.

There are a few convenient functions available in the toolbar of this node:

- delete all clones so that there is only one child
- duplicate the first clone to an arbitrary amount
- hide the clones - you don't want to see 128 oscillators...

The clone node has two parameters: **NumClones** and **SplitSignal**. NumClones will define the number of active clones and will always have the parameter range **1 ... number child nodes**. The second parameter will determine how the signal will be processed and can have three values:

| Value | Description | Typical application |
| -- | --- | --- |
| **Serial** | processes the clones serially (just like a container.chain). | multistage fx, cascaded filters |
| **Split** | processes the clones in parallel without the signal input and adds their output to the signal | any form of synthesis (that doesn't require audio input) |
| **Copy** | Copies the input signal and processes each clone, then adds their output to the signal | feedback delay networks |

> Here's an example of a delay effect offering serial and parallel processing:
```snippet
ScriptNode1068.3oc6Y0zaSCCF1oE2tOX7gPHNvMthTETDbsczxGSZspREgfCHlI0aMrj3JmD5JGP.23DWFm4LR7qfqbBPfPB9QLNvANf.6D2T67wVSWqXHsboJ1u194884wu90oMIcv.shWGo6RnCZgb6BzNITmX6hLrwzR5cY+BVoNP6rParaeBcy66foF3VHJxzDa1hRzAWcPOjiCtCPSKeSjEd2stIaMqQLIdTfFTCvdpQrrv1t.sbPP6tj9bysvtXpCaFyokmMrdXpqA1AvZP71.l4bfcT3JN2l2qNxDbajoGlOH+Ugad9l9tXAtoyA88mq.1C+Mt+DNxcG7SBTyGB0bJPcq0QcvTUndBenRIlkD8lDREckIjlKBRONromkDMH.KjEXYOQLt.rAG3BalCtJKThn.P69Ft5cuEhtA10eQjafGdpQrsw5tFDaG0WEwhUX9EDZ4YBBgBuohvfkBLIyWA97cwTlPIOlydCei4TMLrE927GAHdZf1JRa6TosKtWaiGqXW6Mw8CnQYK4QtgKb3zT3Yup1hK+sJ0wqi7LcisjK64RrPt9DdfFWnWVBpaRrw2WG8.Srpn4zghFYShqbTmh8kPWUQrH7lHpEw1PmYKqCOSDmTFILRlolC9vNXSz.UtZQXcdi2xvJJekWhuJFmu1oRb95BUiyWLNLU9ZQ91hZ7njCHJ2TMYNamJf+A5ne+le7wF24KioNZ2CbSG.dCjkEJVPCjF.UnVYg9IDpz0Iz9HZmxpZ8yDQqKrJA0dr4IKB9LnhmGRw5XiGgUkwK.uNF24AH8MinhycnJdrEIolMrHzomoga5myGzcbUwvAlIwPxme6WvP4ItTixyfRMFUUjlDTCNgUAmK.Yg0tk3sGGfA1uGnKmRD5e94pC6LM0cJ4Cij6QPMWZhI0KMSIUg9atfHfe5scAo9cmzNffd16pzEYPXHX5TydxEBGVURWCyNYOvqNbYmZ9Bau81+Y1sspX.kmcHWDV+Zqt7cmoRE4aEM5DpHPkR7bMr2nzvtiC0QC8.c5.oCaCmoObtu8qm79um8JsCKKUIZsDqUmdkDckTB.QWSdfJWlKSq5KqNVAp0NU8OIxatpgE63uXSShQIV6YupfLiI4B9CmpVq8h25c9mWMyrWAnC1NRdjiEpz86KN4IFTVntD1PJUd3P7Ft8Q8HmzeQxSNlblsK9+TlQwggW9fepwEFRPkOL233r6ZdQVtxGlb7+wjiE8yyU9.R1QoMeia5wI8lzAeWyCl2hFjwa2uDrM+JrsM1vdT9srdCHkSL8+foGd+vTteX5BviHK.CBk9guoOuO15uw6ajO7NfJewJUcEHpuImIZ5kq6OCdcKdttHC8d6SGT8ScuG+W.BGT5fxounTdnq8x284J6O+K1G2b7bQHrgwVyXu6ou6mece5cg+EWI6U+E.3YEUV
```

The default mode is the copy mode, however you can save a few CPU cycles for synthesis applications if you switch to the **Split** mode.

The synchronisation of all clone parameters results in a severe limitation: For almost every real world use case you will need to change certain parameters of the cloned nodes. An additive synthesiser for example will need to use a different frequencies and amplitudes for representing each harmonic, a unisono saw needs to be detuned and spread across the stereo field etc.  
This is where the two nodes control.clone_cable and control.clone_pack come in handy as they allow to send different parameter values to each clone.

> For a detailed explanation of these nodes take a look here and here.



