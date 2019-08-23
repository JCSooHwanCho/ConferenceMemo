# Let us go! 2019 summer
1. 누구나 할 수 있다! Networking
	1. Rest 의 구성
		1. 자원, 행위, 표현
			* 클라이언트가 자원, 행위를 담아 보내면 서버가 표현을 반환
			* URI : 자원에 해당, 인터넷의 자원을 나타내는 유일한 요소
			* 메소드
				* CRUD: Post,Get,Put,delete
			* 표현 : 반환 값 (200,400,500 등)
	2. alamofire vs moya  
		* 동기와 비동기  - data(contentsOf:) vs datatask 
		* Alamofire - URLSession을 래핑, 더 이쁜 코드 작성 가능
		* Moya : 내부적으로 alamofire 사용, 양은 많아 보여도 깔끔하게 적용 가능 -> 핵심 코드가 엄청 간결해졌다
2. 인디앱 수입으로 월세 내기 
	* 	만들었던 앱
		1. QuickMemo
		2. BearFocusTimer
		3. Bear BucketList
	* 2년동안 약 1억 -> 사람들이 환불해가고, 애플에서 떼가고 디자이너랑 나누면 별로 안됨
	* Featured는 중요하다!
		* 개발자의 영역
			1. Error Free
			2. iOS Native
			3. Continuous update
			4. Using Apple's technology & Feature
		* 기타 영역
			1. 앱스토어 설명 - 카테고리 설정 
			2. 리뷰피드백
			3. 홍보 및 노출
			4. Promote 요청
	* 	좋은 기획  + 멋진 구현 + 지속적인 노출 + 지속적인 업데이트 = Profit!
3. ARKit 3 톺아보기  
	* 	key-Point
		1. 더욱 쉬워진 개발
		2. 드디어 들어온 사람
	* 	 더욱 쉬워진 개발
		* 새로운 renderer로 RealityKit을 사용 가능
		* RealityKit의 구성요소
			* ARView 와 Scene 
			* Anchor - ARKit과 현실을 연결하기 위한 기준점
			* Entity - 가상에 물체를 표시하기 위한 요소들
		* Reality Composer 추가 -> 쉽게  AR을 만들 수 있는 앱
	* 드디어 들어온 사람
		* People Occlusion - 가상 물체가 사람 뒤에 렌더링 될 수 있도록 하는 기술  -> 깊이 추정을 활용
		* A12칩 이상에서만 사용 가능
		* 구성하기
			* ARSession 객체 구성
			* frameSemantics 옵션으로 People Occlusion 기능 설정 가능
		* Motion Capture
			* 사람 몸을 tracking 
			* 역시  A12부터 적용가능
		* 그 외
			* ARCoachingView
			* 앞뒤 동시 tracking
			* 다중 face tracking
			* 100장 이장의 이미지 동시 처리
4. iOS 프리랜서로 산다는 것 - GitHub ClintJang
	* 	iOS 프리랜서?
		* 프리랜서란?
			* 특정 회사에 계약으로 고용되지 않고 일하는 사람
			* 법적으로는 '인적용역 사업자' 
		* 경력 기술 양식(이력 문서)
			* 경력 기술서
			* 개인 이력 카드
			* 포트폴리오
		* 개발자 등급 -> 폐지됨 (경력 인증 하고자 했는데, 부작용 발생)
			* 하지만 현업에서는 여전히 분류한다.
			* 초급, 중급, 고급, 특급
		* 계약금액 -> 민감하다...
			* 월단위
				* 초급 : 350 ~ 450 -> 근데 너무 겸손해서 그 이하로 받는다
				* 중급 : 450 ~ 550 -> 보통 520 ~ 600
				* 고급 : 650 ~750 - > 보통 600 ~ 700
				* 특급 : 부르는 게 값이다... 자리도 많이 없다.
				* 지방, 해외면 체제 비용 등이 추가
			* 능력 되면 인맥이나 사이트 통해서 더 벌 수도 있겠지... 
		* 계약서
			* 종류가 다양하지만, 동의했다는 사실만 증빙하면 효력이 있음
			* 문제가 생겼을 때 증빙하는 수단으로 사용 -> 프리랜서로 할꺼면 진짜 잘 챙겨야 된다.
			* 사본 꼭 챙기자.
		* 세금/실수령액 -> 3.3%만 공제
			* 많이 버는데? 
				* 퇴직금, 4대 보험, 고용 불안 등등의 문제점은 스스로 해결해야 함
		* 구인 과정
			1. 이력서 오픈
			2. 전화 대기
			3. 전화 받기 -> 개발자 등급, 계약 급여
			4. 1차 거르기
			5. 지원하기 - 개인 이력 카드
			6. 인터뷰 진행
			7. 구체적인 기간 조건 협상/ 확인
			8. 저울질
			9. 계약서 사본 받기 -> 검토
			10. 확정 혹은 타협(및 거절)
			11. 투입
			12. 투입 1~3일 -> 마지막 선택
			13. 근무 중 -> 월급이 잘 들어와야지...
			14. 완료 -> 2주 전에 연장 혹은 만료 결정
	* 마무리
		* 국내 개발자 - 25만명, 프리랜서는 2.6만명
		* 왜 프리랜서요? - 저임금, 조직 스트레스 등...
		* 좋은 점 - 자유롭다!, 돈 많이 벌어, 원하는 일만 할 수 있다. 장기 휴가 가능....
		* 아쉬운 점 - 고용 불안, 휴가 사용 불편, 잦은 계약서 협의... 공실율, 쉬면 돈 X 등...
		* 프리랜서 특성상 피동적인 역할을 맡을 수 밖에 없게 된다는 점이 아쉬움
		* 직장은 우리를 평생 책임져주지 않는다.
5. Combine vs RxSwift  
	* RxSwift - observable stream을 이용한 비동기 프로그래밍  API
	* Combine - apple의  Rx
	* 비교
		* 지원 버전 : iOS 8 vs 13
		* platform :  애플 플랫폼 공통적으로 지원, Linux vs UIKit for Mac
		* 서드 파티 vs 퍼스트 파티
		* 빠른 피드백, OS 업데이트 필요 없음 vs private API이용 가능, 성능 상 이점, 용량 상 이점
		* RxCocoa vs SwiftUI
	* Rx의 Observable, Combine 의 Publisher
		* class vs protocol(AnyPublisher는 struct)
		* publishSubject vs Passthrough subject
		* behaviorSubject vs currentValueSubject
		* subscribe vs sink
		* bind vs subscribe
		* disposable vs cancellable
		* disposeBag vs (없음, cancellable 을 배열로 만들어야 한다.)
		* observeOn vs receive(on:)
		* subscribeOn vs subscribe(on:)
		* Combine은 아직 완전하지 않다... 테스트 해보고 도입하자.
6. 그래요 저 비전공 개발자에요  
	* 개발자는 디자인을 배워야 할까요?
		* 개발자가 주로 만나는 디자인 - UI/UX
	* 디자인이 개발자에게 어떤 도움을 줄까?
		1. 속도 향상
		2. 협업 기술 향상
		3. 수익 창출
	* 어떻게 잘 할 수 있을까?
		1. 디자이너에게 물어보기
		2. 앱스토어 살펴보		3. dribbble.com 참		4. mobbin.design
		5. designnotes.com 
		6. 8포인트 그리드 시스템 - 일관성을 위해 필요			* 화면 해상도가 대부분 8의 배수이다.
	* 마치며
		* 스킬 배울 필요는 없다.
7. RxSwift internal - Disposable
	*  Observable을 중단하는 법
		1. completed나  error 이벤트
		2. dispose호출
		3. disposeBag 비우기
	* 	 subscribe 함수의 반환형 : Disposable
	* Disposable은 어떻게 Observable을 중단시킬까?
		* Disposable 의 구조
			* protocol Disposable -> 안에는 dispose 함수 선언
			* Disposables -> disposable 타입의 팩토리 객체
				* create() ->NopDisposable 반환
				* create( ()->Void) ->AnonumousDisposable
					* AnonymousDisposable : 클래스, 받은 클로저를 실행
						* DisposeBase, Cancelable 클래스를 상속
						* DisposeBase -> 사실 아무 기능 없음
						* Cancelable : disposable 을 상속하는 프로토콜, dispose 된 Observable이 더이상 이벤트 발생을 못하게 막음
			*  create() 의 구현부 -> 클로저를 받아AnonymousObservable 을 리턴
		* SinkDisposer - cancelable 프로토콜 채택
			* AnonymousObservable에 Sink를 전달, 해당 Sink를 통해 dispose를 수행 가능
			* 사용자가 돌려받게 되는 disposable 이 sinkDisposer
		* 종료 이벤트(completed, error) 발생시
			* (sink,disposable) 를 sinkDisposer가 받아 두 개 다 dispose시킴
		*  DisposeBag -> DisposeBase 상속
			* 메모리에서 사라질 때에 dispose됨(dispose가 private)
		* compositeDisposable: Disposable을 합치는 기능  
	* cf) [GitHub - intmain/DismissDisposable](https://github.com/intmain/DismissDisposable)

8. WWDC CheatSheet
	* Swift, Foundation, SwiftUI, Data, ML, AR,Vision, UI, etc...
	* Swift - What's new in swift5
		* ABI and Module  stability
		* Launch overhead 0%
		* 코드 사이즈 10% 줄임, 최대 15%
		*  브릿징 속도 상승
		*  Docker swift 공식 지원
		* LSP 소개
		* 기타 등등...
	* Foundation - Advances in Foundation
	* SwiftUI 
		* Introducing SwiftUI: Building Your First App
		* SwiftUI Essentials
		* building custom views in swiftUI
	* Data
		* Data Flow Through swift
		* Introducing Combine
	* ML 
		* What's new in Machine Learning
		* Create ML For Object Detection and Sound Classification
		* Desigining Great ML Experiences
	* Vision
		* understanding Images 
	* UI
		* Moderize your UI for iOS13
	* 기타
		* Cryptography and your apps
		* What's new in clang and llvm
		* Great Developer habits