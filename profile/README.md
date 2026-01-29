
 # MOPL - 콘텐츠 디스커버리 & 소셜 플랫폼                                                                                                                                                     
                                                                                                                                                                                              
 MOPL 프로젝트의 백엔드 시스템을 구성하는 레포지토리 모음입니다.                                                                                                                              
<img width="1297" height="728" alt="image" src="https://github.com/user-attachments/assets/e5b7df26-a1c2-4e6c-8d3b-622a19f6e75a" />

## 프로젝트 일정
<img width="980" height="543" alt="image" src="https://github.com/user-attachments/assets/aaa8fa99-8fcb-43c5-b8a0-6294c186d500" />
                                                                                                                                                                                              
                                                                                                                                                                                              
 ## 레포지토리 개요                                                                                                                                                                           
                                                                                                                                                                                              
 ### spring - 메인 API 서버                                                                                                                                                                   
                                                                                                                                                                                              
 Spring Boot 3.5.9 기반의 멀티모듈 프로젝트로, 두 개의 서브모듈로 구성됩니다.                                                                                                                 
                                                                                                                                                                                              
 - **mopl-core**: 콘텐츠 관리, 사용자 인증(JWT/OAuth2), 플레이리스트, 리뷰, 팔로우 등 핵심 REST API를 제공합니다. PostgreSQL, Elasticsearch, Redis를 데이터 저장소로 사용합니다.              
 - **mopl-websocket-sse**: 알림, 다이렉트 메시지, 실시간 함께보기(Watching Session) 등 실시간 통신 기능을 WebSocket과 SSE로 제공합니다. Kafka를 통해 이벤트를 처리합니다.                     
                                                                                                                                                                                              
 Nginx가 리버스 프록시로 두 서비스의 트래픽을 라우팅합니다.                                                                                                                                   
                                                                                                                                                                                              
 **기술 스택**: Java 21, Spring Boot, Spring Security, Spring Data JPA, QueryDSL, MapStruct, Kafka, Elasticsearch, Redis, PostgreSQL                                                          
                                                                                                                                                                                              
 ### batch - 콘텐츠 수집 배치                                                                                                                                                                 
                                                                                                                                                                                              
 Spring Batch 기반의 배치 애플리케이션으로, 외부 API에서 콘텐츠 데이터를 수집하여 DB에 저장합니다.                                                                                            
                                                                                                                                                                                              
 - **TMDB API**: 영화 및 TV 프로그램 데이터 수집                                                                                                                                              
 - **TheSportsDB API**: 스포츠 이벤트 데이터 수집                                                                                                                                             
 - 수집된 콘텐츠의 썸네일을 AWS S3에 업로드하고, 중복 검사 및 태그 처리를 수행합니다.                                                                                                         
                                                                                                                                                                                              
 **기술 스택**: Java 21, Spring Boot, Spring Batch, PostgreSQL, AWS S3, Prometheus PushGateway                                                                                                
                                                                                                                                                                                              
 ### monitoring - 모니터링 스택                                                                                                                                                               
                                                                                                                                                                                              
 Prometheus + Grafana 기반의 모니터링 인프라로, Docker Compose로 구성됩니다.                                                                                                                  
                                                                                                                                                                                              
 - Spring API, WebSocket 서버, Batch 작업, PostgreSQL, Elasticsearch의 메트릭을 수집합니다.                                                                                                   
 - 시스템 개요, 도메인 개요, Batch 모니터링, API별 성능 모니터링 등 6개의 사전 구성된 Grafana 대시보드를 포함합니다.                                                                          
                                                                                                                                                                                              
 **구성 요소**: Prometheus, Grafana, Pushgateway, PostgreSQL Exporter, Elasticsearch Exporter         

## 시스템 아키텍처
<img width="1284" height="592" alt="image" src="https://github.com/user-attachments/assets/317ffaa8-4086-4907-a0e5-d05a92016f17" />

## 배포 
https://mopl.cloud
