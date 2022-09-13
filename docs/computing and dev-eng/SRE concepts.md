# SRE Concepts

**SLI (Service Level Indicator)**: a metric used to define, track and evaluate service quality/reliability. There are different SLIs, depending on the type of service, e.g., uptime percentage, latency percentage, etc. Typical SLI is defined as a ratio GoodService / TotalServiceRequests.

**Goal**: a particular target or threshold defined for an SLI to differentiate a good level of service from the bad. For example, given a particular SLI, a goal “>90%” for that SLI states that the lower threshold of acceptability is 90% with respect to that SLI.

**SLO (Service Level Objective)**: A formal target for service performance/reliability. SLO consists of a criterion that specifies some service quality dimension, such as latency, uptime, etc., and a corresponding SLI goal, e.g., “latency < 100 ms, p90” (90% or more of service requests must be completed within 100 milliseconds). The purpose of SLO is to associate an SLI with its goal.

**SLA (Service Level Agreement)**: A formal agreement between the service provider and the user of the service, specifying commitments of the service provider with respect to the service quality. SLA describes specific SLOs and the periods for which the measurement of the metric is being made, to which the service provider has committed, and the potential consequences for not meeting these SLOs, such as reimbursements to the client or some other measures.
