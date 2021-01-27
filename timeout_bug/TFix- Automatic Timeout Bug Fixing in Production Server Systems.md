### Paper pdf: http://dance.csc.ncsu.edu/papers/ICDCS19.pdf

### Motivation:

This paper is a continuous work on the timeout bug. The 1st and 2nd paper respectviely studies the timeout bugs and proposes an automatic tools for timeout bug detection. This paper is mainly focuses on fixing timeout bugs.

### Main work:

This paper proposes a timeout bug fixing tool called TFix. 

There are 5 major components of TFix:

1. Use TScope to check whether there is a timeout bug
2. Check whether the timeout bug is caused by misused timeout value
3. Check which function is buggy. Use Dapper to extract execution time and frequency of all the functions invoked when the bug happens.
4. Use static taint analysis to identify which timeout varaible is misused.
5. Recommend a proper timeout value based on the normal exeuction round.

### Takeaway:

- One drawback of exisitng handling logics is that they lacks correct/useful log message when bug occurs, which makes developers/users feel difficult to find the root cause.
- TFix's recommendation strategy is like this: 
  - If timeout value is too small, increase the value 2 times
  - If timeout value is too large, set the value to the largest normal exeuction time.
- **Some developers even don't know the right value for the patches to fix the bug.** **So it's really hard for human to do the value setting job, which means our dynamically tuning direction is valuable.**

### Constrains and limitations:

- TFix can only fix timeout bugs that caused by misused timeout value. There are also other 4 types of timeout bugs which TFix can't handle.
- TFix can fix the timtout bug, but it still needs users to reset the timeout value and restart the system, which is also expensive. If we can impelment our dynamically tunning solution then we can beat TFix at this point. 
- TFix needs to assume that the timeout affected function is invoked before the timeout bug is triggered. TFix does the value recommendation based on at least one normal execution time of the affected function. If the bug occurs at the first round then there is no way for TFix to handle it. What's more, TFix's recommendation value is also static, which can't fit all kinds of environment. (This is also proposed by authors)

### Future Direction:

Authors next step is to do the value prediction. But this direction can only solve the 3rd limitation that I propose above, not useful for the first 2.

