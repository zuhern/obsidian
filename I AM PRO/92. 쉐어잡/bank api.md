---
Created: Invalid date
Updated: Invalid date
---
입출금거래요청내역요청 POST /bank?field=requests 후지불에 대한 입금일 경우 body={postId, applicantId} 함께거나.. 화면에서 미지급 리스트 선택하는 경우 bankRewardId (추후 결정)수정 PUT /bank/:requestId/?field=requests&method=modify, confirm 값 없으면 error취소 DELETE /bank/:requestId/?field=requests&method=reject 인경우 관리자가 반려. method없으면 요청자 취소보상금처리상태지급 POST /bank?field=rewards body: {postId, applicantId, paid:true (지급완료), false (후지급예정)} 후지급 후 입금 완료되면 true로 해당 api 호출하면 지급 완료환불완료 PUT /bank/:rewarded?field=rewards환불 DELETE /bank/:rewardId?field=rewards계좌거래내역리스트 조회 GET /bank?field=passbooks한 건 조회 GET /bank/:passbookId거래요청로그리스트 조회 GET /bank?field=logs한 건 조회 GET /bank/:logId?field=logs