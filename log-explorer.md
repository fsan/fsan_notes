#  Log explorer
https://github.com/fsan/log-explorer

## What

The idea is develop a tool capable of getting a set of log messages, organizing them in a smart way and create correlated events.

## How

Original idea is to get messages and learn which part of the messages are related to each other to determine blocks of actions that can be analysed.


## Questions trying to answer
- Can we identify important events leading to failures automatically ?
- Can we generate tags for blocks of events automatically (no training data) ?
- Can we generate a state machine from the logs?
- Can we correlate two different logs by comparing the state machines ?


## Sample
```
input:

[2022-07-24 01:01:01] INFO: Program start up
[2022-07-24 01:01:01] INFO: Listening on port 8086
[2022-07-24 01:01:01] INFO: Received request from 102.32.55.188
[2022-07-24 01:01:01] INFO: Received request from 104.23.45.123
[2022-07-24 01:01:01] WARNING: Failed to obtain resource from store. Try #1
[2022-07-24 01:01:01] INFO: Received request from 104.23.45.123
[2022-07-24 01:01:01] WARNING: Failed to obtain resource from store. Try #2
[2022-07-24 01:01:01] INFO: Received request from 102.32.55.188
[2022-07-24 01:01:01] INFO: Received request from 104.23.45.123
[2022-07-24 01:01:01] WARNING: Failed to obtain resource from store. Try #3
[2022-07-24 01:01:01] INFO: Received request from 101.21.12.123
[2022-07-24 01:01:01] FATAL: store resource was not allocated. exiting...
```

```
start up (state 1) -> listening (state 1) -> request received (state 2)
                             | ^----------------------------|
      v--------------------------------v
resource failure (state 3) -> fatal error (state 4)
```


## Plan

- Is there any log dataset ?
    - https://datasetsearch.research.google.com/search?query=Server%20logs&docid=L2cvMTFwNjVoaGJiMQ%3D%3D
    - https://github.com/logpai/loghub
    - 


- scikit learn test with knn ?
* done
    *  using  into a pca(2) allows this to be plotted in a 2d graph
        *  ![logs-explorer-pca2-knn.png](logs-explorer-pca2-knn-static.png)
        *
        
      


- can we make a video sequence of that ?
Yes it seems
[writer_test.mp4](../../workspace/log-expl/writer_test.mp4)
not sure what this visualization means.

probably it woudl be nicer to clean up the logs messages and maybe structure them in a more analyzable format.
and test with other logs

- can we use Knn over sequence of messages instead?
- can we predict if a log mesasge was unexpected ? (a transition from state A-B is not likely?)