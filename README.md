WORDPRESS INSTALLATION WITH ANSIBLE
=========

Bu proje bir sunucu içerisine mariadb, php ve nginx kurulumu gerçekleştirip üzerine wordpress'i yapılandırarak kullanıcıyı CLI tarafındaki konfigürasyonlarla uğraştırmadan ve hata yapma olasılığını sıfırlayarak wordpress deneyimi yaşaması için yazılmıştır.

Kullanımı için yapılması gereken tek şey bir ansible'a sahip olmak ve bu projenin uygulanacağı sunucuyu host'u olarak tanımlamak yeterli. Rollerin dışındaki main.yaml dosyası çalıştırıldığında bizden isteyeceği bazı değişkenler var. Bu değişkenler dışında geri kalan işlemler ansible taskları halinde halledilecektir. Kullanıcıya kalan değişkenler kısmında girdiği domain adresine gitmek olacak.

`
root@pandorika wordpress]# ansible-playbook main.yaml -K
BECOME password: 
[DEPRECATION WARNING]: The firewalld module has been moved to the ansible.posix collection. This feature will 
be removed from community.general in version 2.0.0. Deprecation warnings can be disabled by setting 
deprecation_warnings=False in ansible.cfg.
Domain name: : hitit.cloud
Database root name:: naneci123
Wordpress database name:: wordpress_db
Wordpress database user:: wordpress_user
Wordpress database user password:: wordpress_pass

PLAY [cent8] ***************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************
ok: [cent8]

TASK [mariadb : Install required package] **********************************************************************
[DEPRECATION WARNING]: Invoking "dnf" only once while using a loop via squash_actions is deprecated. Instead of
 using a loop to supply multiple items and specifying `name: "{{ item }}"`, please use `name: ['mariadb', 
'mariadb-server', 'python3', 'python3-PyMySQL']` and remove the loop. This feature will be removed from 
ansible-base in version 2.11. Deprecation warnings can be disabled by setting deprecation_warnings=False in 
ansible.cfg.
changed: [cent8] => (item=['mariadb', 'mariadb-server', 'python3', 'python3-PyMySQL'])

TASK [mariadb : Mariadb Start Service] *************************************************************************
changed: [cent8]

TASK [mariadb : Install pymysql] *******************************************************************************
ok: [cent8]

TASK [mariadb : Create .my.cnf] ********************************************************************************
changed: [cent8]

TASK [mariadb : Set the root password] *************************************************************************
changed: [cent8]

TASK [mariadb : Delete anonymous mysql.user] *******************************************************************
ok: [cent8]

TASK [mariadb : Remove test database] **************************************************************************
[WARNING]: Module did not set no_log for unsafe_login_password
ok: [cent8]

TASK [mariadb : Create wordpress database] *********************************************************************
changed: [cent8]

TASK [mariadb : Create user for wordpress database] ************************************************************
changed: [cent8]

TASK [php : Install required package] **************************************************************************
[DEPRECATION WARNING]: Invoking "dnf" only once while using a loop via squash_actions is deprecated. Instead of
 using a loop to supply multiple items and specifying `name: "{{ item }}"`, please use `name: ['php-cli', 'php-
fpm', 'php-mysqlnd', 'php-dom', 'php-simplexml', 'php-xml', 'php-xmlreader', 'php-curl', 'php-exif', 'php-ftp',
 'php-gd', 'php-iconv', 'php-json', 'php-mbstring', 'php-posix', 'php-sockets', 'php-tokenizer']` and remove 
the loop. This feature will be removed from ansible-base in version 2.11. Deprecation warnings can be disabled 
by setting deprecation_warnings=False in ansible.cfg.
changed: [cent8] => (item=['php-cli', 'php-fpm', 'php-mysqlnd', 'php-dom', 'php-simplexml', 'php-xml', 'php-xmlreader', 'php-curl', 'php-exif', 'php-ftp', 'php-gd', 'php-iconv', 'php-json', 'php-mbstring', 'php-posix', 'php-sockets', 'php-tokenizer'])

TASK [php : Change CGI.FIXPATH] ********************************************************************************
changed: [cent8]

TASK [php : Change www.conf file] ******************************************************************************
changed: [cent8]

TASK [nginx : Disable SELinux] *********************************************************************************
[WARNING]: SELinux state temporarily changed from 'enforcing' to 'permissive'. State change will take effect
next reboot.
changed: [cent8]

TASK [nginx : Install required package] ************************************************************************
[DEPRECATION WARNING]: Invoking "dnf" only once while using a loop via squash_actions is deprecated. Instead of
 using a loop to supply multiple items and specifying `name: "{{ item }}"`, please use `name: ['nginx', 'tar', 
'unzip']` and remove the loop. This feature will be removed from ansible-base in version 2.11. Deprecation 
warnings can be disabled by setting deprecation_warnings=False in ansible.cfg.
changed: [cent8] => (item=['nginx', 'tar', 'unzip'])

TASK [nginx : Start Nginx service] *****************************************************************************
changed: [cent8]

TASK [nginx : Add firewall http service] ***********************************************************************
changed: [cent8]

TASK [nginx : Add firewall 80/tcp port] ************************************************************************
changed: [cent8]

TASK [nginx : Firewall Restart Service] ************************************************************************
changed: [cent8]

TASK [nginx : Create directory for public html] ****************************************************************
changed: [cent8]

TASK [nginx : Create directory for logs] ***********************************************************************
changed: [cent8]

TASK [nginx : Copy Configuration File] *************************************************************************
changed: [cent8]

TASK [nginx : Download wordpress files] ************************************************************************
changed: [cent8]

TASK [nginx : Copy wordpress file to public html] **************************************************************
changed: [cent8]

TASK [nginx : Copy wp-config file] *****************************************************************************
changed: [cent8]

TASK [nginx : Recursively change ownership of a directory] *****************************************************
changed: [cent8]

TASK [nginx : Change database name in wp-config.php] ***********************************************************
changed: [cent8]

TASK [nginx : Change database user in wp-config.php] ***********************************************************
changed: [cent8]

TASK [nginx : Change user passwords in wp-config.php] **********************************************************
changed: [cent8]

TASK [nginx : Nginx Restart Service Handler] *******************************************************************
changed: [cent8]

RUNNING HANDLER [php : PHP-FPM Start Service Handler] **********************************************************
changed: [cent8]

RUNNING HANDLER [php : PHP-FPM Restart Service Handler] ********************************************************
changed: [cent8]

PLAY RECAP *****************************************************************************************************
cent8                      : ok=32   changed=28   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   

`