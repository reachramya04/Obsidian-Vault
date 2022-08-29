# Construction of Subsets and Set Comprehension


## Constructing Subsets 
$$\{ \ x \ | \ x \in \mathbb{Z} \ , \ x \ mod \ 2 = 0\}$$
The set above represents even integers and this way of representing sets is called set comprehension.

### Steps of constructing subsets through Set Comprehension
* Begin with an existing set , $\mathbb{Z}$
* Apply a condition on to each element in that set where $x \in \mathbb{Z}$ , such that $x \mod{2}=0$
* Collect all the items which satisfy that condition.

**Examples:**
* Set of odd natural numbers, $\{ \ x \ | \ x \in \mathbb{N} \ , \ x \ mod \ 2 \neq 0\}$
* Set of rationals in reduced form ,  $\{ \frac{p}{q} \ | \ p,q \in \mathbb{Z} \ , \ \gcd(p,q)=1 \}$

#### Intervals
* A set of elements between an interval/range can be represented as,
$$\{ z \ | \ z \in \mathbb{Z} \ , \ -6 \leq \ z \ \leq 6\}$$
* Intervals can be of 2 types , **Open Intervals** and **Closed Intervals**.
* Open Intervals is where the endpoints are not included in the set.
Example:
$$\{ q \ | \ q \in \mathbb{Z} \ , \ -3 < \ z \ < 8\} = (-3,8)$$

* Closed Intervals is where the endpoints are included in the set.
Example:
$$\{ q \ | \ q \in \mathbb{Z} \ , \ -3 \leq \ z \ \leq 8\} = [-3,8]$$


## Union , Intersection and Complement
### Union 
When 2 sets are combined together then its called a union , the cardinality (number of elements) of the new set is always less than or equal to the number of elements in parent sets.
$$\begin{align}
X = \{a,b,c,d \} \\
Y = \{ d,e,f\} \\
X \cup Y = \{a,b,c,d,e,f \}
\end{align}$$



![[Pasted image 20220829220342.png]]
