# WWDC19 톺아보기 - KxCoding
1. 개발자가 놓치면 안되는 새로운 기능들
	1. iOS13
		1. Dark Mode 지원
			1. RGB Color -> Semantic Color  : 라이트 모드와 다크 모드의 컬러와 에셋을 별도로 준비해야 함
			2. SF Symbols : 기존 SF Symbols도 다크모드 지원
		2. Modal Presentations : 화면 전체를 덮는 것에서 카드 형태로 겹쳐지도록 변경 -> Swipe down으로 화면 닫을 수 있음(그래도 이전처럼 명시적인 화면 닫기 기능은 제공되어야 함 -> 리젝 사유)
		3. Contextual menus : 기존 Peek&pop(3d touch 전용)을 대체함 -> 3d touch가 없는 디바이스에서도 사용가능(특히 macOS)
	2. iPadOS
		1. 멀티태스킹 - 1개의 앱이 여러 인스턴스를 가질 수 있다.
		2. UIWindowScene API :UILifeCycle을 담당하는 게 기존 AppDelegate에서 SceneDelegate로 분리 됨
		3.  PencliKit
	3. WatchOS : StandAlone앱 가능 : 기존에는 iPhone앱이 반드시 필요했음 
	4. Sign in with Apple : 서드파티 로그인 기능이 존재하면 반드시 이 기능을 추가해야 함
		1.  API가 사용하기 쉬움
		2. private한 이메일 주소 사용 - 보안성
		3. 제공받은 이메일이 올바른 이메일 주소임을 애플이 보증(Anti-Fraud)
		4. 크로스 플랫폼
	5. Swift 5.1
		1. ABI Stability(5.0 이상) - 다른 버전으로 컴파일해도 호환 가능! -> Obj-C 시한부
		2. Module Stability(5.1 이상) - 서로 다른 컴파일러가 만든 모듈이라도 호환성이 보장됨
		3. Shared Swift Runtime - OS에  swift런타임이 내장
			1. 앱 초기실행 오버헤드 사라짐
			2. 코드 사이즈 감소(그냥 해도 10%, 최적화하면 최대 15%까지)
			3. 성능 향상
		4. Swift Package Manager : Xcode에 내장

2. SwiftUI - 선언형 프레임워크 
	* 키워드 - Less Code, Automatic
	1. 	최소 요구사항 - 최소 2년의 버퍼(보수적인 분야라면 더 오래걸리겠지)
		1. iOS 13+
		2. Catalina+,
		3. XCode11+
	2. 눈 여겨볼 사항
		1. 사용하기 위해서 프로젝트 생성시에 SwiftUI 사용 체크(수동으로 추가하는 법도 있을까?)
		2. Preview는 기본적으로 비활성화 -> resume버튼으로 활성화
		3. Preview에서 직접 편집 가능 -> 코드에도 자동 반영(코드,프리뷰,어트리뷰트 인스펙터 3창이 자동으로 싱크됨)
		4. 속성을 변경하는 방법이 메소드로 일원화(modifier로 불림, View마다 제공하는 modifier를 drag&drop으로 추가 가능)
		5. cmd+click으로 Contextual Menu 띄우기 가능 -> modifier 적용가능
		6. resume 버튼을 누르면 자동으로 빌드
		7. 라이브 모드 지원 -> 시뮬레이터 실행 필요 없이 변경사항을 실시간으로 확인 가능
		8. View가 프로토콜이고, 실제 뷰는 View프로토콜을 채택한 struct로 구현됨 -> 런타임 오버헤드 거의 없음( ARC가 없기 때문) -> 최대한 잘게 쪼개 구현하는 것이 권장됨
		9. View 프로토콜은 body속성 하나만 가지고, body 속성에 원하는 대로 구현해주면 갱신이 필요할 때마다 body에 접근해서 자동으로 갱신함
		10.  swiftUI를 만들면 구조체가 2가지 생김 -> 하나는 본체, 하나는 Preview를 띄우기 위한 구조체
		11.  여러개의  Preview를 띄우는 게 가능(여러개 띄우면 느려져서 아직 최적화가 필요하다)
			1. Preview별로 별도의 환경설정 적용 가능(다크 모드 등)
			2. 여러가지 레이아웃으로도 적용 가능(device도 여러 modifier의 적용을 받음)
		12. Identifiable - Id라는 Int 상수 속성을 부여함으로, Identifier로 적용
		13. swiftUI 파일 추가 - UI 항목의 swiftUI  파일 추가
		14. struct의 property로 데이터를 선언하여 사용 -> 생성자로 데이터를 넘긴다.
		15. 조건문으로 제어 가능
		16. delegate,datasource 필요없는 tableView
		17. Preview에서도 Body와 동일한 테크닉 적용가능 -> Preview 에서만 필요한 모습을 쉽게 적용가능
		18. SceneDelegate의 rootViewController 설정하기 ->  Storyboard의 initialViewController를 대체
		19. environment override 버튼 - 동적으로 환경설정 기능(Ligth,Dark모드 등)
		20. Asset의 Apperance 설정 - Any,Light,Dark Asset이 필요함
		21. Semantic Color - System이 붙은 Color들은  Light,Dark등에 자동으로 대응해줌
		22. UIHostingController - 기존 스토리보드와 혼용을 가능하게 해줌
		23. AutoLayout이 없어졌다.
	3. 알아두어야할  struct 및 Protocol
		1. View - 모든 View의 기본이 되는 프로토콜
		2. Text - UILabel 대체
		3. Image - UIImage 대체
		4. VStack,HStack - UIStackView대체
		5. Spacer
		6. List - UITableView대체
		7. Identifiable - tableView의 항목들을 유일하게 식별하기 위해 적용해야할 프로토콜 -> Id라는 let Property 필요(Int,String등이 모두 가능)
		8. NavigationView - UINavigationViewController를 대체
		9. NavigationLink - 네비게이션에서의 Segue를 대체

3. Project Catalyst -> iPad 앱을 macOS 앱으로 포팅하는 기술(2020년 or 2022년 쯤 완성될 예정)
	1. 호환이 안되던 이유 - 기반 프레임워크가 달라서! -> 현재는 대부분 통합되어가는 추세
	2. UIKitforMac
		1. 제한 사항 : Universal앱이여야 함(iPhone 전용 앱 X), 모바일 전용 기능 사용 불가
		2. 사용법 : device에서 mac 체크 -> 타켓을 my mac으로 설정 후 실행
		3. iOS에서의 모든 컨트롤이 macOS에 맞게 포팅 됨
		4. 수동으로 추가해줘야 할 것들 : macApp 용 아이콘, 터치바 요소, 메뉴바 요소 등...
	3. API 분류
		1. 동일한 기능을 보장하는 API
		2. macOS에 적합하게 기능이 변하는  API
		3. 사용 불가능한 API -> targetEnvironment(UIKitforMac)으로 사용 가능한지 체크를 해야한다.
			1. Deprecated framework -> 모든 프레임워크를 최신화시켜야함
			2. iOS-specific frameworks -> ClassKit,HealthKit 등
			3. Hardware-specific frameworks -> ARKit, CarPlay,VisionKit  등
4. Xcode 11
	1. Editor 옵션 버튼 위치 이동(전체 창의 우측 상단 -> 에디터 창 우측 상단), 새로운 에디터 추가 가능(기존에는 보조 에디터만 추가 가능)
	2. 파일 여는 방식의 변화 (Option+shift + 파일클릭 -> 화살표로 인디케이터 조정 -> return -> 새로운 에디터로 열림)
	3. 포커스 모드 추가(특정 에디터만 크게 보는 기능)
	4. 미니맵 기능 추가 -> 빠르게 네비게이션 가능
	5. Environment override 버튼 - Light/dark기능, text크기, Accesibility 기능 추가
	6. Swift Package Manager 추가 
		* File -  Swift Package - Add Package Dependancy
		* GitHub 와 연동됨

5. Combine FrameWork -> Rxswift의 애플버전
	1. 비동기 인터페이스를 구현할 때 좀 더 간단하게 적용하기 위한 방법
	2. 최소 요구사항 :  SwiftUI와 동일 -> 당장은 Rxswift를 공부해라.  Rx 잘 해놓으면  Combine도 수월하다
	3. 중요 컨셉 : Publisher,Subscribers,Operator(각각 Observable, Observer,Operator에 대응) -> Protocol로 구현되어 있다
		1. publisher protocol : 주로 struct로 구현 ->  Foundation 에는 이미 Combine으로 Publisher구현이 대부분 되어 있다
		2. subscriber protocol: 주로 class로 구현(상태 변화에 주로 쓰기 때문에) -> subscriber  protocol의  extension으로 주요한 class들이 구현이 되어 있다.
		3. @published (property wrapper -> 5.1부터 추가) : property를 published로 만들어 줌,  $연산으로 published에서 publisher를 꺼내 사용
			* cf) @State,@Environment 
		4. receive(on:) : observeOn을 대체
		5. assign : 바인딩하기
		6. AnyCancellable : Disposable에 대응(메모리 관리는 프로그래머가 직접)
		7. 