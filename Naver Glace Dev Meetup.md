#네이버 GLACE Dev. Meetup

---

1. GLACE CIC(네이버 지도 서비스)에서는 이렇게 가고 있습니다 
	* 네이버 앱 : 컨텐츠(웹 페이지, 동영상)를 잘 보여주기 위한 것,
		* 비슷한 컨셉의 서비스들은  대부분 네이버 앱에 흡수되는 중
	* 네이버 지도는 네이버 앱과는 다른 성격
		* 장소에 대한 정보와 검색 기능을 제공
		* 경로 탐색 기능
		* 대중교통 정보를 모으고 사용자들에게 제공
			* 지하철 노선도를 따로 만든다
		* 위성 사진을 비롯한 다양한 지도 정보를 제공
			* 거리뷰 & 항공뷰
		* 네이버 지도 앱
		* vector 맵으로의 전환 준비중(app은 이미 완료, web은 20년 중)
		* 글로벌 지도 준비중
		* 거리뷰 데이터를 통한 다양한 서비스 준비중
			* 길찾기에 활용(분기점에 활용)
		* 내비게이션 서비스를 강화예정
		* 대중교통 길안내
		* 커버리지가 넓다...
		* 항상 최신 데이터를 유지해야만 한다.
			* 조금만 뒤쳐지도 쓸모가 없어진다.
	* 개발 역량이 다양하게 필요하다.
		* Computer Science
		* Map Dev
		* Backend
		* FrontEnd

2. 네이버 지도 API, 요람에서 무덤까지 - API 제작, 배포, 운영 과정 -  API Life Cycle에 맞춰서
	1. 디자인  : 대세 따르는 게 아니라 왜 이 기술이 필요한 지 설득해야 한다. -> 토론과 협의
		* 	기술 스택
			* 메인 스트림 - sprint, mysql, intelliJ, NGinx
			* 일부 도입/ 레거시 -  node.js, kotlin, 몽고 db, cassandra, 아파치 웹 서버, 이클립스, Go 등..
		* 인프라
			* Reliabilty : fault tolerance -> Hystrix
			* Scalability: scale up vs scale out
			* message platform -> kafka
		* 네이밍 
	2. 개발 단계 
		* Skeleton 만들기, Mock api
		* 이슈 쪼개기 -> 한 이슈는 3일 이내
		* git flow
		* code review
		* CI/CD
		* Sprint 2주~4주, Iterations
	3. 테스트
		* QA
		* Regression Test : 실제 Production log 기반
		* Performance Test  ([ngrinder](https://github.com/naver/ngrinder))
		* 가용량 점검, 증설  
	4. 배포
		* Load Balance : 여러 대의 서버가 있을 때 한 쪽에 트래픽이 몰리지 않도록 하는 것
		* Blue / Green Deploy : 버전에 따라 Blue(옛 버전), Green(새버전)으로 나누어, 점진적으로 새 버젼으로 이동시키는 것
		* A/B테스팅 
		* 서버모니터링 : Nagios, Zabbix, Prometeus, in k8s
		* API 모니터링 : pinpoint
		* 로그 수집 : ELK, GA, Firebase
		* 데이터 분석 : Spark, zeplin
	5. 은퇴 : 사실상 없다 -> 예전 API를 사용하는 경우가 있어서, 부담되지 않는 선에서 계속 관리한다.

3. 네이버 지도를 지탱하는 기술 - 아틀라스 플랫폼
	1. 지도플랫폼의 필요 기능
		1. 다양하고 정밀한 데이터를 저장하고 꺼내쓸 수 있는 저장소
		2. 데이터 정제
			* 하천 레이어 경량화
			*  dissolve
			* 분할 (clipping) 
		3. 모양 만들기  - 레이어링, 스타일링
			* 지도 제착 툴 필요 - Arcmap, QGIS등
			* 네이버는 자체 제작한 툴(Catalog) 사용(협업, 디버깅 용이) -> 오픈된 툴은 아니다. 내년 중에는 사내로, 내후년에는 일반인 대상으로 오픈 할 예정
		4. 지도 렌더링/ 타일링  	
	2. 좋은 플랫폼의 4대 조건
		1. 최소한의 서버로 대용량 트래픽을 처리
		2. 내장애성
		3. 확장과 변경의 용이성
		4. 손 쉬운 사용
	3. 네이버 Atlas의 구조 -> 사진 참조

4. 네이버 지도 길찾기 API - 내비게이션 적응기 
	* Traffic Intelligence
		* 최신 교통정보와
		* 도로네트워크 데이터, 위치 정보를 기반으로
		* 사용자에게 현실의 정보를 바탕으로 가장 효율적인 경로를 제공
			* 최신이 아닌 데이터 - 부정확, 비효율적인 경로 제공
			* 위치정보 - 도보, 차량 여부에 따라 다른 데이터 제공
	* 교통정보 생성
		* 실시간 소통정보 / 패턴 소통정보 생성
			* 차량 궤적 정보 -> 맵 매칭 -> 소통정보 -> 길찾기 결과 / 화면 표시 반영
		* 맵 매칭 고도화  - 잘못된 정보를 정제
			* 각도를 감안한 전이 확률 
			* 소요시간 결과 정제 - 동일 도로 통과 소요시간에 대한 클러스터링을 통한 이상값 제거
		* 궤적정보 기반 맵 업데이트 
			* 신규도로 탐지
	* 길찾기
		* 난점
			* 네비게이션용 데이터의 복잡함 -> 기존 JSON에 넣기는 어려움
			* 다양한 플랫폼에서의 사용 - 플랫폼마다 줘야할 데이터 형태가 다를 수 있다.
		* 구조 설계
			* API 다양화 : 필요한 정보만 최적화시키기
		* 길찾기 알고리즘
			* 다익스트라 + A* 단일경로
			* Bi-directional 탐색으로 다양한 경로 동시 찾음
		* 빠른 응답속도

5. 네이버 지도 앱은 다른 앱과 이런게 다릅니다.
	* 	모바일 앱 : 벡터 맵 SDK(Maps Mobile SDK) + 네비게이션 SDK + iOS/AOS 앱 개발
	* 벡터 맵 SDK
		* 지원 플랫폼 : 안드로이드, iOS, centOS
		* 사용 언어 : 자바, 코틀린,  C++, obj-c, Swift
		* 그래픽스 : OpenGL-ES, Metal, Vulkan -> 알면 쉬운데, 모르면 어렵다...
	* 내비게이션 SDK 
		* GPS 데이터로 위치 판단
		* 경로 추적
		* 애플리케이션에서 표시
	* 애플리케이션
		* 검색
		* 내비게이션
		* POI(Point of Interest)
		* 크래시를 막기 위한 많은 테스트
	* 결론 : Naver maps 개발자는 다른 앱 개발자들이 경험하지 못하는 많은 것들을 경험할 수 있다.