# 크립토 좀비 정리
> https://cryptozombies.io 사이트에서 학습한 내용 정리

## 상태변수
> 컨트랙트 스토리지에 영원히 저장되는 변수(블록에 저장)

## private
+ private 키워드는 함수명 다음
+ 함수 인자명과 마찬가지로 private 함수명도 언더바(_)로 시작

## view
+ 어떤 값을 변경하거나 write 기능 없음.
+ 함수를 보기만 하고 변경하지 않는다.

## pure
+ 함수가 앱에서 어떤 데이터도 접근하지 않는 것을 의미

## 이벤트
이벤트는 자네의 컨트랙트가 블록체인 상에서 자네 앱의 사용자 단에서 무언가 액션이 발생했을 때 의사소통하는 방법

// 이벤트를 선언한다
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public {
  uint result = _x + _y;
  // 이벤트를 실행하여 앱에게 add 함수가 실행되었음을 알린다:
  IntegersAdded(_x, _y, result);
  return result;
}
그러면 자네 앱의 사용자 단은 해당 이벤트가 일어나는지 귀를 기울이지. 자바스크립트로 이를 구현하면 다음과 같네:

YourContract.IntegersAdded(function(error, result) {
  // 결과와 관련된 행동을 취한다
})


## Array push
 array.push()는 배열의 새로운 길이를 uint형으로 반환한다

 ## Mapping
 > 매핑은 기본적으로 키-값 (key-value) 저장소로, 데이터를 저장하고 검색하는 데 이용된다. 첫번째 예시에서 키는 address이고 값은 uint이다. 두번째 예시에서 키는 uint이고 값은 string이다.

```
mapping (address => uint) public accountBalance; // 금융 앱용으로, 유저의 계좌 잔액을 보유하는 uint를 저장한다:      

mapping (uint => string) userIdToName; //userID로 유저 이름을 저장/검색하는 데 매핑을 쓸 수도 있다
```

## 비교
+ 솔리디티는 고유의 스트링 비교 기능을 가지고 있지 않기 때문에 keccak256 해시값을 비교하여 스트링 값이 같은지 판단한다

## Internal vs External
+ Iternal은 함수가 정의된 컨트랙트를 상속하는 컨트랙트에서도 접근이 가능하다 점을 제외하면 private과 동일
+ External은 함수가 컨트랙트 바깥에서만 호출될 수 있고 컨트랙트 내의 다른 함수에 의해 호출될 수 없다는 점을 제외하면 public과 동일


## 챕터 12: 다수의 반환값 처리하기 중요.
getKitty 함수는 우리가 살펴 본 예시 중 유일하게 다수의 반환값을 갖는 함수이지.

function multipleReturns() internal returns(uint a, uint b, uint c) {
  return (1, 2, 3);
}

function processMultipleReturns() external {
  uint a;
  uint b;
  uint c;
  // 다음과 같이 다수 값을 할당한다:
  (a, b, c) = multipleReturns();
}

// 혹은 단 하나의 값에만 관심이 있을 경우: 
function getLastReturnValue() external {
  uint c;
  // 다른 필드는 빈칸으로 놓기만 하면 된다: 
  (,,c) = multipleReturns();
}

## modifier
 modifier onlyOwner(). 제어자는 다른 함수들에 대한 접근을 제어하기 위해 사용되는 일종의 유사 함수라네. 보통 함수 실행 전의 요구사항 충족 여부를 확인하는 데에 사용

 ## Gas
 + 만약 자네가 구조체 안에 여러 개의 uint를 만든다면, 가능한 더 작은 크기의 uint를 사용. 솔리디티에서 그 변수들을 더 적은 공간을 차지하도록 압축
 ```
struct NormalStruct {
  uint a;
  uint b;
  uint c;
}

struct MiniMe {
  uint32 a;
  uint32 b;
  uint c;
}
```
 + uint, string 등은 자동으로 uint256 사용
 + 데이터 타입은 하나로 묶어놓고 사용. 즉, 구조체에서 서로 옆에 있도록 선언하면 솔리디티에서 사용하는 저장 공간을 최소화. 
 ```
uint c; uint32 a; uint32 b; //아래 보다 가스 덜 사용
uint32 a; uint c; uint32 b;
```
+ view 함수는 gas 소모 하지 않는다

## memory 
+ storage를 사용하는데는 gas가 사용 되기 떄문에 어떤 배열에서 내용을 빠르게 찾기 위해, 단순히 변수에 저장하는 것 대신 함수가 호출될 때마다 배열을 memory에 다시 만든다.
+ 어떤 배열에서 내용을 빠르게 찾기 위해, 단순히 변수에 저장하는 것 대신 함수가 호출될 때마다 배열을 memory에 다시 만듬.
+ memory를 사용할때는 항상 크기를 설정

## 함수 정리
+ private
  + private은 컨트랙트 내부의 다른 함수들에서만 호출될 수 있음을 의미하지. 
+ internal 
  + internal은 private과 비슷하지만, 해당 컨트랙트를 상속하는 컨트랙트에서도 호출 가능
+ external
  + external은 오직 컨트랙트 외부에서만 호출
+ public
  + 마지막으로 public은 내외부 모두에서, 어디서든 호출 가능
+ view
  + view는 해당 함수를 실행해도 어떤 데이터도 저장/변경되지 않음
+ pure는 해당 함수가 어떤 데이터도 블록체인에 저장하지 않을 뿐만 아니라, 블록체인으로부터 어떤 데이터도 읽지 않음.
  + 이들 모두는 컨트랙트 외부에서 불렸을 때 가스를 전혀 소모하지 않는다.

## Payable
+ 생성한 contract로 이더 보내기

## 출금
+ 해당 컨트랙트 주소에 있는 이더를 출금
+ this.balance : 컨트랙트에 저장돼있는 전체 잔액

## 오버플로우, 언더플로우
1. 8비트 데이터를 저장할 수 있는 uint8 하나를 가지고 있다 가정. 
2. 저장할 수 있는 가장 큰 수는 이진수로 11111111(또는 십진수로 2^8 - 1 = 255)
3. uint8 number = 255; number++; 해당 코드 실행시
4. 오버플로우 발생 (number 가 0으로 된다 또는 00000000)
5. 언더플로우는 이와 유사하게 0 값을 가진 uint8에서 1을 빼면, 255와 같아진다. uint는 음수가 없기 떄문에

## assert
+ assert는 조건을 만족하지 않으면 에러를 발생시킨다는 점에서 require와 비슷. assert와 require의 차이점은, require는 함수 실행이 실패하면 남은 가스를 사용자에게 되돌려 주지만, assert는 그렇지 않다. assert는 일반적으로 코드가 심각하게 잘못 실행될 때 사용


# Web3

## Call
> call은 view와 pure 함수를 위해 사용 블록체인에 트랜잭션을 생성하지 않는다.
+ public으로 변수를 선언하면 자동으로 같은 이름의 퍼블릭 "getter" 함수를 생성


## Send
> send는 트랜잭션을 만들고 블록체인 상의 데이터를 변경. view와 pure가 아닌 모든 함수에 대해 send를 사용.

## Wei
> 이더리움의 가장 작은 단위 1eth = 10^18 wei
+ 변환: web3js.utils.toWei("1"); 1 eth

## indexed
> 이벤트를 필터링하고 현재 사용자와 연관된 변경만을 수신하기 위해, ERC721을 구현할 때 Transfer 이벤트에서 했던 것처럼 솔리디티 컨트랙트에 indexed 키워드를 사용.
```
event Transfer(address indexed _from, address indexed _to, uint256 _tokenId);
이 경우, _from과 _to가 indexed 되어 있기 때문에, 프론트엔드의 이벤트 리스너에서 필터링 가능:

// `filter`를 사용해 `_to`가 `userAccount`와 같을 때만 코드를 실행
cryptoZombies.events.Transfer({ filter: { _to: userAccount } })
.on("data", function(event) {
  let data = event.returnValues;
  // 현재 사용자가 방금 좀비를 수령
  // 해당 좀비를 보여줄 수 있도록 UI를 업데이트할 수 있도록 여기에 추가
}).on("error", console.error);
```
event와 indexed 영역을 사용하는 것은 컨트랙트에서 변화를 감지하고 프론트엔드에 반영할 수 있게 하는 유용한 방법.

## Event
1. getPastEvents를 이용해 지난 이벤트들에 대해 질의를 하고, fromBlock과 toBlock 필터들을 이용해 이벤트 로그에 대한 시간 범위를 솔리디티에 전달할 수 있다.
```
cryptoZombies.getPastEvents("NewZombie", { fromBlock: 0, toBlock: "latest" })
.then(function(events) {
  // 생성된 모든 좀비의 목록을 우리가 받을 수 있게 할 것이네.
});
```
2. 위 메소드를 사용해서 시작 시간부터의 이벤트 로그들에 대해 질의를 할 수 있기 때문에, 이벤트를 저렴한 형태의 storage로 사용할 수 있다.
3. 데이터를 블록체인에 기록하는 것은 솔리디티에서 가장 비싼 비용을 지불하는 작업 -> 이벤트를 이용하는 것은 가스 측면에서 훨씬 더 저렴
  + 3.1 여기서 단점이 되는 부분은 스마트 컨트랙트 자체 안에서는 이벤트를 읽을 수 없다. 하지만 히스토리로 블록체인에 기록하여 앱의 프론트엔드에서 읽기를 원하는 데이터가 있다면, 이는 새겨놓아야 할 중요한 사용 예시이네.
  + 3.2 예를 들어, 우린 이것을 좀비 전투의 히스토리 기록용으로 사용 - 좀비가 다른 좀비를 공격할 때마다, 그리고 누군가 이길 때마다 우린 이벤트를 생성 -> 스마트 컨트랙트는 추후 결과를 계산할 때 이 데이터가 필요하지 않지만, 사용자들이 앱의 프론트엔드에서 찾아볼 수 있는 유용한 데이터가 된다.