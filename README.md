# ejabberd
Install Ejabberd in Centos7

install the required library
 - yum install glibc

 download and install ejabberd
  - wget https://www.process-one.net/downloads/downloads-action.php?file=/ejabberd/19.05/ejabberd-19.08-0.x86_64.rpm
  - rpm -ivh ejabberd-19.08-0.x86_64.rpm
  
  configure database, install if not exist
   - mysql -u root -p
   - CREATE DATABASE ejabberd;
   - GRANT ALL ON ejabberd.* TO 'ejabberd'@'localhost' IDENTIFIED BY 'mypass';
   - FLUSH PRIVILEGES;
   - EXIT;
   
   login to database as ejabberd user
   - mysql -u ejabberd -p
   - USE ejabberd;
   - SOURCE /opt/ejabberd-19.05/lib/ejabberd-19.08/priv/sql/mysql.sql;
   - EXIT;
   
   edit the ejaberd config
   - vi /opt/ejabberd/conf/ejabberd.yml   
      
    // insert to eof
     sql_type: mysql   
     sql_server: "localhost"  
     sql_database: "ejabberd"  
     sql_username: "ejabberd"  
     sql_password: "mypass" 
     
    // add your hostname  
    
    hosts:  
       - "localhost"
       - "myhostname.com"  
    
    acl -> "admin" -> "user"  
       - "admin@myhostname.com"
     
    api_permissions -> "public commands" -> "who"
       ip: 192.168.3.101/32
    
    - :wq
    
    
   
