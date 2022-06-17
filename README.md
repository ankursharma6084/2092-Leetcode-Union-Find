# 2092-Leetcode-Union-Find
2092. Find All People With Secret

Solution 1. Union Find
Sort meetings in ascending order of meeting time.

Visit the meetings happening at the same time together.

We can connect the two persons in the same meeting using a UnionFind.

Tricky point here: After traversing this batch of meetings, we reset the persons who don't know the secret by checking if he/she is connected to person 0. With UnionFind, reseting means setting id[x] = x.

In the end, we add all the persons who are connected to person 0 into the answer array.

 OJ: https://leetcode.com/problems/find-all-people-with-secret/

 Time: O(MlogM + (M + N) * logN) where `M` is the length of meetings
       Can be reduced to O(MlogM + (M + N) * alpha(N))
 Space: O(M + N). Can be reduced to O(N) if we make ppl an unordered_set.

Complexity Analysis:

Sorting takes O(MlogM) time.

Each meeting is visited and pushed into/popped out of ppl only once. For each visit, the connect/connected takes amortized O(logN) time. So, traversing all the meetings takes O(MlogN) time. Note that if we do union-by-rank, the time complexity can be reduced to O(M * alpha(N)) where alpha(N) is the inverse function of Ackermann function, and is even more efficient than logN. But in LeetCode, the difference is negligible, so I usually just use path compression for simplicity. It's definitly worth mentioning this knowledge during your interview though.

Lastly, traversing all the persons and checking connection with person 0 takes amortized O(NlogN) time.

So, overall the time complexity is amortized O(MlogM + (M + N) * logN), which can be reduced to O(MlogM + (M + N) * alpha(N)) with union-by-rank.

As for space complexity, the Union Find takes O(N) space. The ppl array takes O(M) space in the worst case, but it can be reduced to O(N) if we use unordered_set. I use vector<int> because unordered_set<int> has extra overhead which at times consumes more time/space than vector<int> in LeetCode.

So, overall the (extra) space complexity is O(M + N) which can be reduced to O(N).
