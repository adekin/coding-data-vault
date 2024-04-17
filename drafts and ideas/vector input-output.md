```c++

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

```
