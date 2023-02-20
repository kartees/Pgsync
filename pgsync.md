# Pgsync

Synchronize data between two postgres databases 

Note:
- postgres server should be installed
- applicable for databases either in local or remote server

1. Installation 
```
sudo apt update
sudo apt install ruby ruby-dev libpq-dev build-essential
gem install pgsync
```
check installation using `pgsync --version`


2. created two postgres databases 
- test_pgsync_1 with owner as user_one
- test_pgsync_2 with owner as user_two

3. created 2 tables in both test_pgsync_1 and test_pgsync_2 databases
    - names [name (varchar), valuestream (varchar)]
    - department ( dept (varchar), strenght (int) ]

4. Insert some values in the names and department tables on the test_pgsync_1 database


5. Initialized the pgsync using the command `pgsync --init`
- now pgsync.yml is created on the root directory

6. open the .pgsync.yml using the command `vim ~/.pgsync.yml`
- configure the source and destination database connection URLs

source database
- from: postgres://user_one:password@remote_ip:5432/test_pgsync_1
destination database
- to: postgres://user_two:password@remote_ip:5432/test_pgsync_2

- add a line `to_safe: true` on the pgsync.yml file as the destination is not on the local

7. If we want to exclude some tables, configure the exclude section by adding the table names
```
exlude:
- department
```

8. Now run the command `pgsync` to sync the databases from source to destination
   the output will be
```
   From: test_pgsync_1 on 192.168.224.236:5432
   To: test_pgsync_2 on 192.168.224.236:5432
   Completed in 0.2s
```

9. Run `pgsync --list` to check the sync was completed or not