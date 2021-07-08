---
layout: default
title: 다익스트라 알고리즘
parent: 알고리즘
nav_order: 24
permalink: /algorism/dijkstra
---
## 다익스트라 알고리즘?
{: .fs-9 }
이해하기 전에는 이름부터 강하기 때문에 어렵게 느껴질것이다. 하지만 그렇게 복잡하지는 않다.<br>
쉽게 생각하면  너비우선탐색(BFS)에서 우선순위를 정하고 해당 우선순위의 값을 계속 업데이트 치면서 이동한다고 생각하면 된다. <br>
주로 하나의 정점에서 다른 모든 정점 간의 각각 가장 짧은 거리를 구하는 문제에서 사용된다.

## 로직..
<img src="https://www.fun-coding.org/00_Images/dijkstra.png" width=300>

1. 시작노드을 기준으로 배열을 선언하여 시작부터의 각 정점 거리를 저장한다. 이떄 시작점은 0 나머지는 모두 최대값으로 저장한다
<img src="https://www.fun-coding.org/00_Images/dijkstra_initial.png">

2. 시작노드에서 인접된 노드들을 우선 순위 큐에 넣는다.이때 넣으면서 해당 노드의 거리가 배열의 저장된 거리보다 작다면 배열에 업데이트 시켜주며 우선순위 큐에 저장된다.
<img src="https://www.fun-coding.org/00_Images/dijkstra_1st.png">

3. 우선순위큐에서 가장 첫번째 노드를 추출한다. (우선순위는 가장 거리가 작은 노드) 이후 추출된 노드의 인접한 노드들 에게 현재의 추출된 노드의 거리를 더한후 우선순위 큐에 저장한다. 이를 우선순위 큐의 저장값이 없을때 까지 반복한다.
<img src="https://www.fun-coding.org/00_Images/dijkstra_2nd.png">
<img src="https://www.fun-coding.org/00_Images/dijkstra_3rd.png">
<img src="https://www.fun-coding.org/00_Images/dijkstra_3-2th.png">
<img src="https://www.fun-coding.org/00_Images/dijkstra_5th.png">



```java

import java.util.*;

public class dijkstra_Alg {

    public static void main(String[] args) throws CloneNotSupportedException{



        Node A = new Node("A");
        Node B = new Node("B");
        Node C = new Node("C");
        Node D = new Node("D");
        Node E = new Node("E");
        Node F = new Node("F");

        A.addBranch(B,8);
        A.addBranch(C,1);
        A.addBranch(D,2);
        A.addBranch(F,6);

        C.addBranch(B,5);
        C.addBranch(D,2);

        D.addBranch(E,3);
        D.addBranch(F,5);

        E.addBranch(F,1);

        F.addBranch(A,5);

        List<Node> graph = new ArrayList<>();
        graph.add(A);
        graph.add(B);
        graph.add(C);
        graph.add(D);
        graph.add(E);
        graph.add(F);

        A.distance = 0;
        System.out.println( Utill.dijkstra(graph,A));
        /** out put >>
        [A/0/[]
        , B/6/[A>C>B]
        , C/1/[A>C]
        , D/2/[A>D]
        , E/5/[A>D>E]
        , F/6/[A>F, A>D>E>F]
        ]
        **/




    }

    public static class Utill {

        public static List<Node> dijkstra (List<Node> list, Node root) throws CloneNotSupportedException{

            PriorityQueue<Node> pq = new PriorityQueue<>();
            Map<Node,Integer> temp;
            int curDis = 0;
            root.path = root.name;
            pq.add(root);

            while ( !pq.isEmpty() ) {
                Node curNode = pq.poll();
                curDis = curNode.distance;
                temp = curNode.branchs;
                String curPath = root.path;
                Iterator<Node> keys = curNode.branchs.keySet().iterator();
                while( keys.hasNext() ){
                    Node node = keys.next();
                    int nodeDis = curDis + temp.get(node);
                    if ( node.distance >= nodeDis ) {
                        String path = curNode.path + ">" + node.name;
                        list.get(list.indexOf(node)).setDistance(path,nodeDis);
                        Node que = list.get(list.indexOf(node)).clone();
                        que.distance = curDis + temp.get(node);
                        que.path = path;
                        pq.add(que);
                    }
                }
            }

            return list;
        }

    }


    public static class Node implements Comparable<Node> , Cloneable {

        String name;
        String path;
        Integer distance;
        Map<Node,Integer> branchs;
        List<String> pathList ;

        public Node(String name) {
            this.name = name;
            this.distance = Integer.MAX_VALUE - 2;
            branchs = new HashMap<>();
            pathList = new ArrayList<>();
        }

        public void addBidBranch(Node node , Integer dis , boolean isBid) {
            this.branchs.put(node,dis);
            node.branchs.put(this,dis);
        }
        public void addBranch(Node node , Integer dis ) {
            this.branchs.put(node,dis);
        }

        public void setDistance(String path , Integer dis ) {
            if ( path != null ) {
                if ( dis < this.distance) {
                    pathList.clear();
                }
                pathList.add(path);
            }
            this.distance = dis;
        }

        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (o == null || getClass() != o.getClass()) return false;
            Node node = (Node) o;
            return Objects.equals(name, node.name);
        }

        @Override
        public int compareTo(Node o) {
            return this.distance - o.distance;
        }

        @Override
        public String toString() {
            return name+"/"+distance+"/"+pathList+"\n";
        }

        @Override
        public Node clone() throws CloneNotSupportedException {
            return (Node)super.clone();
        }
    }

}
```