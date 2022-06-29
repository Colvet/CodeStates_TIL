# NFT
> 대체 불능한 토큰. 디털 자산의 소권 분쟁을 해결. 토큰에 대한 소유권이 나뉘어 질 수 있다.

## ERC-721
+ balanceOf
    + 해당 주소가 보유하고 있는 NFT 갯수
+ ownerOf
    + 해당 NFT 소유 주소
+ approve
    + 해당 주소에 NFT 토큰 전송 권한을 부여
+ getApproved
    + 해당 토큰의 전송 권한을 갖고 있는 주소
+ setApprovalForAll
    + NFT 소유자가 해당 주소에게 모든 NFT 토큰에 대한 전송 권한을 부여(해제)
+ isApprovedForAll
    + setApprovalForAll 권한이 있는지 참/거짓
+ transferFrom
    + NFT 소유자로부터 해당 NFT 토큰을 다른 주소로 전송
+ safeTransferFrom
    + 전송 받는 주소가 erc721을 받을 수 있느지 체크

## ERC-721A
> NFT 프로젝트 Azuki 팀에서 개발. 단일 트랜잭션에서 여러 NFT를 발행 -> 가스 절감 효과

## ERC-4907
> 더블 프로토콜이 개발. NFT소유권과 사용권을 분리하고 사용권 만료시 이를 자동 회수(반납)하는 기능을 포함


