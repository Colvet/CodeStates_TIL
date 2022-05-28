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
