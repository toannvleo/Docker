# Hướng dẫn  build và run container oracle database 12c

- Bước 1: Tải hình ảnh cơ sở dữ liệu 12.1.0.2 từ repository về

```
$ docker pull toannvleo/oracle-database:12.1.0.2-ee
``` 

- Bước 2: Tạo và gán quyền thư mục để lưu trữ dữ liệu cơ sở dữ liệu

```
$ mkdir oradata
$ chmod a+w oradata
```

- Bước 3: Tạo và chạy container cơ sở dữ liệu 12.1.0.2

```
docker run --name c_db_oracle -p 1521:1521 -v /home/oracle/oradata:/opt/oracle/oradata toannvleo/oracle-database:12.1.0.2-ee
```

# Cac cau lenh chay

```
su root 
nano /etc/sudoers
user_name ALL=(ALL)  ALL

sudo chmod 666 /var/run/docker.sock
sudo usermod -aG docker ${USER}


$ mkdir oradata
$ chmod a+w oradata
$ docker run --name c_db_oracle -p 1521:1521 -v /home/vtoan/oradata:/opt/oracle/oradata toannvleo/oracle-database:12.1.0.2-ee


cd $ORACLE_HOME
cd network/admin/
cat tnsnames.ora

sqlplus sys/S0QLjokXWqU=1@ORCLCDB as sysdba
alter session set "_ORACLE_SCRIPT"=true;
GRANT CREATE SESSION TO HIS_RS;
sudo rm -r directory

alter user system identified by orcl;

select username as schema_name from sys.all_users;
```