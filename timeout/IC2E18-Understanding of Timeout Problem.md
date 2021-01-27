### Main work:

This paper studied on real-world timeout bugs and answered 3 research questions, which are (1) What's the root causes of timeout bugs? (2) What impact can timeout bugs impose to systems? (3) How are timeout bugs diagnosed?

### Motivation:

The motivation of this paper is that timeout is a commonly used failure handling mechanisms, however, modern cloud systems lack proper configuration and handling of these timeout events and often causes unknown bugs. This paper conducts a research study on those timeout bugs.

### Contribution:

- This paper concludes **5 different root causes** of timeout bugs, they are:
  (1)**Misued timeout value**: misconfigure a timeout value
  (2)**Missing timeout checking**: Operation lacks of timeout mechanism (e.g. Network connection needs timeout to close it if network hangs a long time.)
  (3)**Improper timeout handling**: a timeout event is handling by inproper retries or aborts
  (4)**Unnecessary timeout**
  (5)**Clock drifting**: asynchronous clocks caused timeout

- Paper shows impact of the timeout bugs, result shows that timeout bugs have severe result on the both performance and reliability of the system.
- Paper also propsed that timeout bugs are hard to detect due to the lack of correct ERROR log message (Either no log message or wrong error message).

### Takeaway:

- There are 2 root causes which are related to my research, they are (1)misused timeout value and (2)improper timeout handling.
  For (1)misused timeout vlaue, paper also proposed that stale timeout value is not good enough. It should update during the system execution. But the paper doesn't go deeper into it.
  As for (2)improper timeout handling, it includes insufficient/excessive retries, incorrect retry, which all related to our project. Current handling logics are all static, which may not be suitable for all kinds of environments. So if we could make the handling logic more dynamic, we could update during the system exeuction and fit different environments.

- There are several good real-world issues in the paper which may also benefits my research:
  - HDFS-6166, HBase-13647, HBase-6684, HBase-3273, Mapreduce-6263: misconfiguring a timeout value.
  - HBase-3295, HDFS-4404, Mapreduce-5616: Insufficient/excessive retries when timeout.
  - HDFS-4646: Hardcoding timeout as 0 makes bug
  - HBase-16556: Incorrectly reused timeout value
  - Zookepper-593: client timeout value needs to synchornize with server timeout during execution.

### Future Direction:

After this paper, the authors published their 2nd and 3rd paper, which are about timeout bug diagnosis (TScope) and timeout bug auto-fixing (TFix).

