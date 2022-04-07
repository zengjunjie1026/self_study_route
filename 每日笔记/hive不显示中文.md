 (1)、进入数据库 Metastore 中执行以下 5 条 SQL 语句 

 ①修改表字段注解和表注解
alter table COLUMNS_V2 modify column COMMENT varchar(256) character set utf8
alter table TABLE_PARAMS modify column PARAM_VALUE varchar(4000) character set utf8
② 修改分区字段注解：
alter table PARTITION_PARAMS modify column PARAM_VALUE varchar(4000) character set utf8 ;
alter table PARTITION_KEYS modify column PKEY_COMMENT varchar(4000) character set utf8;
③修改索引注解：
alter table INDEX_PARAMS modify column PARAM_VALUE varchar(4000) character set utf8;

 (2)、修改 metastore 的连接 URL

<property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://IP:3306/db_name?createDatabaseIfNotExist=true&amp;useUnicode=true&characterEncoding=UTF-8</value>
    <description>JDBC connect string for a JDBC metastore</description>
</property>