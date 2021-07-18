# Competitive Programming-SOC

1) Handbook of CP by Antti Laaksonen:-
        Completed the section 1 of the book consisting of 10 chapters.
        Completed the require portion of the second section of the book which consisted of graphs and trees.xod
2) Did Problems on Codeforces, Codechef and HackerRank.


What I liked the most in my SOC:-
  I thoroughly enjoyed reading and solving problems on Dynamic Programming in CP. The fact that we could reduce the time complexity fro n
   Dynamic Programming is mainly an optimization over plain recursion. Wherever we see a recursive solution that has repeated calls for same inputs, we can optimize it using Dynamic Programming. The idea is to simply store the results of subproblems, so that we do not have to re-compute them when needed later. This simple optimization reduces time complexities from exponential to polynomial. For example, if we write simple recursive solution for Fibonacci Numbers, we get exponential time complexity and if we optimize it by storing solutions of subproblems, time complexity reduces to linear. 
   
   A general algorithm for a DP problem:
   
   
    int m, n;
    vector<long long> dp_before(n), dp_cur(n);

    long long C(int i, int j);

    // compute dp_cur[l], ... dp_cur[r] (inclusive)
    void compute(int l, int r, int optl, int optr) {
    if (l > r)
        return;

    int mid = (l + r) >> 1;
    pair<long long, int> best = {LLONG_MAX, -1};

    for (int k = optl; k <= min(mid, optr); k++) {
        best = min(best, {(k ? dp_before[k - 1] : 0) + C(k, mid), k});
    }

    dp_cur[mid] = best.first;
    int opt = best.second;

    compute(l, mid - 1, optl, opt);
    compute(mid + 1, r, opt, optr);
    }

    int solve() {
    for (int i = 0; i < n; i++)
        dp_before[i] = C(0, i);

    for (int i = 1; i < m; i++) {
        compute(0, n - 1, 0, n - 1);
        dp_before = dp_cur;
    }

    return dp_before[n - 1];
    }
