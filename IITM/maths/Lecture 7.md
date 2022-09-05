# Relations
## Identity Relation 
It is when the element is related to itself .
$$I = \{(a \ , \ b) \ | \ (a \ , \ b) \in  C \times C \ , a = b \}$$
It forms a set of duplicate elements like $\set{(1 \ , \ 1) \ , \ (2 \ , \ 2) \ , \ (3 \ , \ 3)}$,
where $A = \set{1,2,3}$

## Symmetric Relation
It is when the pairs are present in reverse order in the set.
If $(a \ , \ b)$ belongs to some set say $A$ i.e. $(a \ , \ b) \in A$ then,
$(b \ , \ a)$ would also belong to the same set i.e. $(b \ , \ a) \in A$

$$S = \set{(a,b) \ | \ (a,b) \in A \times A \ , \ gcd(a,b)=1}$$

It forms a set like $\set{(1,1) \ , \ (1,2) \ , \ (1,3) \ , \ (2,1) \ , \ (2,2) \ , \ (2,3) \ , \ (3,1) \ , \ (3,2) \ , \ (3,3) }$,
where $A = \set{1,2,3}$

Also a **set which has reflexive relation will also have an identity relation** as $\set{(1 \ , \ 1) \ , \ (2 \ , \ 2) \ , \ (3 \ , \ 3)}$ are present in the set above.


## Transitive Relation
It is when 2 elements are related to each other such that **a** is related to **b** and **b** is related to **c** then **a** is related to **c**.
$(a,b)$ belongs to $A$ and $(b,c)$ belongs to $A$ then $(a,c)$ should also belong to $A$.
$$T = \set{(a,b) \ | \ (a,b) \in A \times A \ , \ a<b}$$
If $a < b$ and $b < c$ then $a<c$.


## Antisymmetric Relation
It is when one pair is their , its reverse should not be in the Set.
$(a,b)$ belongs to some set $A$ then $(b,a)$ should not belong to $A$.
i.e. $(a,b) \in A$ and $a \neq b$ then $(b,a) \notin A$
$$A = \set{(a,b) \  | \ (a,b) \in \ \mathbb{R} \times \mathbb{R} \ , \ a < b}$$
## Equivalence Relations
It is when a set satisfies all the conditions for **Symmetric , Reflexive and Transitive** relations.
