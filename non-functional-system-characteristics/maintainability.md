---
description: >-
  Learn about maintainability, how to measure it, and its relationship with
  reliability.
---

# Maintainability

### What is maintainability? <a href="#what-is-maintainability" id="what-is-maintainability"></a>

Besides building a system, one of the main tasks afterward is keeping the system up and running by finding and fixing bugs, adding new functionalities, keeping the system’s platform updated, and ensuring smooth system operations. One of the salient features to define such requirements of an exemplary system design is **maintainability**. We can further divide the concept of maintainability into three underlying aspects:

1. **Operability**: This is the ease with which we can ensure the system’s smooth operational running under normal circumstances and achieve normal conditions under a fault.
2. **Lucidity**: This refers to the simplicity of the code. The simpler the code base, the easier it is to understand and maintain it, and vice versa.
3. **Modifiability**: This is the capability of the system to integrate modified, new, and unforeseen features without any hassle.

**Measuring maintainability**

**Maintainability**, `M`, is the probability that the service will restore its functions within a specified time of fault occurrence. `M` measures how conveniently and swiftly the service regains its normal operating conditions.

For example, suppose a component has a defined maintainability value of 95% for half an hour. In that case, the probability of restoring the component to its fully active form in half an hour is 0.95.

Maintainability

> **Note:** Maintainability gives us insight into the system’s capability to undergo repairs and modifications while it’s operational.

We use (mean time to repair) MTTR as the metric to measure `M`.

<figure><img src="../.gitbook/assets/Screenshot 2023-08-20 at 4.42.58 AM.png" alt=""><figcaption></figcaption></figure>

In other words, MTTR is the average amount of time required to repair and restore a failed component. Our goal is to have as low a value of MTTR as possible.

#### Maintainability and reliability <a href="#maintainability-and-reliability" id="maintainability-and-reliability"></a>

Maintainability can be defined more clearly in close relation to reliability. The only difference between them is the variable of interest. Maintainability refers to `time-to-repair`, whereas reliability refers to both `time-to-repair` and the `time-to-failure`. Combining maintainability and reliability analysis can help us achieve availability, downtime, and uptime insights.
