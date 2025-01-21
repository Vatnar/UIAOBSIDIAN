En variabel eller abstrakt datatype brukt for å kontrollere en common ressurs for flere tråder og unngå [[critical sections]]. 

A useful way to think of a semaphore as used in a real-world system is as a record of how many units of a particular resource are available, coupled with operations to adjust that record _safely_ (i.e., to avoid [race conditions](https://www.wikiwand.com/en/articles/Race_condition "Race condition")) as units are acquired or become free, and, if necessary, wait until a unit of the resource becomes available.

Read:
https://www.geeksforgeeks.org/mutex-vs-semaphore/
