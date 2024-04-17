```c++

#ifdef LOCAL
#define _GLIBCXX_DEBUG
#endif
#include <bits/stdc++.h>
using namespace std;
using ll = long long;
using ld = long double;
using uint = unsigned int;

template<typename T>
inline istream& operator>> (istream& in, vector<T>& vec) {
    for (auto& i : vec) {
        in >> i;
    }
    return in;
}

template<typename T>
inline ostream& operator<< (ostream& out, vector<T>& vec) {
    if (vec.empty()) {
        return out;
    }
    out << *vec.begin();
    for (uint i = 1; i != vec.size(); i++) {
        out << ' ' << vec[i];
    }
    return out;
}

vector<ll> z_function(string& s) {
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
    return z;
}

void solve() {
    ll n;
    cin >> n;
    vector<ll> z(n);
    cin >> z;
    if (z[0] != 0) {
        cout << '!';
        return;
    }
    vector<char> alphabet(('z' - 'a' + 1) * 2, 'a');
    for (ll i = 1; i < alphabet.size(); i++) {
        alphabet[i] = (alphabet[i - 1] == 'z' ? 'A' : (alphabet[i - 1] + 1));
    }
    string ans(n, ' ');
    ll curChar = 0, j = 0, prefLen = 0;
    for (ll i = 0; i < n; i++) {
        if (z[i] == 0 && prefLen == 0) {
            ans[i] = alphabet[curChar++];
            continue;
        }
        if (z[i] > prefLen) {
            prefLen = z[i];
            j = 0;
        }
        ans[i] = ans[j++];
        prefLen--;
    }
    vector<ll> q(z_function(ans));
    for (ll i = 0; i < n; i++) {
        if (z[i] != q[i]) {
            cout << '!';
            return;
        }
    }
    cout << ans;
}

int main() {
    ios_base::sync_with_stdio(false);
    cin.tie(nullptr);
    cout.tie(nullptr);
    ll n;
    cin >> n;
    while (n--) {
        solve();
        cout << '\n';
    }
    return 0;
}

```
