# [Medium 950. Reveal Cards In Increasing Order](https://leetcode.com/problems/reveal-cards-in-increasing-order/)

## Problem:
Input: [17,13,11,2,3,5,7]  
Output: [2,13,3,11,5,17,7]  
Explanation:   
We get the deck in the order [17,13,11,2,3,5,7] (this order doesn't matter), and reorder it.  
After reordering, the deck starts as [2,13,3,11,5,17,7], where 2 is the top of the deck.  
We reveal 2, and move 13 to the bottom.  The deck is now [3,11,5,17,7,13].    
We reveal 3, and move 11 to the bottom.  The deck is now [5,17,7,13,11].  
We reveal 5, and move 17 to the bottom.  The deck is now [7,13,11,17].  
We reveal 7, and move 13 to the bottom.  The deck is now [11,17,13].  
We reveal 11, and move 17 to the bottom.  The deck is now [13,17].  
We reveal 13, and move 17 to the bottom.  The deck is now [17].  
We reveal 17.  
Since all the cards revealed are in increasing order, the answer is correct.  

## Thoughts:
  
![](https://assets.leetcode.com/users/votrubac/image_1543911256.png "Thanks to votrubac")

+ First approach
+ sort the array; create a new result array;
+ add the smaller half in odd plot of result;
+ add the bigger half into the first empty plot, then the third, then ...;
+ return result;
- **The hardest part is to make sure insert actions follows the odd sequence. Here the programm uses counters in for loop by adding a constant each time the result reaches a empty plot and recount every two empty plot. Also p %= result.size() makes sure that when the p counter exceeds size(), result[p] can still point to the start of the array. (We need p to keep track of result while using i to keep track of deck, and using j to determine if the empty spot is okay to insert.**

* Second Approach
* same idea, but this time uses a list and list iterator to skip even empty plots.


## Code:
```c++
class Solution {
public:
    vector<int> deckRevealedIncreasing(vector<int>& deck) {
        sort(begin(deck), end(deck));
        vector<int> result(deck.size(),0);
        result[0] = deck[0];
        
        for(int i=1, p=0; i<deck.size(); i++){
            for(int j=0; j<2; p %= result.size(), j += (result[p] == 0 ? 1 : 0)){
                p++;
            }
            result[p] = deck[i];
        }
        return result;
    }
};
```
```c++
class Solution {
public:
    vector<int> deckRevealedIncreasing(vector<int>& deck) {
        sort(begin(deck), end(deck));
        list<int> l(deck.size());
        iota(begin(l), end(l), 0);    //iota fills the range from arg1 to arg2 starting at arg3 l = {0,1,2,3...}
        vector<int> res(deck.size());
        auto lp = l.begin();
        for (int i = 0, skip = 0; !l.empty(); skip = !skip) {
            if (lp == l.end()) lp = l.begin();
            if (skip) ++lp;
            else {
                res[*lp] = deck[i++]; //dereference the iterator to get the value it points to
                l.erase(lp++);
            }
        }
        return res;
    }
};
```
## reference:
(https://leetcode.com/problems/reveal-cards-in-increasing-order/discuss/201574/C%2B%2B-with-picture-skip-over-empty-spaces)
