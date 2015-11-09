#指令

**創database**

    CREATE xxxxdb
**給某user權力**

    GRANT ALL ON xxxxdb.* TO '<user>'@'localhost' IDENTIFIED BY '<password>';
**換database**

    USE xxxxdb
**列出database中的table們**

    SELECT table_name FROM information_schema.TABLES;
**列出某table中的欄位**

    SELECT column_name FROM information_schema.columns where table_name="???";
**條件的列出table裡某些欄位的值，或是有多個table(可以分別取a, b...)**

    SELECT a.tx_id,a.tx_nTime FROM tx a WHERE a.tx_nTime > 1437023500 LIMIT 10 OFFSET 5;
-WHERE: 條件
-LIMIT: 取幾個
-OFFSET: 從符合該條件的第幾個開始取

#語法

<a href="http://www.codedata.com.tw/database/mysql-tutorial-basic-query">
    MySQL 超新手入門（3）SELECT 基礎查詢
</a>

要照順序  
<table>
    <tr>
        <td>SELECT</td>
        <td>想查詢的欄位（*表示全部）</td>
    </tr>
    <tr>
        <td>FROM</td>
        <td>想查的TABLE</td>
    </tr>
    <tr>
        <td>WHERE</td>
        <td>查詢條件</td>
    </tr>
    <tr>
        <td>GROUP BY</td>
        <td>分組設定</td>
    </tr>
    <tr>
        <td>HAVING</td>
        <td>分組條件</td>
    </tr>
    <tr>
        <td>ORDER BY</td>
        <td>排序條件</td>
    </tr>
    <tr>
        <td>LIMIT</td>
        <td>限制</td>
    </tr>


