# 建表SQL

## 说明
1. 名字以下划线间隔，表名开头用tb(table),字段开头用f(field),外键开头用fk(foreign key)
2. 主键均命名f_id，并使用UUID生成，以避免并发情况和多字段声明主键问题
3. 所有布尔值默认值为false,
4. 所有外键字段设定NOT NULL非空
5. 部分关键名字字段添加UNIQUE唯一属性
6. 注释##

### User:用户信息
    CREATE TABLE tb_user(
        f_id VARCHAR(36) PRIMARY KEY,
        f_user_name VARCHAR(255) UNIQUE NOT NULL,
        f_password VARCHAR(255) NOT NULL,
        f_email VARCHAR(255) NOT NULL
    );
### visitor:访客
    CREATE TABLE tb_vistor(
        f_id VARCHAR(36) PRIMARY KEY,
        f_ip VARCHAR(255) NOT NULL
    );
### Article:文章
    CREATE TABLE tb_article(
        f_id VARCHAR(36) PRIMARY KEY,
        f_article_name VARCHAR(255) NOT NULL,
        f_read_num INT,
        f_article_text VARCHAR(255),
        f_article_html VARCHAR(255),
        f_create_time DATETIME NOT NULL,
        f_update_time DATETIME NOT NULL,
        fk_user VARCHAR(36) NOT NULL,
        CONSTRAINT FOREIGN KEY (fk_user) REFERENCES tb_user(f_id)
    );
### Tag:标签管理
    CREATE TABLE tb_tag(
        f_id VARCHAR(36) PRIMARY KEY,
        f_tag_name VARCHAR(255) UNIQUE NOT NULL
    );
### 中间表 ArticleTag:文章与标签之间的绑定关系
    CREATE TABLE tb_article_tag(
        f_id VARCHAR(36) PRIMARY KEY,
        fk_article VARCHAR(36) NOT NULL,
        fk_tag VARCHAR(36) NOT NULL,
        CONSTRAINT FOREIGN KEY (fk_article) REFERENCES tb_article(f_id),
        CONSTRAINT FOREIGN KEY (fk_tag) REFERENCES tb_tag(f_id)
    );