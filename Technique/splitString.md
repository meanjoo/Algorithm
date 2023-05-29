## 특정 문자 기준으로 자르기
### 정수 문자열일 때
```C++
int sep = str.find("특정 문자"); // 특정 문자가 ,인 경우 → str.find(",");
int prev = 0;
while(sep != string::npos) {
  string sub = str.substr(prev, sep-prev);
  v.push_back(stoi(sub));
  prev = sep + 1;
  sep = str.find("특정 문자", prev);
}
v.push_back(stoi(str.substr(prev)));
```

### 일반 문자열일 때
정수 문자열일 때와 같은데, vector에 push하는 부분에서 stoi()만 빼주면 된다.
```C++
int sep = str.find("특정 문자");
int prev = 0;
while(sep != string::npos) {
  string sub = str.substr(prev, sep-prev);
  v.push_back(sub);
  prev = sep + 1;
  sep = str.find("특정 문자", prev);
}
v.push_back(str.substr(prev));
```

## substr()
문자열에서 일부를 반환한다. substr(시작 인덱스, 개수)

```C++
string originStr = "Hello, World!";

cout << originStr.substr() << '\n';
cout << originStr.substr(3) << '\n';
cout << originStr.substr(5, 4) << '\n';
cout << originStr.substr(0, 20) << '\n';
// cout << originStr.substr(20) << '\n';
```

▼ 출력 결과
```
Hello, World!
lo, World!
, Wo
Hello, World!
```

아무 값도 전달하지 않으면 원래 문자열을 그대로 반환한다.  
값을 하나(i)만 전달하면 i번째 인덱스부터 원래 문자열의 끝까지를 반환한다. 이 값을 원래 문자열의 길이보다 큰 값으로 주게 되면 오류가 발생한다.  
값을 두 개(i, len)를 전달하면 원래 문자열의 i번째 인덱스부터 len개만큼의 문자열을 반환한다. i+len-1이 원래 문자열의 마지막 인덱스를 초과하여도 오류는 발생하지 않고 i번째 인덱스부터 원래 문자열의 끝까지를 반환한다.
