# Naver Tech Concert - Mobile(iOS)
1. 네이버 지도 밑그림을 그리는 SDK 개발자가 하는 일 - Maps/Mobile 손원영
	* 현재 네이버지도 SDK의 버전은 5.0
	* 네이버 지도앱에 사용되는 기능들 중 범용적인 기능을 뽑아 만든 것이 SDK
	* 5.0 출시 후 변경 점
		1. 레스터 -> 벡터
		2. 옵C -> Swift
		3. 다국어 지원 향상(영어 + 일본어, 중국어)
		4. 실시간 업데이트 지원
		5. 기술 개편
			1. 각종 엔진 내재화
			2. 백터맵 엔진
			3. 모듈형 설계
		6. 사용성 개편
	* 하지만 평가는 좋지 못햇다...
		1. 격변의 UI/UX
		2. 예전 디자인에 익숙한 사용자들
		3. 엔진의 퀄리티 문제
	* 지속적인 개선과 업데이트 -> 평점은 안 돌아왔지만 사용자는 많이 돌아왔다.
	*  NaverMap Mobile SDK overview
		* OpenGL ES를 사용하는 모바일 풀 벡터 지도 렌더링 엔진
		* 오픈 소스 소프트웨어 및 오픈 스탠다드 최대한 활용
		* 네이버 클라우드 플랫폼을 통해 무료로 공개
	* 처음부터 새로 개발 하지 않았다
		* 지도 엔진만 생각하면 처음부터 만들 수 있지만
		* 엔진은 다양한 플랫폼과 유기적으로 움직이므로 오픈소스 사용이 필연적(인력 문제도 있었고)
	* 오픈소스 엔진을 래핑하지도 않았다
		* 범용 GIS엔진을 그대로 쓸 수는 없었다
	* 답은 포크 & 재개발
		* 디렉토리 구조부터 API까지 수정
		* 안 건드릴 곳은 안 건드리고 건드릴 곳은 과감히 건드림
	* 과거 이미 렌더링 된 비트맵은 이어붙이는 데에서, 온 디멘드 렌더링 단계로 발전 (여전히 비트맵으로 해야하는 건 텍스쳐로)
	* 개선사항
		* 퀄리티 향상(줌인, 줌아웃, 회전 시 동적으로 요소들이 재배치 됨)
		* 데이터 사용량 절감(이미지를 통째로 가져오는 것에서 데이터만 받아오므로) -> 특히 기존에는 여러 레이어를 모두 가져와야 했으므로 
			* 레이어 중 하나만 바뀌어도 전부 다시 받아야 했으므로 데이터 낭비가 필연적 -> 지금은 바뀐 부분만 받아오게 할 수 있다
		* 빠른 업데이트 -> 기존 전체 렌더링하는 데에 들던 시간이 굉장히 절약됨
	* 집중한 기능 -> 서비스 지향 기능 개발
	* 성능 : 구형기기에서 너무 느리다
		* 디버깅 툴로 연산 최적화
		* 그래픽스, 멀티스레딩 등의 부분의 최적화
		* 최대한 재사용
		* 디자이너/기획자에게 읍소하여 최대한 일을 줄여야...
		* 저사양 옵션으로 타협을 봐야할 수도 있다. 
	* API 디자인/문서화
		* API문서
			* 스레드,널 가능성, 단위 에너테이션
			* 값 범위 , 예외
		* 개발 가이드
			* 최대한 자세히, 예제코드와 스크린 샷도 꼼꼼히, 링크도 철저히
		* 뭔가 구구절절한 설명이 필요하다면 설계가 잘못되거나 이름이 잘못지어진 것...
	* Naver Cloud Platform으로 출시 -> 다양한 기업에서 사용중
		* 지속적인 피드백과 버전업 배포 -> 지도 앱 새버전 출시 후 배포
	* 마무리
		* 앱 안 만들어도 모바일 개발자 가능합니다
		* 자신만의 SDK를 배포해서 더 많은 앱을 만들 수 있다.

2. 들숨에 협업, 날숨에 클린코드 - 뱅크샐러드 박보영
	* 마춤뻡봇에서 SwiftLint 까지
		* 처음에는 그저 맞춤법 밖에 할 게 없었다.
		* 코딩 컨벤션 맞추기
			* 뱅크 샐러드의 예시
				1. guard문 맞추기 -> if-else와 비슷한 구문이므로 비슷하게 사용하자
				2. init components를 표현하는 방식 -> components,parameter는 개별로 보기 쉽게, 하나의  line이 너무 길지 않게 하자(Code review, splitView 시의 가독성 - 약 100자 정도)
			* 정답은 없다. 각자의 취향과 관점은 다르다.
			* 하지만 이들이 모두 모여서 시너지를 내려면 작은 것부터 맞춰야 한다.
			* **우리의 예술로 팀의 생산성을 극대화한다.**
		* 단점: 코딩 컨벤션 관련 수정만 줄창 올라온다.... -> indent 지옥 ->  SwiftLint 도입
		* 좀더 비즈니스 로직에 집중할 수 있도록 하기 위해
	* MVC 탈출하기
		*  Apple의 MVC는 뷰의 생명주기에 컨트롤러가 너무 깊게 관여 -> Massive View Controller가 되기 너무쉽다.
		* Viper,MVP,MVVM 패턴 등... -> 뱅크샐러드는 그 중 MVVM을 도입
		* 왜 도입했나? -> View와 비즈니스 로직을 분리하기 위함 -> RxSwift 도입
		* MVVM 구조
			* View : 예쁜 껍데기 -> layout(),attribute, bind 이 세가지만 가지고 있도록!
			* ViewBindable(프로토콜) -> view에서 발생하는 모든 이벤트, 액션 전달
			* ViewModel : ViewBindable의 구현체
			* Model -> Network 등을 연결, Business Logic만을 전담
		* 동작
			1.  초기 동작 - View 는 attr,layout 로 초기상태를 그림
			2. 액션 - ViewModel이 이벤트를 받아 Model에게 필요 동작을 시킴
			3. 갱신 - Model의 결과를 ViewModel이 받아 View에 전달
		* TDD
			* 처음 상태 - 테스트 커버리지 0%
			* func 단위, Model 단위의 테스트
			* 네트워크 통신 부분은 실제로 할 수도 있지만, 받을 걸로 기대하는 더미 데이터를 넣어주는 방식으로 해결 
		* Swift  버전업
			* 버전을 거듭하는 변화속에서도 클린코드에 대한 고민이 엿보임
				* ex) Result (기존  try-catch 에러 핸들링을 대체함)
		* Summary
			* 훌룡한 정의는 이미 많다
			* 경쟁에서 최고의 무기는 협업이다.
				* Lint : 우리가 읽기 좋은 코드
				* MVC 탈출기 : 우리가 수정하기 용이한 코드
				* TDD : 우리가 확신할 수 있는 코드
				* Swift 버전업: 우리 모두 고민하여 개선하는 코드
			* 모든 고민에는 **우리**가 있어야 한다

3. 쉽고 재미있는 iOS 디버깅 - LLDB Command - 한국카카오은행 안정민
	* LLDB - Xcode의 기본 컴파일러인 LLVM에서 사용하는 디버거(https://lldb.llvm.org)
	* LLDB 사용예시 - 거의 다 alias가 있음
		* 스레드 리스트 출력 - thread list
		* 특정 스레드로 이동 - thread select #
		* 현재(모든) 스레드의 backtrace 보기 - thread backtrace (all) 
		* 지정된 범위의  frame만 보기 - thread backtrace -c 5 [0~4]
		* 숨겨진 frame 보기 기능도 있음
		* 현재 스레드의 특정 frame index 이동 - frame select #
		* 현재 스레드 정보 출력 - thread info
		* frame 위 아래로 이동 - up #/ down #  [default : 1]
		* 현재 frame에 변수를 출력 frame variable (변수명)
		* global 변수 출력 target variable [변수명] -> 실사용 전까지 할당 안된다.
		* 현재 소스 수준의 다음 코드 진행 - thread step-over , next , n
		* 소스 수준을 한단계 밑으로 내려감 -  thread step-in
		* 현재  frame 진행 후 벗어남 - thread step-out, finish
		* 특정 줄/주소 전까지 실행 - thread until # , --frame : 특정 프레임 지정
		* 특정 라인으로 코드 이동
			* thread jump --[line|by] # , --line: 라인 지정, --by : 오프셋 지정
			* 함수로 점프하면 런타임 크래시 남
		* 중단점 거르기
			* expr ---ignore0breakpoints false --(line)
	* LLDB 명령어
		* Evaluationd Expression
			* 기본 설정 언어는 없음 - 수동으로 설정해야 함
			* 명령어
				* po [expression] -코드 실행 후  description 출력
				* p [expression] - 코드 실행 후 값 출력
				* v(fr v) [expression] - 코드를 실행하지 않고, 메모리에서 값을 읽어 옴
			* po는 컴파일을 두번 거치기 때문에, 실제로 실행하지 않는  v를 권장
			* 메모리 주소를 알면 객체 상태를 원하는 것으로 변환 가능 -> 라이브 코딩 가능
		* Script - Python REPL(10까지는 python2,11부터는  python3)
			* script 명령어로 python 명령어를 직접 사용 가능
	* Chisel -> 파이썬으로 작성된 LLDB 명령어 모음(Facebook 제작)

4. ARKit,CoreML,Turi Create 삼형제
	* 데모 앱
		1. Face Detection - AVFoundation의  face detection,[Google MLKit | Vision FrameWork]
			* Tip . 좌표 변경
				* UIKit - 좌 상단이 (0,0)
				* CoreGraphics - 우 하단이 (0,0)
				* AffineTransformation으로 변환
			* Style Transfer - CoreML 이용
		2. 발열 문제 
			* ARKit 사용 시간을 줄이는 법 밖에는 해결책이... 
			* 기기가 뜨거워지면 강제로 프레임을 낮추자
			* 온도 변화에 observer를 달 수 있다
		3. Memory 제한 - app이 사용할 수 있는 양은 한계가 있다.
		4. Anchoring - SceneKit
	* 성장 - 개인 앱을 출시해보자
	* Turi Create으로 Style Transfer 모델 트레이닝 하기
		* Style Transfer : 어떠한 그림의 스타일을 따서 다른 사진에 적용하는 과정 -> 여기서는 지폐의 질감
		* 유명 라이브러리 - 로우 레벨부터 다루는 비교적 전문가를 위한 도구 -> Model base approach?
		* 애플의 솔루션 - CreateML, Turi Create -> Task Based Approach  -> 데이터만 있으면 비전공가도 원하는 모델 사용가능
		* 모델 학습 과정
			* 일반적인 과정 -> 데이터 준비(입력, 정답) , 모델 훈련, 모델 평가
			* Style Transfer 모델의 과정 - 데이터 준비(스타일 이미지,콘텐트), 모델 훈련(콘텐트 이미지의 시맨틱 오차, 스타일 이미지의 스타일 오차 최소화), 모델평가(눈으로 봐야만 확인 가능)
		* 디폴트 세팅으로 하면 만족할만한 결과를 얻기 힘들다.
			* 하이퍼파라미터를 잘 설정해야 한다.
			* 근데 이 부분에 대한 문서가 없다 -> 소스 직접 까서 원하는 파라미터를 뽑아냄
			* 파라미터 조합으로 학습을 해야하는데, 로컬로는 한번에 하나 뿐 -> 병렬로 돌리기 위해 NSML 사용
			* 지폐의 배경색이 반영되는 문제 -> 스타일 이미지를 원하는 부분만  Crop하고 이미지 사이즈를 조정
	* Wrap-up
		1. ML 잘 모르는데 Style transfer 모델 쓰고 싶다? ->  Turi Create 사용
		2. Create ML에서 제공하는 모델이다? -> CreateML 쓰자
		3. 스타일 트랜스퍼 모델은 눈으로 봐야만 결과 평가가 가능하다 -> 잘 비교할 수 있는 방범이 필요
		4. 클라우드에서 병렬적으로 돌리자
		ss
5. 사용자 경험을 높이는 애니메이션 만들기 - 네이버 Apollo  CIC 김기범
	* 왜 애니메이션이 필요한가?
		* 화면 구현도 바쁜데 굳이?
			* 형태는 기능을 따른다 - 루이스 설리번
		* Human Interface Guidelines
			* iOS Design Themes 
				* Content를 중심으로 디자인 하라
				* 애니메이션 = 컨텐츠를 이해하기 쉽게 만드는 도구
	* 애니매이션의 기능
		* 중요한 컨텐츠 강조  : 컨텐츠 상에 중요한 변화가 생겼을 때 발동 됨, 한 번 재생되면 멈추지 않고 재생(Fire-and-forget) -> UIView.animate
		* 컨텐츠의 맥락 유지(변화과정을 드러냄) -> 트랜지션 효과와 밀접히 관련 -> UIView.transition,UIViewControllerAnimatedTransition(프로토콜), UIViewControllerTransitioningDelegate
			* 대부분 fire-and-forget  방식이나, 사용자 제스처에 따라 점진적으로 재생되기도 함
		* 유저 입력에 대한 컨텐츠의 반응 -> 사용자 제스터에 따라 점진적으로 재생됨 -> UIView의  touches계열 메소드를 이용
	* 왜 애니메이션 구현이 어려운가?
		* 시간 요소가 들어가 복잡함
		* 디버깅이 어려움
		* 스펙 이해 어려움
		*  API가 난해
	* 애니메이션 요소 파악
		* 복잡한 애니메이션의 스펙을 빠르게 분석 가능
		* 어떤 API를 사용할 지 신속히 판단 가능
		* 새로운 API를 이해할 때 도움이 됨
	* 애니메이션의 정의 : 특정 이벤트가 발생 했을 때  UI요소를 시간에 따라 변화시키는 것
	* 애니메이션의 3요소
		* 특정 이벤트 - 트리거
			* 단발성(fire-and-forget) : 한번 발동되면 알아서 재생
				* 시작조건, 변화 값들을 잘 정의해놔야 함
			* 연속성 : 사용자의 입력에 따라 지속적으로 반응
				* UIGestureRecognizer와 연관이 깊음
				* 연속적으로 값이 들어오는 Gesture를 주로 사용
				* Rx와 궁합이 잘 맞음
				* iOS 10부터 나온 UIViewPropertyAnimator를 이용 가능(Animaiton의 Progress를 조정 가능)
		* UI요소를 - 타겟
			* 애니메이션이 적용될 대상이나 속성 -> 시간에 따라 변화할 수 있는 속성과 
			* UIView,CALayer,NSLayoutConstraint,UIBaizerPath
				* UIView - UIKit 레벨에서, 애플이 이미 만들어 놓은 애니매이션을 쉽게 적용
				* CALayer - 좀 더 커스텀한 애니매이션 적용할 때 사용 
				* NSLayoutConstraint -  UIView의 위치를 움직일 때 필요
				* UIBaizerPath - CAShapeLayer와 함께 선을 그릴 때 사용
		* 시간에 따라 - 타임
			* 얼마나 오랫동안 재생할 것인가 -> 0.3~0.5초가 적당
			* Curve(Timing Function) - 커브 값은 가능한 실제 세계의 움직임과 비슷하게 [시간곡선 그리는 사이트](https://cubic-bezier.com)
		* 연습하기
			* 많이 해봐야 됨
			* Dribbble에서 좋은 애니메이션 찾아 카피해보기([Dribbble](https://www.dribbble.com)   )
			* 가능한 기본 API 적용해보기
			* 사용하는 앱에서 3요소 분석해보기
		* Wrap-up
			* 앵프라맹스 - 눈에 보이지 않는 차이지만 쌓여서 큰 차이를 만들어 내는 것
			* 애니메이션도 그러하다.

6. [패널톡] iOS 개발자의 성장 루트
	1. 취업?창업?자영업? 어느 길로 갈 것인가?
		* 개발자의 커리어 패스로는 창업은 적당하지 않다. 비전 없으면 굳이 하지 않아도 된다.
		* 어떤 회사에서 취업하는 것이 개발자 커리어 관리 측면에서 좋을까요?
			* 회사에서 얼마나 지원해 줄 수 있는가? -> SI라고 무조건 나쁜 건 아니다. 하지만 잘 골라야지
			* 작은 회사는 인프라가 부족하니 스스로 노력을 해야한다 -> 알아서 잘 할 수 있다면 어떤 회사던 나쁘지 않다. 하지만 그렇지 않다면 큰회사가 좋을 것이다.
		* 어떻게 해야 내가 원하는 회사를 갈 수 있을까?
			* 원하는 회사에 가려면 그 회사가 필요한 인재가 되어야 한다.
			* 일단 공부 열심히 해야한다. 하면 엔간한 건 커버된다.
			* 이력서만 넣지 말고, 여러 행사에 지속적으로 참여해야 한다
			* hackDay -> 미리 해보고 감 -> 원하는 회사에 가고 싶은데 뭔들 못하리 
			* 회사에서 진행하는 교육 프로그램에 참여해보라 -> 부스트캠프
			* 구인의 형태가 기존 공채에서 다각화 되는 중이기 때문에 따라가야 함
			* 이력서를 넣으면 피드백을 요청하자 -> 2~3년차의 이력서가 화려해지는 건 한계가 있다. -> 인사 담당자들에게 물어보면 친절하게 대답해주고, 이 피드백을 반영하면서 성장하자. -> 면접관에게 코드를 보여주는 건 실력을 그대로 드러내므로 양날의 검이다.
			* 항상 붙는 사람과 떨어지는 사람이 있다. 이력서를 계속 업데이트 해야 한다. -> 말빨에 자신 없으면 면접 경험이 많아야 한다.
		* 공부를 하는 방법
			* (나와 다른 사람들이)공부를 하는 방법을 공부하라
				* Case 1.  일단 한번 만들어 보세요 -> 모르는 게 나올 때마다 계속 필요한 것을 찾아간다.  -> 지식의 순서가 없이 들어오기 때문에 반드시 잘 정리되어야 한다.
				* Case 2. 나는 게으르다 -> 스스로를 극한 상황으로 몰아가라(추천하지는 않는다...)
				* Case 3. 일단 검색부터 한다 -> 일단 돌아가야 하니까 갖다 붙인다? -> 왜 그렇게 해야 했는지의 이유를 파악해야 한다. 안그러면 갖다 붙이는 것 밖에 못한다.
				* Case 4. 스터디 - 혼자 공부하는 것은 한계에 부딪힌다 -> 실무를 경험한, 높은 수준의 사람이 한 명 이상은 필요하다.
				* Case 5. iOS 뿐 아니라 다른 분야도 기웃기웃 해보자 - 다른 분야의 비슷한 개념을 접하고 그 개념을 좀 더 퓨어하게 바라볼 수 있다.
				* Case 6. 책으로 공부한다. -> 각 분야의 뛰어난 사람들이 쓴 것이 책 -> 체계적으로 공부 가능 -> 학생은 책을 많이 못 사니, 도서관이나 리뷰 이벤트 등을 많이 활용해보자 -> 나중에는 원하는 책이 한글로 없어 원서로 넘어간다. -> 번역을 직접 할 기회도 얻게 된다.
				* Case 7. 공식 문서 참조 -> 가장 정확한 자료로 볼 수 있다.
				* 가장 좋은 방법 : 다른 사람에게 설명하는 것! -> 글(블로그)이나 말로 해보기
		* 대안 개발 환경에 대해서는?
			* 모바일 개발을 빠르게 할 수 있을 것 같지만, 요구사항과 현재 스킬셋에 따라 필요가 다르다. -> 뭘 선택해도 어차피 네이티브를 알아야 되기 때문이다.
			* 크로스 플랫폼이 동시 런칭의 답이 아니다
		* iOS 개발자의 미래는?
			* 애플이 망하면 갈아타야지 -> 그래서 공부하는 방법이 필요하다.(망하면 딴 거 빨리 공부해서 갈아타야 되니까)
			* 애플이 잘 될지 망할지는 아무도 모른다.
			* iOS 개발자로 커리어를 시작한다면 어떨까?
				* 장점
					1. 모바일과 데스크탑을 아우르는 선택 범위
					2. iOS 개발자의 공급은 많지 않다. -> 경험있는 사람이 안드로이드나 웹보다 적다 -> 전환 사례도 많다.
					3. 네이티브 개발자의 수요는 반드시 존재한다.
				* 유의점
					* 특정 플랫폼에 종속되지 않고, 개발자로써의 능력을 키워야 한다. -> 회사의 입장에 따라 다른 일을 하게 될 수도 있다. -> 결국은 기본 CS 지식이 곧 기초 체력이다.
		* 
7. Engineering Culture Booth QnA
	1. 네이버의 서비스는 네이버 앱만 있지 않나요?  -> 절대 아니다
		1. 포브스 선정 5년 연속 혁신 기업 Top 10 -> 네이버앱만 하면 절대 나올 수 없는 기록
		2. 자율주행, 로봇 등을 담당하는 Naver Labs
		3. Snow, 제페토 등의 서비스를 담당하는 회사
		4. 라인 웍스
		5. 인공지능 Clova
		6. VLive 
	2. 네이버에서 일하면 좋은 게 있나요?
		1. 최고의 동료와 전문가
		2. 수많은 사용자에게서 오는 실시간 피드백
		3. 1초다마 새롭게 생겨나는 데이터, 그리고 그 데이터를 처리하는  인프라
		4. 개발자 채용 계획 - 8월말 개발자 공채 OPEN 예정