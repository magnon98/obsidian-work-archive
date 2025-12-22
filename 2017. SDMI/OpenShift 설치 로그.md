sudoer 설정  
고정 IP 설정  
호스트명 변경  
ssh-key 설정  
hosts 설정  
업데이트  
openshift-ansible clone (사용한 commit id: 6528031d5ec24d62ffe28687bb134bc1237f0210)  
ansible 스크립트 수정  
/home/magnon/openshift-ansible/roles/openshift_master_certificates/tasks/main.yml  
[from]  
- name: Lookup default group for ansible_ssh_user  
  command: "/usr/bin/id -g {{ ansible_ssh_user | quote }}"  
  changed_when: false  
  register: _ansible_ssh_user_gid  
- set_fact:  
    client_users: "{{ [ansible_ssh_user, 'root'] | unique }}"
 
[to]  
- name: Lookup default group for ansible_ssh_user  
  command: "/usr/bin/id -g root"  
  changed_when: false  
  register: _ansible_ssh_user_gid  
- set_fact:  
    client_users: "root"  
설치 진행