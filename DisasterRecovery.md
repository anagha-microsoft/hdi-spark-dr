# HDInsight-Spark - High Availability and Disaster Recovery

[High availability](README.md#1--architectural-considerations-for-high-availability)<br>
[Disaster recovery](DisasterRecovery.md)<br>

## 2.  Architectural considerations for Disaster Recovery

### 2.0.1.  What is your SLA for Disaster Recovery?
The SLA for disaster recovery can be covered under two popular acronyms -<br>
[RTO - Recoverty Time Objective](https://en.wikipedia.org/wiki/Recovery_time_objective)<br>
The targeted duration of time and a service level within which a business process must be restored after a disaster (or disruption) in order to avoid unacceptable consequences associated with a break in business continuity.<br>
[RPO - Recovery Point Objective](https://en.wikipedia.org/wiki/Recovery_point_objective)<br>
A recovery point objective (RPO) is defined by business continuity planning. It is the maximum targeted period in which data might be lost from an IT service due to a major incident.<br><br>

The RPO and RTO requirements drive the DR architecture for your HDInsight solution.

### 2.0.2.  Options & considerations



