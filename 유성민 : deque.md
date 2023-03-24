**덱의 성질**

덱은 양쪽 끝에서 삽입과 삭제가 전부 가능하며, 기능 그대로 **deque**의 뜻은 **Double Ended Queue**라는 뜻을 가지고 있다.

-   원소의 추가는 O(1)이다.
-   원소의 제거는 O(1)이다.
-   제일 앞/뒤의 원소의 확인은 O(1)이다.
-   제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로 불가능하다.

제일 앞/뒤가 아닌 나머지 원소들의 확인/변경이 원칙적으로는 불가능 하지만, **STL deque에서는 인덱스로 원소에 접근이 가능하다**.

**덱의 구현**

우선 덱은 양쪽으로 확장이 가능해야 하기 때문에 배열의 크기가 2\*MX+1 이고 head와 tail의 초기값이 MX이다.

덱도 원형으로 구현하는게 가능하지만 아래 코드는 선형 구조이다.

```
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

**STL deque**

STL의 deque는 vector와 비슷하면서 front에서 O(1)에 추가와 제거가 가능한 느낌이 강하다. insert도 있고 erase도 있고 인덱스로 원소에 접근도 가능하다. 이와같이 vector의 기능에 deque에 기능이 추가되어서 vector의 상위호환이라 생각할 수 있지만, deque는 모든 원소들이 메모리 상에 연속하게 배치되어 있지 않다. 그렇기 때문에 굳이 앞쪽에서의 추가/제거가 필요하지 않다면 deque를 사용할 필요가 없다.

```
#include <bits/stdc++.h>
using namespace std;

int main() {
    cin.tie(0)->sync_with_stdio(0);

    deque<int> DQ;
    DQ.push_front(10);      //10
    DQ.push_back(50);           //10 50
    DQ.push_front(24);          //24 10 50

    for(auto x : DQ) cout << x;
    cout << DQ.size() << '\n';          //3
    //
    if(DQ.empty()) cout << "DQ is empty\n";
    else cout << "DQ is not empty\n";       //DQ is not empty

    DQ.pop_front();             //10 50
    DQ.pop_back();              //10
    cout << DQ.back() << '\n';  //10
    DQ.push_back(72);          //10 72
    cout << DQ.front() << '\n';     //10
    DQ.push_back(12);              //10 72 12
    DQ[2] = 17;                 //10 72 17

    DQ.insert(DQ.begin()+1, 33);        //10 33 72 17
    DQ.insert(DQ.begin()+4, 60);                //10 33 72 17 60
    for(auto x : DQ) cout << x << ' ';
    cout << '\n';
    DQ.erase(DQ.begin() + 3);           //10 33 72 60
    cout << DQ[3] << '\n';              //60
    DQ.clear();                 //DQ의 모든 원소 제거
}
```