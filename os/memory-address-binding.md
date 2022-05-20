# Memory Address binding

## Address binding

프로그램을 실행하면, 프로세스(실행된 프로그램)을 위한 독자적인 주소 공간이 생성된다.
대부분의 시스템은 프로세스가 메모리 내 어느 부분에든 올라갈 수 있도록 지원하고 있다.

해당 프로세스의 주소가 0번지부터 시작한다고 해서 물리 메모리(하드웨어) 주소의 0번지부터 시작할 필요는 없다.

운영체제가 이를 가능하도록 지원하며 주소 바인딩이라는 방식을 통해 주소를 할당한다.
이를 통해 할당된 주소를 논리 주소(logical address) 또는 가상 주소(virtual address)라고 부른다.

주소 바인딩은 할당 시점에 따라 세 가지로 나뉘는데, 아래와 같다.

- 컴파일 타임 바인딩(Compile time binding)
    
    프로세스가 물리 메모리에 들어갈 위치를 알고 있다면 컴파일 타임에 절대 코드(Absolute code)를 생성할 수 있다.
    
    (Absolute code(절대 코드): 어셈블리어가 정한 위치에 물리적으로 고정적으로 위치하는 코드)
    
    이 방식은 프로그램 내부에서 사용하는 주소와 물리 주소가 같다.
    따라서, 물리 주소를 변경하고 싶은 경우 다시 컴파일을 해야하며, 잘 사용하지 않는다.
    
    다른 프로세스가 메모리를 차지하고 있는 경우도 있을 수 있으며, 하나의 프로세스만 사용할 때, 사용할 수 있다.
    
- 로드 타임 바인딩(Load time binding)
    
    프로세스가 메모리 내 어디로 올라올 지 컴파일 시점에 알지 못한다면, 컴파일 타임에 재배치 가능 코드(relocatable code)로 만들어야 한다.
    
    이 방식은 프로그램이 메인 메모리에 적재될 때(로드) 이루어진다.
    
    컴파일 타임 바인딩과 다르게 멀티 프로그래밍이 가능하지만, 메모리를 참조하는 명령어를 다 변경해야 하기 때문에, 메모리 로딩 시간이 오래걸린다.(실제로 사용되지 않는다.)
    
- 런 타임 바인딩(Run time binding || execution time binding)
    
    프로그램을 실행 한 후에도, 프로그램이 위치한 물리 주소가 변경될 수 있는 바인딩 방식
    
    이 방식은 cpu가 주소를 참조 할 때마다, 해당 데이터의 물리 주소가 어디에 위치하는 지 주소 매핑 테이블을 이용해 바인딩을 점검한다.
    
    실행 시간에 바인딩이 이루어지므로 기준/상한 레지스터를 포함한 MMU라는 하드웨어 지원이 필요하다.
    

## MMU

실행 시간에 할당되는 런 타임 바인딩은 MMU의 지원이 필요하다고 했다.

여기서 MMU(Memory management unit)은 CPU 코어 안에서 가상 주소를 물리 주소로 변환해주는 장치이다.

![출처: [https://www.sciencedirect.com/topics/computer-science/memory-management-unit](https://www.sciencedirect.com/topics/computer-science/memory-management-unit)](https://user-images.githubusercontent.com/46529663/169479922-d70d0d2e-a976-43b5-a5be-e78412425c02.png)

출처: [https://www.sciencedirect.com/topics/computer-science/memory-management-unit](https://www.sciencedirect.com/topics/computer-science/memory-management-unit)

![Screen Shot 2022-05-20 at 2.18.18 PM.png](https://user-images.githubusercontent.com/46529663/169480032-d31bb768-7829-4e47-8bdb-a5cee655b2e1.png)

위 사진에서 재배치(기준) 레지스터 속에 들어있는 값을 메모리에 보내는 모든 주소에 더하게 된다.

이를 통해 사용자는 실제 물리 주소에 접근하지 않는다.

위 방식은 주어진 주소부터 연속적으로 상한 주소까지 메모리를 할당하는 연속 메모리 할당(contiguous allocation)으로 MMU를 간단하게 만들어준다.

하지만 연속 메모리 할당은 한계가 있기 때문에, 대부분의 운영체제에서 사용되지 않고, **페이징**이라는 기법을 통해 메모리를 관리한다.

## Reference

[운영체제의 주소 바인딩 알아보기](https://lifelife7777.tistory.com/178)

[[운영체제 OS]Address Binding 주소 할당, 주소 바인딩, 논리적 주소(logical) vs 물리적 주소(physical), 컴파일 타임](https://jhnyang.tistory.com/133)

[[운영체제 OS]Address binding 로드타임 바인딩(load time binding), 실행타임(execution time) 바인딩 (run time binding) 주소할당](https://jhnyang.tistory.com/246)

[Memory Management Unit](https://www.sciencedirect.com/topics/computer-science/memory-management-unit)

[[운영체제 OS] 메모리 관리기법 - 페이징 (paging)이란? 내부 단편화(Internal Fragmentatoin)에 대해 알아보자](https://jhnyang.tistory.com/290?category=815411)