---
layout: default
title: 너비우선탐색(BFS)와 깊이우선탐색(DFS)
parent: 알고리즘
nav_order: 23
permalink: /algorism/bfs_dfs
---
## 너비우선탐색과 깊이우선탐색?
{: .fs-9 }
- 너비우선탐색
> Breadth-First Search 라고 한다. 하나의 정점으로부터 시작하여 차례대로 모든 정점들을 한 번씩 방문하는 것으로 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법이다.
두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다. <br>

- 깊이 우선 탐색
> Depth First Search 라고 한다. 정점의 자식들을 먼저 탐색하는 방식이다. 순환 알고리즘의 형태 를 가지고 있다. <br>


---

 ![](https://www.fun-coding.org/00_Images/BFSDFS.png)

- BFS 방식: A - B - C - D - G - H - I - E - F - J 
  >  한 단계씩 내려가면서, 해당 노드와 같은 레벨에 있는 노드들 (형제 노드들)을 먼저 순회함
- DFS 방식: A - B - D - E - F - C - G - H - I - J 
  >  한 노드의 자식을 타고 끝까지 순회한 후, 다시 돌아와서 다른 형제들의 자식을 타고 내려가며 순화함


---
## 아래와 같이 구현 가능하다

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Objects;

/**
 * 그래프 노드 클래스
 *   - 넓이 , 깊이 우선 검색시 사용
 */
public class graph {

    LinkedList<node> nodes;

    public static LinkedList<node> bfs(node root) {

        LinkedList<node> checkList = new LinkedList<>();
        LinkedList<node> brc = new LinkedList<>();
        brc = root.branchs;
        checkList.add(root);
        root.check = true;
        while ( !brc.isEmpty() ) {
            node nd = brc.pop();
            if (!nd.check) {
                checkList.add(nd);
                brc.addAll(nd.branchs);
            }
            nd.check = true;
        }
        return checkList;
    }

    public static LinkedList<node> dfs(node root) {

        LinkedList<node> checkList = new LinkedList<>();
        LinkedList<node> brc = new LinkedList<>();
        brc = root.branchs;
        checkList.add(root);
        root.check = true;
        while ( !brc.isEmpty() ) {
            node nd = brc.removeLast();
            if (!nd.check) {
                checkList.add(nd);
                brc.addAll(nd.branchs);
            }
            nd.check = true;
        }
        return checkList;
    }
    static class  node {
            String name; //해당 노드의 명
            int cost;  // 코스트
            LinkedList<node> branchs; // 인접 노드
            boolean check; // 검색 여부

            // 생성자 함수 해당 명과 코스트처리
            public node(String name, int cost) {
                this.name = name;
                this.cost = cost;
                check = false;
                branchs = new LinkedList<>();
            }

            // 브런치 추가
            public void addBranch(node... nodes  ){
                for ( node nd : nodes) {
                    if ( !branchs.contains(nd) ) {
                        branchs.add(nd);
                        nd.branchs.add(this);
                    }
                }
            }


            // 브런치 삭제
            public void removeBranch(node node){
                if ( branchs.contains(node) ) {
                    branchs.remove( branchs.indexOf(node) );
                    node.branchs.remove( node.branchs.indexOf(this) );
                }
            }

            // 큐데이터 불러오기
            public node queueGet(){
                return branchs.pop();
            }

            // 스택데이터 불러오기
            public node stackGet(){
                return branchs.removeLast();
            }

            // 같은 명일시 같은 노드로 본다
            @Override
            public boolean equals(Object o) {
                if (this == o) return true;
                if (o == null || getClass() != o.getClass()) return false;
                node node = (node) o;
                return Objects.equals(name, node.name);
            }

        @Override
        public String toString() {
            return "{" + name  +
                    "," + cost +
                    '}';
        }
    }

    public static void main(String[] args) {
        node A = new node("A" , 0);
        node B = new node("B" , 0);
        node C = new node("C" , 0);
        node D = new node("D" , 0);
        node E = new node("E" , 0);
        node F = new node("F" , 0);
        node G = new node("G" , 0);
        node H = new node("H" , 0);
        node I = new node("I" , 0);
        node J = new node("J" , 0);

        A.addBranch(B,C);
        B.addBranch(D);
        C.addBranch(G,H,I);
        D.addBranch(E,F);
        I.addBranch(J);

        /**넓이우선
        List bfsRes =   bfs(A);
        System.out.println(bfsRes);
        //out put >> [{A,0}, {B,0}, {C,0}, {D,0}, {G,0}, {H,0}, {I,0}, {E,0}, {F,0}, {J,0}]
        **/
        /**깊이우선
        List dfsRes =   dfs(A);
        System.out.println(dfsRes);
        //out put >> [{A,0}, {C,0}, {I,0}, {J,0}, {H,0}, {G,0}, {B,0}, {D,0}, {F,0}, {E,0}]
        **/

    }
    

}

```
