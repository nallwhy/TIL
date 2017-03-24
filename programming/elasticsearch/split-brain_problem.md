## HOW TO AVOID THE SPLIT-BRAIN PROBLEM IN ELASTICSEARCH

http://blog.trifork.com/2013/10/24/how-to-avoid-the-split-brain-problem-in-elasticsearch/

cluster node 간의 연결에 문제가 생겼을 때 투표를 통해 새로운 master 를 선출하는데, 이를 방지하기 위해 N/2 + 1 개의 투표를 받았을 때 master 가 되도록 해야한다는 내용.

문제를 어느정도 해결할 수는 있지만 완벽한 해결책은 되지 않는다는 얘기도 있다.