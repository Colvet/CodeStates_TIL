# Solidity

## 상태변수
> 상태 변수는 값이 컨트랙트 스토리지에 영구적으로 저장되는 변수를 의미.
+ Boll
    + true, false
+ int, uint
    + 부호가 있는경우 int 부호가 없는 0 이상의 값은 uint
+ address
    + 0x로 시작하고 최대 40자리의 16진수로 구성되는 문자열을 값으로 가진다.
    + 0.8 버전부터 address 형식은 송금이 불가능한 주소값. 특정 주소 값으로 송금을 하기 위해서는 ```address payable``` 형식을 사용해야 한다.
```solidity
address addr1;
address payable p_addr1 = payable(addr1);

```
## 참조형 데이터
> 배열과 같이, 데이터를 저장하는 영역에 연속되어 저장되어 있는 값의 첫번째 메모리의 주소를 값으로 가지는 변수

+ 구조체
```
contract exmapleC {

	struct UserInfo {
	    address account;
	    string lastName;
	    string firstName;
	}
	
	function newUser (address newAddress, string newLastName, string newFirstName){
	    UserInfo memory newOne = UserInfo({account: newAddress, lastName: newLastName, firstName: newFirstName})
	}
}
```

+ 매핑
    + 스토리지 데이터 영역에서 ```키-값``` 구조로 데이터를 저장할 때 사용하는 참조형
    + mapping({키 형식} => {값 형식}) {변수명}
```
mapping(address => int) public userAddr
```
## 글로벌 변수
> 솔리디티 언어에 내장되어 있는 변수

+ block
    + blockhash(uint blocknumber): 주어진 블록의 해시를 bytes32 형태로 반환합니다
    + coinbase:블록의 채굴자 주소. address 형식
    + gaslimit: 블록의 가스 한도. uint 형식
    + number : 블록의 번호. uint 형식
    + timestamp: 블록 타임스탬프. uint 형식
+ msg
    + gasleft(): 남아있는 가스의 양을 uint256 형태로 반환
    + data: 전체 콜데이터 본문. bytes 형식
    + sender: 현재 호출을 수행하고 있는 메시지 발신자. address 형식
    + gas: 남은 가스양. uint 형식
    + value: 메시지와 함께 보낸 이더 금액. uint 형식
+ tx
    + gasprice : 트랜잭션 가스 비용. uint 형식
    + origin: 트랜잭션 발신자. address 형식
+ This
    + gasprice : 트랜잭션 가스 비용. uint 형식
    + origin: 트랜잭션 발신자. address 형식

## 상태 변수 접근 수준
+ internal
    + 커트랙트 및 해당 커트랙트를 상속 받은 커트랙만 인터널 상태 변수를 사용할 수 있다.
+ public
    + 컴파일러가 퍼블리 상태 변수에 getter 함수를 생성. 퍼블릭 상태 변수는 커트랙트 내에서 직접 퍼블릭 상태 변수를 사용할 수 있고, 외부 컨트랙트나 클라이언트 코드에서 getter 함수를 통해 퍼블릭 상태 변수에 접근
+ private
    + 동일한 컨트랙트 멤버만 프라이빗 상태 벼수에 접근할 수 있다.

## 함수 접근 수준
+ external
    + 외부 커트랙트나 클라이언트 코드에서 호출할 수는 있으나, 커트랙트 내부에서는 호출할 수 없다
+ public
    + 커트랙트 내/외 부, 클라이언트 코드에서 호출
+ internal
    + 커트랙트 멤버와 상속된 커트랙트에서만 호출
+ private
    + 커트랙트 멤버만 호출
+ view
    + 상태를 변경하지 않는 읽기 전용 함수
+ pure
    + 스토리지에서 변수를 읽거나 쓰지 않는 함수
+ payable
    + 함수에서 이더를 받을 수 있다.
+ constructor
    + 생성자 함수를 선언하면, 컨트랙트가 생성될 때 생성자 함수가 실행되며 커트랙트의 상태를 초기화할 수 있다.

## 함수 변경자(modifier)
> 함수 선언에 modifier를 추가하여 함수에 변경자를 적용할 수 있다. 변경자를 작성할 때는 ``_;``를 사용. ``_;``는 함수를 실행하는 시점을 나타내며, 변경자 코드는 ``_;`` 코드를 기준으로 실행 시점이 달라짐. ``_;`` 이전의 코드는 함수가 실행되기 전에 실행되고, ``_;`` 이후의 코드는 함수 실행이 종료되고 실행

```변경자: 함수를 실행하기 전, 요구 조건을 만족하는 지 확인하는 작업```

## 상속
> contract 객체는 상속을 지원. ``is`` 키워드를 지정. 다중 상속 지원

## 에러 핸들링
+ revert
    + 해당 함수를 종료하고 에러를 리턴
+ require, assert
    + 설정한 조건이 참인지 확인하고, 조건이 거짓이면 에러를 리턴

## 이벤트
> 어떤 결과가 발생했을 때 해당 컨트랙트에서 dApp 클라이언트, 또는 다른 컨트랙트에게 전달. 경우에 따라 ``emit`` 키워드를 사용해 이벤트를 실행. 이벤트가 실행될 경우, 트랜잭션에 기록
