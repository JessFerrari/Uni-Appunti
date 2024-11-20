---
Subject: "[[Indice - Information Retrieval|IR]]"
Super Topic: "[[Indexing a document]]"
tags:
  - IR
  - inverted_index
Creation: 2024-10-24
---
To answer a query  we don't need all document but the top thousand to maximize the user satisfaction. 
We want to improve the efficiency in order to receive a god number of documents.

The goal is: for a  query and a parameter k, find the *exact Top-k* scored OR result.


# Min-Heap
The easiest possible strategy is answer he OR query, riceve all results (to many) and then compute the exact top-k; but it's very inefficient.
To compute the exact top-k with this strategy, we use a [[Min-Heap]] because we can access easily to the min value, that is in the  root.  It's very inefficient because the cost is proportional to the number of postings in the posting list of the query terms.
The threshold $\tau$ is the smallest score of the heap and if the value $s<\tau$ we can ignore it.

When we see a new result we can compare it with the root. 
if it's grater than the root it means that is more relevant. Than we insert the new element in the tree. if in the tree are already $k$ elements we compere the new element and re sort the tree.
Else, if it's less than the root we simply don't insert it.
Then when documents are finish we can select the top-k. In the leaves there are the most relevant documents.

Example:
	Top-3 in a Min-heap.
	We start with a threshold $\tau=0$ and we have 7 document with different values:
		2.1, 3.1, 2.3, 2.5, 1.5, 3.0, 0.5
	For the first element we just use it as root of the tree and change the $\tau=2.1$
	Then arrive the second, 3.1, that is grater than 2.1, so in will be a child : $(2.1(3.1))$
	Then we take he third, 2.3. It's greater then 2.1 but is less then 3.1 so it will be the dx child: $(2.1(2.3, 3.1))$ 
	![[Pasted image 20241026113735.png]]
	Then the fourth is 2.5 that is greater then 2.1 and less than 2.3. We want that in our tree there are only three elements (the top 3 elements) so the dx child become the new root, 2.5<3.1, and the dx child is 2.5 and the sx is 3.1 . Also we change the threshold $\tau=2.3$
	Min-heap : $(2.3 (2.5, 3,1))$
	The fifth is 1.5<2.3 and we skip it.
	The sixth is 3.0>2.3, 3.0>2.5 but is less then 3.1 so we re-change the root ad the threshold: $\tau=2.5$ and Min-heap = $(2.5 (3.0, 3.1))$
	The last element to compute is 0.5 that is less than tau so w skip it.
 
The time for each operation is logarithmic over the number of elements stored in the heap.
To build the heap the time complexity is : $\Theta(n\log k)$, where n is the total number of documents and $k$ is the number of stored documents.

### Query OR top-1

![[Pasted image 20241026114436.png]]
We take the pointers to the document with the smallest document ID, (10, 0.5) and move forward to (13, 0.9).
We don't change $\tau$ because 0.5<2.1 .
Now we sum the values for the same documents and we have:
- (11, 0.3)
- (13, 1.4)
- (15, 2.5)

We now move the pointer to (11, 03) to (12, 0.1), 0.3<2.1 so we skip it 
The values are:
- (12, 0.1)
- (13, 1.4)
- (15, 2.5)

now move (12, 0.1) to (13, 0.1), 0.1<2.1 so skip it and values are:
- (13, 1.5)
- (15, 2.5)

The sum of all values of 13 is smallest than 2.1 so we skip all 13 :
![[Pasted image 20241026115613.png]]
Now we compute the values for documents and we have:
- 15, 3.7
- 25, 0.8

3.7>2.1 so we change the Top-1 document and the $\tau$ in :
$d=15$ and $\tau=3.7$ 

For this algorithm we touch every single posting.


# WAND ( Weak AND)

WAND is a dynamic pruning strategy which allows to skip more docIds than the min-heap.
It guaranteed to compute the exact Top-k result but skips many postings.

Given the current threshold $\tau$, skip documents that are guaranteed to have a score $s<\tau$.
For each posting list, store the upper bound (UB) that is the largest score in the posting list.

The UBs allow to approximate the true score of a document for the query and do not touch all the documents.

Example: we have 4 terms and so 4 posting list $Q= t_{1}, t_{2}, t_{3}, t_{4}$ and we don't really calculate the true score $s(Q,d)=s(t_{1},d)+s(t_{2},d)+s(t_{3},d)+s(t_{4},d)$ but just approximate it with upper bounds, such as $s(Q,d)\leq UB(t_{1})+UB(t_{2})+s(t_{3},d)+s(t_{4},d)$

Approximating the score we can use the upper bounds safely without skipping documents that are in the top-k.

 
Moving  a pointer is very expensive so is best do reasoning. 


Algorithm:
1. Compute the UB for each posting list
2. Sorting by the current docID (to do every time after the move of a pointer)
3. Take the first and reasoning on the values: Is the $\tau<s(Q,d)$, $s(Q,d)$ is an approximation and it is $\leq$ then the sum of UBs (see the example)

Example:
Calculate the UBs
![[Pasted image 20241026124548.png]]
Sort by current docID
![[Pasted image 20241026124628.png]]
Take the first: language->10, 0.5
the question is :
$\tau=2.1<?? s(Q,10)\leq s(\text{language},10)=0.5$

All pointer point to a docID bigger than 10, so 10 is only in the first posting list. For this we can safely say that the score of 10 for others terms is 0.
So we can say:
$\tau=2.1<s(Q,10)=s(\text{language,10}=0.5)$ 
so we can skip it.

now we consider the next term :  "best", (11, 0.3), and we ask:
$\tau=2.1<?? s(Q,11)\leq UB(\text{language})+s(\text{best},11)=1.1+0.3=1.4$
NO!! 1.4<2.1 o we can skip it.

We go to term "programming", (13, 0.5), and we ask:
$\tau=2.1<?? s(Q,11)\leq UB(\text{language})+UB(\text{best})+s(\text{programming}, 13)=1.1+0.3+0.5=1.9$
NO!! 1.9<2.1, skip it

now we go to term "rust", (15, 2.5) and we ask:
$\tau=2.1<?? s(Q,11)\leq UB(\text{language})+UB(\text{best})+UB(\text{programming})+s(\text{rust},15)=1.1+0.3+0.5+2.5=4.9$
YESS 4.9>2.1 so we have to evaluate the document 15.
So now we have to evaluate 15.

1) we move pointers with [[Basic operation on posting list|nextGEQ_t(15)]]
2) evaluate the document 15
3) update $\tau$ and $d$

![[Pasted image 20241026141241.png]]

$s(Q,15)=s(t_{1},15)+s(t_{2},15)+s(t_{3},15)+s(t_{4},15)=0+0.2+1.0+2.5=3.7$
$d=15$ and $\tau=3.7$

If we have to go on we need to re-sorting the posting lists.

# MaxScore
 MaxScore is another dynamic pruning strategy. It guarantees to compute the Exact Top-k results but skips many postings.
-> idea: given the current threshold $\tau$, split the posting list into essential and non essential.
for non essential we are meaning the lists with the smaller upper bound UB such that  $\tau>UBs$. We can ignore the non essential list.
During the algorithm the essential group is decreasing because $\tau$ is increasing.
MaxScore is good when the query is long.

Example:

![[Pasted image 20241026142016.png]]
For first we have to sort by the UBs![[Pasted image 20241026142418.png]]

We sum the smallest UB with the one before so : $UB(t_{4})+UB(t_{3})=1.3<\tau=2.1$
If we add also $UB(t_{2})$ we obtain $1.3+1.1=2.4>\tau=2.1$ so $t_{2}$ isn't in the non-essential group.
![[Pasted image 20241026142949.png]]
Now we touch only 2 posting list:
Let's start from the smallest docID, the 10 in $t_{2}$, and evaluate in the same way of DaaT OR. 
We estimate it we the UBs of non essential list plus the evaluate of essentials.
Is $\tau=2.1<s(Q,10)\leq UB(t_{4})+UB(t_{3})+s(t_{2},10)+s(t_{1},10)=0.3+1.0+0.5+0=1.8$?
NO, so we can skip it.

We now proceed with the pointers and we point in $t_{2}$ the $(13, 0.9)$.
We do the same as before:
$\tau=2.1<s(Q,13)\leq UB(t_{4})+UB(t_{3})+s(t_{2},13)+s(t_{1},13)=0.3+1.0+0.9+0=2.2$
YES! so we have to fully evaluate 13. we only move the last because it the only that point to a docID smaller than 13, and then evaluate the score = $0.9+0.5+0.1=1.5<\tau$ so we don't update. 
![[Pasted image 20241026144339.png]]

Now we move the $t_{2}$ pointer ![[Pasted image 20241026144612.png]]
and evaluate the smallest docID : (15, 2.5) in $t_{1}$.

$\tau=2.1<s(Q,15)\leq UB({t_{4}})+UB(t_{3})+s(t_{2},15)+s(t_{1},15)=0.3+1.0+0+2.5=3.8$
That's true so we fully evaluate 15:

move all pointers to 15 with $\text{nextGEQ}_{t}(15)$ and than evaluate the total score = $2.5+0+1.0+0.2=3.7<\tau=2.1$ so now we can update $\tau$ and the top-1 document $d=15$

# a real example
![[Pasted image 20241026145445.png]]