Eclipse Luna PDT x64 다운로드
 
Workspace 지정은 본인이 선호하는 위치로.  
되도록 시스템 드라이브(OS가 설치된)가 아닌 곳으로 설정
 
B'skit 사용할 때의 컨벤션은  
d:\work\workspace_[프로젝트명]_[프로그래밍언어 또는 프레임웍]  
Ex)  
d:\work\workspace_tizen_drupal  
d:\work\workspace_tizen_ruby
   

Preferences --\> General --\> Workspace --\> Encoding : UTF-8  
Preferences --\> General --\> Workspace --\> Line Delimiter : Unix  
Preferences --\> General --\> Editors --\> Text Editors --\> Insert spaces for tabs : check  
Preferences --\> PHP --\> Editor --\> Save Actions --\> Remove trailing whitespaces : check, All lines : check
   

Eclipse 플러그인 설치(drupal용 컨텐트 타입 설정하는 플러그인)  
Eclipse install url : [http://xtnd.us/downloads/eclipse](http://xtnd.us/downloads/eclipse)  
Market url : [http://marketplace.eclipse.org/content/drupal-eclipse-pdt/](http://marketplace.eclipse.org/content/drupal-eclipse-pdt/)
 
이 플러그인으로는 .profile 확장자가 연동 안됨.  
Preferences --\> General --\> Content Type 메뉴  
--\> Text --\> PHP Content Type 선택  
--\> 'Add' 버튼 눌러서 *.profile 추가
   

Preferences --\> PHP --\> Code Style --\> Formatter --\> Import 후 아래 파일 선택

![[drupal code conventions formatter v0.1.xml]]

형상관리
 
개발서버의 소스를 기준으로 형상관리  
로컬에서의 작업은 소스/DB를 복제하여 개발서버와 분리된 상태로 작업
 
url : [http://bliex.com:82/svn/~~~~](http://bliex.com:82/svn/~~~~)
 
drush dl module_filter  
drush en module_filter
    
drush dl ctools  
drush en views_content, term_depth, stylizer, page_manager, ctools_plugin_example, ctools_custom_content, ctools_ajax_sample, ctools_access_ruleset, bulk_export, ctools
    
drush dl views  
drush en views_ui
   

drush dl media  
drush dl medua_youtube  
drush en media_youtube  
y
 
drush dl admin_menu  
drush en admin_menu_toolbar  
y  
drush dis toolbar  
y

- Module Filter
    - [https://www.drupal.org/project/module_filter](https://www.drupal.org/project/module_filter)
    - [http://ftp.drupal.org/files/projects/module_filter-7.x-2.0-alpha2.tar.gz](http://ftp.drupal.org/files/projects/module_filter-7.x-2.0-alpha2.tar.gz)
- Devel
    - [https://www.drupal.org/project/devel](https://www.drupal.org/project/devel)
    - [http://ftp.drupal.org/files/projects/devel-7.x-1.5.tar.gz](http://ftp.drupal.org/files/projects/devel-7.x-1.5.tar.gz)
- Chaos Tool Suite
    - [https://www.drupal.org/project/ctools](https://www.drupal.org/project/ctools)
    - [http://ftp.drupal.org/files/projects/ctools-7.x-1.6.tar.gz](http://ftp.drupal.org/files/projects/ctools-7.x-1.6.tar.gz)
- Views
    - [https://www.drupal.org/project/views](https://www.drupal.org/project/views)
    - [http://ftp.drupal.org/files/projects/views-7.x-3.10.tar.gz](http://ftp.drupal.org/files/projects/views-7.x-3.10.tar.gz)
- Entity API
    - [https://www.drupal.org/project/entity](https://www.drupal.org/project/entity)
    - [http://ftp.drupal.org/files/projects/entity-7.x-1.5.tar.gz](http://ftp.drupal.org/files/projects/entity-7.x-1.5.tar.gz)
- Administration Menu
    - [https://www.drupal.org/project/admin_menu](https://www.drupal.org/project/admin_menu)
    - [http://ftp.drupal.org/files/projects/admin_menu-7.x-3.0-rc5.tar.gz](http://ftp.drupal.org/files/projects/admin_menu-7.x-3.0-rc5.tar.gz)

Acquia 설치

- [https://www.acquia.com/downloads](https://www.acquia.com/downloads) 에서 Acquia Dev Desktop 2 를 다운로드
- 또는 [http://www.acquia.com/sites/default/files/downloads/dev-desktop/AcquiaDevDesktop-2-RC-2015-01-23.exe](http://www.acquia.com/sites/default/files/downloads/dev-desktop/AcquiaDevDesktop-2-RC-2015-01-23.exe)
- 설치 경로는 기본값으로,
- Sites folder 는 D:\work\devdesktop 으로 설정
- Apache port : 8083
- MySQL port : 33067
- 설치 후 Dev Desktop 실행(방화벽 경고시 방화벽 해제)
- Start from Scrach 선택
- Acquia Drupal 7.34 버전 선택해서 설치   
   

프로젝트 생성  
PHP Project 선택하여 기본값으로 프로젝트 생성  
프로젝트 속성 --\> PHP --\> Build Path --\> Link source… --\> 드루팔 소스 디렉토리 지정
   

Formatter xml 은 계속 보완해 나갈 예정.