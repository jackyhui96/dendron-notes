---
id: iejKZSSI2uXn6ap8Y4GLJ
title: Tuning
desc: ''
updated: 1643450714450
created: 1643450708282
---

### Scheduler binds
## cpu topology
```erlang
[{node,[{processor,[{core,[{thread,{logical,0}},
                           {thread,{logical,8}}]},
                    {core,[{thread,{logical,1}},{thread,{logical,9}}]},
                    {core,[{thread,{logical,2}},{thread,{logical,10}}]},
                    {core,[{thread,{logical,3}},{thread,{logical,11}}]}]}]},
 {node,[{processor,[{core,[{thread,{logical,4}},
                           {thread,{logical,12}}]},
                    {core,[{thread,{logical,5}},{thread,{logical,13}}]},
                    {core,[{thread,{logical,6}},{thread,{logical,14}}]},
                    {core,[{thread,{logical,7}},{thread,{logical,15}}]}]}]}]
```
## notes
* tested on mn2splltg539sl0
    * CPU(s):               16
    * Thread(s) per core:    2
    * Core(s) per socket:    4
    * Socket(s):             2
    * NUMA node(s):          2
    * NUMA node0 CPU(s):     0-3,8-11
    * NUMA node1 CPU(s):     4-7,12-15
* `erlang:system_info(scheduler_bindings).` to get scheduler bindings
* `erlang:system_flag(scheduler_bind_type, BindType).` to set scheduler binding type
* `erlang:system_info(cpu_topology).` to set scheduler binding type

## binding type and scheduler binding results
```erlang
thread_no_node_processor_spread
{0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15

thread_spread
{0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15}

spread
{0,4,1,5,2,6,3,7,8,12,9,13,10,14,11,15}

processor_spread
{0,4,1,5,2,6,3,7,8,12,9,13,10,14,11,15}

no_spread 
{0,8,1,9,2,10,3,11,4,12,5,13,6,14,7,15}

no_node_thread_spread
{0,1,2,3,8,9,10,11,4,5,6,7,12,13,14,15}

no_node_processor_spread
{0,1,2,3,8,9,10,11,4,5,6,7,12,13,14,15}

unbound
{unbound,unbound,unbound,unbound,unbound,unbound,unbound,
         unbound,unbound,unbound,unbound,unbound,unbound,unbound,
         unbound,unbound}
```
