- AD 연동  
- AD 연동 관련 현재 구성된 현황, 상태 및 예상되는 문제점 식별 필요  
- MySQL 사용자 정보 table 확인한 결과 JIRA / Confluence / Crowd 별로 사용자를 관리하는 것으로 보이며, 단일 사용자 그룹으로 일괄 관리하는 것이 가능한지 확인 필요  
--\> Jira 및 Confluence은 솔루션, 단독으로 작동할 수 있는 별개의 제품  
--\> 사용자 정보는 Jira 및 Confluence 의 각종 컨텐츠에서 사용되고 있어 DB 구조상 불가능
    
- DOOSAN AD group 인 Confluence-users / jira-software-users group 에 crowdadmin 관리자 계정으로 사용자 계정 관리작업이 가능한지 확인 필요  
- DDI 에서 작업 시 해당 관리 계정으로 group에 사용자 정보 관리가 제한적이었음을 확인하였지만 후속 조치 상황이 파악되지 않음  
--\> 현재 AD 연동에 사용하는 방식은 'Delegated Authentication'으로 AD 정보는 인증에만 사용되고, 그룹 정보는 사용할 수 없습니다.  
그룹 정보를 사용하려면 'Delegated Authentication' 으로 변경전에 사용했던 Connector 방식을 사용해 연동하여 AD와 Crowd, Crowd와 Jira / Confluence 간의 데이터를 주기적으로 동기화 해야 합니다.
      

- 프로젝트 별 관리 담당자 지정을 위한 confluence-administrator / jira-administrator 그룹 추가 필요 여부  
--\> 프로젝트별 담당자라면 해당 프로젝트에 대해서만 권한이 있어야 할 것이기 때문에 하나의 그룹으로 묶을 수는 없습니다.  
프로젝트 담당자는 개별 유저에 대해 role 을 부여하거나 프로젝트별 담당자 그룹을 만들어 role을 부여해야 합니다.  
현재는 100 유저 라이센스이기 때문에 개별 유저를 대상으로 하는 것이 더 효율적일 것입니다.
   

- CI / CD 연동  
- Github / Jenkins 대상으로 연동 설정 구성 현황  
- Git-repo 구성 및 deploy 설정 설명 및 현황 전달 필요  
--\> 프로젝트마다 git repo, jenkins job 이 모두 다를 것이기 때문에 CICD 연동은 프로젝트 단위로 수행됩니다.  
샘플로써는 구성이 가능하지만, 모든 프로젝트에 글로벌하게 적용되도록 할 수는 없습니다.  
플러그인 단순 설치는 가능.  
git, jenkins 플러그인은 무료 버전도 있음.
    
- SSL 적용  
- SSL 적용을 요청하였지만 세부 진행 계획 확인되지 않음  
--\> 인증서 필요하고 준비되면 route에 추가한다고 말씀드렸습니다
      

- 메일 서버 설정 정보 확인  
- 관리 계정 crowdadmin@doosan 으로 관리용 이메일이 사용 가능함  
- SMTP 서버 ip 10.224.49.221 (krrelay.corp.doosan.com)  
- 계정 crowdadmin@doosan.com  
--\> 기 설정되어 있는 것 확인하였습니다.
      

- Addon 구성 및 어플리케이션 설정  
- Team calendar / redaction / gliffy diagram 구축 현황 및 사용자 문서  
--\> 설치된 상태. 사용자 문서는 어떤 것? 사용법?
      

- Teams for jira , mobility for jira 등의 addon 설정 가능 여부  
--\> Teams for jira는 Teams 에서 설정하는 것...  
프로젝트 범위를 벗어나는 것 같은데…  
시도해 보았으나 에러 발생해서 진행 불가
 
--\> 모빌리티는 트라이얼 버전으로 설치 완료  
[https://www.mobilityforjira.com/instructions/#step_2](https://www.mobilityforjira.com/instructions/#step_2)
       
- JIRA / Confluence / Crowd 백업 기능 구성 여부  
--\> 백업은 일일백업(XML 방식)으로 수행. 새벽 2시로 설정.  
JIRA:  
- 메뉴: Administration \> System \> Advanced \> Services  
- 파일 경로: /var/atlassian/jira/export  
Confl:  
- 메뉴: Administration \> Scheduled Jobs \> Back Up Confluence  
- 파일 경로: /var/atlassian/confluence/backups  
Crowd:  
- 메뉴: Administration \> Backups  
- 파일 경로: /var/atlassian/crowd/shared/backups
      

- MySQL OCP vnet 내부에 이전 구성에 따른 DB 설정 및 migration
      

- 구축 및 구성 관련 작업 이력  
- 블릭스 소프트 내부 작업 현황 자료 혹은 별도의 형태로 제공 방안 협의 필요  
--\> 작업 이력은 계속 정리중
      

- 간헐적인 오류 현상  
- 서버 접속 끊김 : 504 gateway time-out (SMTP 서버 설정 확인 중 자주 발생함)  
- AD 로그인 실패 : 간헐적으로 발생함  
- Jira 상당 메뉴 표시 오류 : application link 선택 아이콘이 2줄 형태로 간헐적으로 표시됨  
- Tinymce 미지정 오류 resource url : ….  
--\> crowd, jira, confl 모두 4번 노드에 올라와 있는데  
현재 4번 노드가 안티바이러스에 의해 간헐적으로 부하가 걸려 발생되는 문제.  
오후에 심하고, 17시 경부터 상태 좋아짐...;;
    
- Sw update 및 tech support 방안 제공 필요  
--\> 새로운 버전으로 앱 생성 및 초기 설정 후 XML 백업파일 이용하여 복원. 첨부파일은 단순 복사  
--\> 테크 서포트는 OCP 와 같은 형태로 가능. 계약과 관련해서는 아는 바 없음.
      

- 사용자 문서 (아키텍처, 매뉴얼, 설정 정보 등) 제공 필요  
--\> 아키텍쳐.... 그릴 게 없는데... OCP 아키 위에 그리기?  
--\> 솔루션이기 때문에 별도 작성되는 매뉴얼은 없음.  
--\> 설정 변경한 내용은 설치보고서에 추가.