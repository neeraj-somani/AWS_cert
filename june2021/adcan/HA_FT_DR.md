# High Availability (HA), Fault-Tolerance (FT) and Disaster Recover (DR) 

### HA
- aims to ensure an agreed level of operational performance, usually uptime, for a higher than normal period.
  - HA is not aiming to stop failure
  - instead, its a design when system fails, its components can be replaced/fixed as quickly as possible
  - often, by using some way of automation
  - HA is not about User experience
  - HA is maximizing system's online time as much as possible
  - for HA, user disruption, while not being ideal, is okay. becoz HA is all about minimizing outage.
  - HA is all about keeping system operations
  - its about fast and automatic recovery of issues.
  - it comes with its own cost as a side effect
 
 ### Fault Tolerance (FT)
- its the property that enables a system to continue operating properly in the event of failure of some (one or more faults within) of its components, without major impacting to customer.
- FT designs in such a way that even in case of disruption, system should operate properly.
- example, system should be connected to 2 backend server (active-active) all the time
- on the other side, HA could use (active - passive) combination
- FT is not a failover configuration
- this cost more and very complicated
 
### Disaster Recovery (DR)
- its a set of policies, tools and procedures to enable the recovery or continuation of vital technology infrastructure and systems following a natural or human-induced disaster.
- this comes when HA and FT can't be an option
- example, natural calamity, builing catches fire, flood or explodes
- DR should be pre-planned in advance everything

