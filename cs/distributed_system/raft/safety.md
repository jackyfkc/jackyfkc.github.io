Safety
---
Once a log entry has been applied to a state machine, no other state machine must apply a different value for that log entry.


**Raft safety property**

* If a leader has decided that a log entry is committed, that entry will be present in the logs of all future leaders


**This guarantees the safety requirement**

* Leaders never overwrite entries in their logs

* Only entries in the leader's log can be committed

* Entries must be committed before applying to state machine

