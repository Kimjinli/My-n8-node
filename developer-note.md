개발자로서 가장 직관적으로 구조를 이해할 수 있는 **"HTTP 웹훅을 받아서 노션(Notion)에 기록하기"**의 아주 기초 버전을 만들어 봅시다. 노션 설정이 당장 번거로우면 우선 **"웹훅을 받아서 구글 시트나 간단한 응답 보내기"**로 대체할 수 있지만, 일단 n8n의 기본 흐름을 익히는 게 목적입니다.

가장 쉬운 'Hello World'급 자동화를 만들어 보겠습니다.

1단계: 첫 번째 워크플로우 만들기 (Webhook → Response)
빈 캔버스에서 시작하세요.

Webhook 노드 추가: 캔버스 중앙의 + 버튼을 누르고 Webhook을 검색해서 추가합니다.

설정: 생성된 Webhook 노드를 더블 클릭합니다.

HTTP Method: POST (데이터를 보낼 때 주로 씁니다)

Path: hello-n8n 정도로 적어줍니다.

URL 복사: 상단의 Test URL 탭을 클릭하고 그 주소를 복사해둡니다.

주의: 꼭 'Test URL'을 쓰셔야 실시간으로 데이터 들어오는 게 보입니다.

Listen 모드 실행: 오른쪽 상단의 Listen for Test Event를 누릅니다. 이제 n8n은 신호를 기다립니다.

2단계: 신호 보내보기 (테스트)
개발자시니까 터미널이나 curl이 편하시겠죠? 새로운 터미널 탭을 열고 복사한 URL로 데이터를 쏴보세요.

Bash
curl -X POST https://복사한-주소/hello-n8n \
     -H "Content-Type: application/json" \
     -d '{"message": "안녕 n8n!", "author": "개발자"}'
결과 확인: n8n 캔버스로 돌아오면 Webhook 노드에 초록색 체크가 뜨고, 보낸 데이터({"message": "안녕..."})가 들어온 것을 확인할 수 있습니다.

3단계: 응답 노드 연결 (선택사항)
신호를 받았으니 답장을 줘야겠죠?

Webhook 노드 옆의 +를 눌러 Respond to Webhook 노드를 추가합니다.

이 상태로 저장하면 끝입니다. 이제 아까 curl을 날리면 n8n이 데이터를 받고 "성공"이라는 응답을 돌려줍니다.

4단계: 깃(Git)에 저장하기 (오늘의 핵심)
이제 이 작업물을 잃어버리지 않게 깃허브 레포에 저장해 봅시다. 캔버스 오른쪽 상단의 Save를 먼저 눌러주세요.

터미널에서 n8n 종료: 실행 중인 터미널에서 Ctrl + C를 눌러 잠시 끕니다.

워크플로우 추출 (Export):

Bash
# workflows 폴더가 없다면 먼저 만드세요: mkdir workflows
n8n export:workflow --all --output=./workflows/