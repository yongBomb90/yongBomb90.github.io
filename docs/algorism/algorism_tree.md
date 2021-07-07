---
layout: default
title: 트리구조?
parent: 알고리즘
nav_order: 3
permalink: /algorism/intro
---
## 트리구조? 이진트리구조?
{: .fs-9 }
 비선형 데이터 구조로 **Node와 Branch를 이용해서, 사이클을 이루지 않도록 구성한 데이터 구조**를 트리라고 부른다.
 즉, 하나의 데이터가 하나의 노드쪽로 이동이 가능하도록 구현한 구조를 트리 구조라한다. 이는 데이터 검색같은 상황에서 가장 많이 쓰이는 구조이다.
 이러한 트리구조중 가장 많이 쓰이는 구조가 이진트리 구조이다. <br>
 <br>
 **이진트리란 각각의 노드가 두개의 자식을 가지고 있는 구조를 말한다.**
 <br>
 
 ![](/assets/images/binary-search-tree-insertion-animation.gif)

---

## 이진트리탐색?
 이진 트리의 모든 노드를 방문하는 것 혹은 방문하여 어떤 작업을 하는 것을 이진 트리 탐색이라고 한다. 이진 트리 탐색의 방법에는 여러 가지가 있으며, 다음의 방법들이 유명하다.
 <div class="code-example" markdown="1">
 ![](/assets/images/tree.png)

 1. **in-order(중위 순회)** : 왼쪽 자식노드(L), 내 노드(P), 오른쪽 자식노드(R) 순서로 방문한다.
    > 검색순서 : A, B, C, D, E, F, G, H, I (left, root, right)
 2. **pre-order(전위 순회)** : 내 노드(P), 왼쪽 자식노드(L), 오른쪽 자식노드(R) 순서로 방문한다.
    > 검색순서 : F, B, A, D, C, E, G, I, H (root, left, right)
 3. **post-order(후위 순회)** : 왼쪽 자식노드(L), 오른쪽 자식노드(R), 내 노드(P) 순서로 방문한다.
    > 검색순서 : A, C, E, D, B, H, I, G, F (left, right, root)
 4. **level-order(레벨 순회)** : 내 노드로부터 깊이 N인 노드들 순서로 방문한다.(N: 나(트리)의 깊이)
    > 검색순서 : F, B, G, A, D, I, C, E, H
 </div>
