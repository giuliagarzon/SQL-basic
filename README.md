# SQL-basic
http://search.maven.org/#search|ga|1|hive%20serde%20xml
https://github.com/dvasilen/Hive-XML-SerDe/wiki/XML-data-sources
hive.apache.org
maven.org


Crear una tabla en XML:

add jar hdfs:/tmp/hivexmlserde-1.0.5.3.jar;
CREATE external TABLE books(book_id string, author string, title string, price string, publish_date string)
ROW FORMAT SERDE 'com.ibm.spss.hive.serde2.xml.XmlSerDe'
WITH SERDEPROPERTIES (
"column.xpath.book_id"="/book/@id",
"column.xpath.author"="/book/author/text()",
"column.xpath.title"="/book/title/text()",
"column.xpath.price"="/book/price/text()",
"column.xpath.publish_date"="/book/publish_date/text()"
)
STORED AS
INPUTFORMAT 'com.ibm.spss.hive.serde2.xml.XmlInputFormat'
OUTPUTFORMAT 'org.apache.hadoop.hive.ql.io.IgnoreKeyTextOutputFormat'
location '/tmp/books'
TBLPROPERTIES (
"xmlinput.start"="<book",
"xmlinput.end"="</book>"
);

Funciones de strin:

substring

select count(author) as frecuencia, author from books_csv group by author order by frecuencia ASC;
regexp_replace(price, "[\$]","")
regexp_extract(var, "()")
split(var., delimitador)[]
regexp_extract(author, "(.*),(.*)",1)
