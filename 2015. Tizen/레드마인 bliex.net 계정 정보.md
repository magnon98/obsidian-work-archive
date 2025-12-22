MySQL  
root // 개인기본  
redmine // redmine
 
RED MINE  
admin // admin
   

메일 발송용 gmail
 
bliextizen@gmail.com  
Qmfflrtm
   

Create user 'tizen'@'%' identified by 'xkdlwps';  
grant all privileges on *.* to 'tizen'@'%';

DB table name 에 prefix 설정
 
$ cd /var/www/redmine-2.5.0/config  
$ cp additional_environment.rb.example additional_environment.rb  
$ vi additional_environment.rb
 
config.active_record.table_name_prefix = 'r_' 추가 후 저장
   

redmine_ 로 지정했더니  
특정 컬럼의 인덱스 길이가 64를 넘어가서 에러 발생함 ㅠㅠ
 
==Index name 'index_redmine_custom_fields_projects_on_custom_field_id_and_project_id' on table 'redmine_custom_fields_projects' is too long; the limit is 64 characters/usr/local/rvm/gems/ruby-1.9.3-p551/gems/activerecord-3.2.17/lib/active_record/connection_adapters/abstract/schema_statements.rb:573:in `add_index_options'==

설치시 참고 문서  
ruby는 기존 것 지우고 1.9.3으로 설치 필요.  
[http://www.redmine.org/projects/redmine/wiki/Install_Redmine_25x_on_Centos_65_complete](http://www.redmine.org/projects/redmine/wiki/Install_Redmine_25x_on_Centos_65_complete)

Drupal
 
tizen // xkdlwps
   

Redmine  
admin // admin