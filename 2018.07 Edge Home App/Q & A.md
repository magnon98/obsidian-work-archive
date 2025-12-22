1. Menu Tree 추가 ￼현재의 IA(정보구조가 복잡하지 않고 따라서 Spoke UI형태로 모두 수용가능하기 때문에, 굳이 메뉴트리를 추가하여 공간을 차지할 필요는 없다는 의견이나, 차후에 추가될 메뉴를 감안하여 미리 구조를 만들어두고자 함이라면 OK. 3. Landscape, Portrait 화면 모두 표시 ￼현재 문서의 Landscape view외에, Portrait view도 목업이 필요하다는 의미인지? 현재 문서는 정보 구조와 기능, flow 등을 설계한 wireframe이기 때문에, 레이아웃(가로/세로뷰를 포함한)은 디자인 단계에서 확인 및 논의 가능함 
    1. Portrait 로 변경 시 Icon 크기는 작게 변하는게 적합 ￼실제 (7인치 화면) 실장하게될 디바이스에서의 UX를 고려하면 ICON 사이즈나, 카드뷰의 영역 사이즈등은 변경되지 않는 것이 옳음 ￼--\> 가로 / 세로 중 어느쪽에 더 비중을 둘지 결정 필요. 5. Touch Screen에서 Long Press 정의 필요 ￼터치 환경에서의 Long Press는 마우스를 사용하는 non-touch 사용 환경에서의 동작 이벤트와 매핑되어야 함. 마우스 오버와 매핑한다면, 가능한 부분은 카드뷰에서의 hover시, 전체 정보 표시￼--\> 일반적으로는 롱프레스 =~ 우클릭, ￼--\> 5-3 하고 엮어서 생각해보면 롱프레스를 마우스의 hover 와 매핑하는 정도… ￼--\> 사용자가 정해져 있어 경험이 쌓이면 괜찮겠지만, 여러 마우스 액션을 롱프레스에 엮는건 바람직하지 않음. 7. Back to Home 을 Home Icon으로 대체 ￼사용환경을 고려하여 Graphic Resource 사용을 최소화 하려는 의도였으나, 현재 사용 가능 용량이 어느정도 확보되었음. 아이콘으로 대체 OK￼--\> 이미지를 사용하게 되면 아무래도 리소스 사용 측면이나, 체감 속도가 조금 더 느려질 수 밖에 없음. 미묘한 차이지만, 페이지 로딩 기준이 1초라…. 9. User Container 카드뷰 화면 (2페이지) 
    1. User Container 중 Link 가능한 Container만 선택 가능 해야 함 ￼이해하는 바가 맞다면, 카드뷰에서 상세화면으로 보내는 링크와 외부 링크가 동시에 존재하면 되지만, 아래 6번과 관련하여 '상세화면' 존재 여부에 따라 달라질 것으로 보임￼--\> 컨테이너의 상세 정보 조회는 필요 없는 것인지
      
    3. 각 컨테이너의 State 정보 정보는 Up or Exit ￼현재 TBD / 확정되는 대로 변경 예정￼--\> 임시로 running / exited 로 표현중
      
    5. 생성일자를 Image Name으로 변경 (일부 화면 표시 하고 Mouse 등 Focus 가져가면 전체 정보 표시) ￼생성일자보다는 Image..의 정보가 더 표시 우선순위가 높은 것으로 이해하겠음 / Image..관련 string이 길기 때문에, 일부만 표시하고 hover(마우스)나 롱프레스(터치) 시, 전체 정보를 툴팁 형태로 띄워주는 것으로 진행
      
    
10. User Container 상세 화면 (3페이지) 
    1. User Container Details 대신 컨테이너 이름 표시 ￼OK
      
    3. Header 와 Body 로 구분하여 Header에 Container이름 및 로케이션 표시 ￼'로케이션'은 무엇을 의미하는지? / 제공되는 로케이션 정보가 있다면 이름과 함께 표시 가능￼--\> frame을 위 아래로 나누라는 의미인지???￼--\> reverse proxy이기 때문에 frame 외에는 header 영역을 정의할 방법이 없음.￼--\> 로케이션 정보는 어디에 있는지? container env?
      
    5. Body 에 Container의 index.html 표시 ￼현재 Service, Web UI 등등의 내용과 전혀 다른 정보를 의미하는지 확인이 필요하며, 이에 따라 상기 5번 a항목의 Link에 대한 것도 정확한 결정이 가능할 것으로 보임
      
    
11. 디바이스 정보 및 설정 화면 (4페이지)
    1. Save 버튼 Icon으로 대체 ￼아이콘으로 대체 OK
      
    3. Restore Icon 버튼 추가 (초기 값으로 Restore) ￼아이콘 형태로 추가하겠음 / 초기 값은 '공장 초기화'의 개념으로 이해했음￼--\> devicemgmt.RestoreDevice() 에 호출하는게 맞는지?￼￼
      
    5. 각 Section을 Fold 형태로 하면 어떨지요? (공유된 EQ UX Guide 참조)
        1. 만약 Fold 형태가 어렵다면 Scroll은 Header 이하 부터 위치하는게 적합 ￼데스크탑 환경이라면 Header이하부터 스크롤링 되는 것이 일반적이나, 사용 환경 자체가 작은 화면을 보는 형태이기 때문에 전체 스크롤을 사용하였음 / Critical한 이슈는 아님
          
        3. 각 항목별로 Save/Restore 버튼 ￼여러개의 항목을 한 번에 수정하는 경우가 있을 것으로 판단하여 전체 Save를 넣었으나, 실제 Use Case가 그렇지 않다면 항목별로 버튼을 두는 것으로 OK￼--\> 항목별 Save / restore 만 있는 것인지, 전체에 대한 save / restore 도 필요한지?￼--\> restore는 devicemgmt.RestoreDevice() 호출이 아닌 Web UI 상에서 수정 전 상태로 돌리는 것을 말하는지?
          
        
    6. 수정 필요 사항
        1. Wifi / Ethernet 의 Enable/Disable 상호 배타 적이어야 함 (둘 중 하나만 선택 가능하도록 수정 필요) ￼OK 
          
        3. Wifi / Ethernet 항목에서 Enable/Disable 버튼이 각 항목에서 가장 위에 위치 하도록 수정 ￼OK / 더불어 Enable/Disable에 따라 하위에 포함되는 옵션들이 모두 활성/비활성 동작하는 것으로 이해하겠음￼--\> 리눅스 시스템은 기본적으로 텍스트 기반 설정이라 enable / disable 에 관계 없이 각 속성에 대한 설정은 가능한데, disable 되었을 때는 각 속성도 disable 하라는 것인지?
          
        
    7. Save 후 결과 값 표시
        1. 수정된 항목에 대해서만 결과 값을 받아 표시 ￼OK / 수정된 '값'은 제외하고 '항목'만을 표시하여 처리 (e.g. 'Ethernet' Changes Saved successfully.)￼--\> 개별 항목들에만 save 가 있다면 문제 없음.￼--\> 전체에 대한 save 도 필요하다면 표현을 어떻게 할지?
      
    
12. 브라우져 팝업 메시지 (6 Page)
    1. Popup은 공유된 EQ UX Guide 의 Popup과 동일한 형태로 변경 필요 ￼원래 사용환경의 리소스&퍼포먼스 이슈로 팝업은 브라우저 기본 팝업을 사용할 계획이었나, 문제가 없다면 레이어 팝업을 사용 하겠음
      
    3. Leave this page 와 Stay in this page 위치 변경 ￼OK
      
    5. Stay this page -\> Stay in this page로 변경 ￼OK
      
    
13. 기타
    1. Virtual Keyboard를 사용시 체 화면의 50% 미만으로 위치 하는게 좋으며, Menu 의 Back 버튼과 Keyboard의 Back 버튼 충돌 이슈 있으므로 조정 필요 ￼OS에서 제공하는 Virtual Keyboard는 수정이 불가한 영역으로 보는 것이 좋음 / '버튼 충돌 이슈'는 단순 화면상에서의 겹침을 의미하는 것인지, 기능상의 충돌의 의미하는 것인지? (Keyboard의 Back버튼으로 브라우저 Back버튼이 동작한다던가..)￼--\> 웹에서는 IME를 제공하지 못함. 몇몇 솔루션이 있으나 완성도 판단이 힘듬.￼--\> chrome 에서는 back 버튼으로 이전페이지 이동이 불가능해졌음. Chromium도 마찬가지 (사실 충돌이슈는 history.back() 하지 않아 발생하는 코딩 오류)