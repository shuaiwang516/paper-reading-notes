### Paper pdf: http://dance.csc.ncsu.edu/papers/ICAC18.pdf

### Motivation:

Timeout bugs are commonly occured in large-scale systems, they can cause bad impact on systems such like performance degradation or even system crash. Meanwhile, timeout bugs are hard to detect due to the lack of log message or lack of correct log message[[1]](http://dance.csc.ncsu.edu/papers/IC2E18.pdf).

### Main work & Contribution:

This paper proposes an automatic timeout bug detection tool called **TScope**. TScope traces kernel level system calls and collect runtime system informations and performans bug detection based on the system call traces.

There are 4 major procedure of TScope to detect a timeout bug:

1. TScope uses LLTng to extract information of all system call during system execution
2. TScope select those timeout-related system call and filter out those unrelated ones. (There is a selection set contains all timeout-related system call manually made by authors.)
3. TScope extract the execution time of timeout-related system calls and make it vector
4. TScope performs anomaly detection based on the exeuction time vector. If the system call is anomaly and timeout-related, then claims a timeout bug found.

### Takeaway:

- TScope only cares about execution time when detecting timeout bugs and gains a pretty good detection accuracy, which means that exeuction time is a key expression of timeout bugs. So when we are dynamically tunning/updating these timeout configurations, one way of evaluation is based on the running time.
- Real-world timeout bug in the paper:
  - Hadoop-11252: misconfiguring timeout parameter

### Future Direction:

TScope can only detect timeout bugs, it still needs manual efforts to fix it. So the author propsed their 3rd paper about timeout bug on bug-fixing.

