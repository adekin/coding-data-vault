```c++
#include <iostream>
#include <vector>
using namespace std;
using ll = long long;
 
int main() {
    string s;
    cin >> s;
    ll n = s.size(), l = 0, r = 0; // Z-block = s[l; r)
    vector<ll> z(n, 0);
    for (ll i = 1; i < n; i++) {
        if (i < r) {
            z[i] = min(r - i, z[i - l]);
        }
        while (i + z[i] < n && s[z[i]] == s[i + z[i]]) {
            z[i]++;
        }
        if (i + z[i] > r) {
            l = i;
            r = i + z[i];
        }
    }
    for (auto& i : z) {
        cout << i << ' ';
    }
    return 0;
}

```
