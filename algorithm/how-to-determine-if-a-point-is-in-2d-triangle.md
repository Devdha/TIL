# How to determine if a point is in 2D triangle?

42Seoul 과제인 CPP Module 02 ex03에는 해당 과제에서 만든 클래스들을 이용하여, 
한 점이 삼각형 내에 있는 지 확인하는 함수를 구현하라고 한다.

바로 구글에 `point in triangle algorithm` 으로 검색하니, 처음 나오는 Stack Overflow 글을 발견하고, ~~코드를 찾아서 긴 시간 이해하려고 씨름하다가 이해하지 못해서 다른 방식으로 진행 해야겠다...~~

다음 날 같은 방식으로 구현한 동료를 발견하여, 코드를 이해하고 해결하였다.

사용한 방식은 벡터의 외적을 이용하여 해당 외적의 값이 모두 같은 방향을 가르킬 때, 점이 삼각형 내에 있다고 판단한다.

![위 필기는 동료가 코드를 작성할 때, 이해를 위해 작성한 내용을 공유해주었다. (출처: hyojekim)](https://user-images.githubusercontent.com/46529663/169479808-42073d7a-7cc6-4cf1-abeb-fb08c1d99e52.jpg)

위 필기는 동료가 코드를 작성할 때, 이해를 위해 작성한 내용을 공유해주었다. (출처: hyojekim)

아래 코드에서 sign 함수 내의 식은 벡터의 외적을 구하는 식으로, 
d1일 때를 예시로 BP.x * BA.y - BA.x * BP.y 라는 식을 통해 벡터의 외적을 d1에 저장하게 된다.

예시로 a(0, 0) / b(20, 0) / c(10, 20) / point(5, 5)가 주어졌을 때, 
d1은 BA벡터와 BP벡터의 외적을 구하면 양수가 되고, 이처럼 3개 변과 점과의 관계를 갖는 벡터들의 외적을 구하면 모두 양수이다. ( = 점은 삼각형 안에 있다.) 라는 결론이 나온다.

```cpp
#include "Point.hpp"
#include <iostream>

float sign(Point const p1, Point const p2, Point const p3) {  
    return (p1.getX() - p3.getX()) * (p2.getY() - p3.getY()) \
				- (p2.getX() - p3.getX()) * (p1.getY() - p3.getY());
}

bool bsp(Point const a, Point const b, Point const c, Point const point) {
    float   d1, d2, d3;
    bool    neg, pos;

    d1 = sign(point, a, b);
    d2 = sign(point, b, c);
    d3 = sign(point, c, a);

    if (d1 == 0 || d2 == 0 || d3 == 0)
        return false;
    neg = (d1 < 0) || (d2 < 0) || (d3 < 0);
    pos = (d1 > 0) || (d2 > 0) || (d3 > 0);

    return !(neg && pos);
}
```

이해를 위한 참고자료

[https://stackoverflow.com/questions/2049582/how-to-determine-if-a-point-is-in-a-2d-triangle](https://stackoverflow.com/questions/2049582/how-to-determine-if-a-point-is-in-a-2d-triangle)

[https://www.gamedev.net/forums/topic.asp?topic_id=295943](https://www.gamedev.net/forums/topic.asp?topic_id=295943)
[https://math.stackexchange.com/questions/51326/determining-if-an-arbitrary-point-lies-inside-a-triangle-defined-by-three-points](https://math.stackexchange.com/questions/51326/determining-if-an-arbitrary-point-lies-inside-a-triangle-defined-by-three-points)

그 외에 무게중심을 구하는 방식, 각 변의 꼭짓점과 주어진 점으로 이루어진 삼각형 3개를 구한 뒤 삼각형과 너비가 같은 지 확인하는 방식 등을 사용할 수 있다.