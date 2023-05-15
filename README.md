Collection of tools and resources to detect and remove Snake malware

## network detection
rumor has it these rules are pretty bad (https://twitter.com/EcOzurie/status/1656376989006061574)
```

James
@EcOzurie
Unfortunately I must advise against using the CISA Suricata rules for Snake (http & http2), they're incredibly vague and will absolutely bury you in FPs from the moment they're activated.

We're looking at alternatives.
```

## host-detection
snake-finder.py 
defines a class called snake that inherits from the PluginInterface. It has the following key components: 

get_requirements: This method specifies the requirements for the plugin to run, including the kernel module, and the versions of pslist and vadinfo components. 

list_injections: This method is responsible for identifying injected components in the memory of a given process. It first checks if the process has a valid address, and then iterates through the process's Virtual Address Descriptor (VAD) tree to find memory regions with specific attributes, like having "PAGE_EXECUTE_READWRITE" protection. It then filters these regions further based on the presence of specific byte patterns, which are indicative of the Snake malware. 

_generator: This method iterates through a list of processes, calling list_injections for each process to find injected components. If an injected component is found, it yields relevant information, such as the process ID, process name, memory address, size, and protection attributes. 

run: This method sets up the output format and calls the _generator method with a list of processes retrieved using the pslist.PsList.list_processes method.

The source code to snake-finder and the Suricata rules were published by the FBI in a May 9th, 2023 report
source: https://www.cisa.gov/sites/default/files/2023-05/aa23-129a_snake_malware_2.pdf


### Sonnet of the Tamed Serpent
In Ryazan's cold and Moscow's frosty air,
The Russian FSB did build a Snake,
A tool of stealth, espionage affair,
With power vast, it left a chilling wake.
Uroburos, the name it had acquired,
It slithered through the networks, silent, sly,
Through NATO secrets, information mired,
And on the world's stage, it would not shy.
But lo, a flaw! A weak encryption key,
Discovered by the agencies that pry,
Operation MEDUSA, swift and free,
Did vanquish Snake with PERSEUS, thereby.
Alas, the Snake is tamed, yet vigilance remains,
For cyber threats will always stake their claims