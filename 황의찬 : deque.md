# deque
양쪽 끝에서 삽입과 삭제가 전부 가능한 자료구조.  
  
## deque의 성질
1. 원소의 추가가 O(1)  
2. 원소의 제거가 O(1)  
3. 제일 앞/뒤의 원소 확인이 O(1)  
4. 제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능  
STL deque -> 인덱스로 원소에 접근할 수 있습니다.  
  
## 구현
덱에서는 양쪽에서 모두 삽입이 가능. 양쪽으로 확장해야 합니다.  
시작 지점이 0번지라면 왼쪽으로 확장을 할 수가 없게 됩니다.  
대신에 시작 지점을 배열의 중간으로 둬야 합니다.  
```c++
#include <bits/stdc++.h>
using namespace std;

const int MX = 1000005;
int dat[2*MX+1];
int head = MX, tail = MX;

void push_front(int x){
    dat[--head] = x;
}

void push_back(int x){
    dat[tail++] = x;
}

void pop_front(){
    head++;
}

void pop_back(){
    tail--;
}

int front(){
    return dat[head];
}

int back(){
    return dat[tail-1];
}

void test(){
    push_back(30); // 30
    cout << front() << '\n'; // 30
    cout << back() << '\n'; // 30
    push_front(25); // 25 30
    push_back(12); // 25 30 12
    cout << back() << '\n'; // 12
    push_back(62); // 25 30 12 62
    pop_front(); // 30 12 62
    cout << front() << '\n'; // 30
    pop_front(); // 12 62
    cout << back() << '\n'; // 62
}

int main(void){
    test();
}
```
  
## STL deque
```c++
#include <bits/stdc++.h>

using namespace std;
#define X first
#define Y second
typedef pair<int, int> pii;
/**
 * 앞쪽과 뒷쪽에서의 추가와 제거가 모두 필요하면
 * STL deque 사용하는 것이 효율적
 */
int main() {
    cin.tie(0)->sync_with_stdio(0);
    deque<int> dq;
    dq.push_front(10); // 10
    dq.push_back(50); // 10 50
    dq.push_front(24); // 24 10 50
    for (auto i : dq) cout << i << ' ';
}
```
vector와 비슷하지만 front에서도 O(1)에 추가와 제거가 가능합니다.  
vector와 달리 deque은 모든 원소들이 메모리 상에 연속하게 배치되어 있지 않습니다.  
앞쪽과 뒷쪽에서의 추가와 제거가 모두 필요하다면 당연히 STL deque을 사용하는 게 효율적  
인덱스로 접근 가능, insert와 erase가 있다.  

문제에서 앞뒤 삽입/삭제를 O(1)에 하도록 요구하는 경우 덱 사용 고려  
