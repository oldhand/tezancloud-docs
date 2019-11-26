**Content即文档数据库**<br>

## 简单Content示例
```xml
<entry xmlns="http://www.w3.org/2005/Atom" xmlns:xn="http://localhost/atom/1.0" xmlns:my="http://localhost/xn/atom/1.0">
<id>77</id>
<xn:id>77</xn:id>
<xn:application>admin</xn:application>
<xn:type>tabs</xn:type>
<title type="text">admin</title>
<published>2019-11-26 09:32:35</published>
<updated>2019-11-26 09:32:35</updated>
<author><name>q5s71tfc18d</name></author>
<datatype>0</datatype>
<my:childmodule xn:type="string"></my:childmodule>
<my:presence xn:type="string">0</my:presence>
<my:tabid xn:type="string">114</my:tabid>
<my:tablabel xn:type="string">公告</my:tablabel>
<my:tabname xn:type="string">Announcements</my:tabname>
<my:tabsequence xn:type="string">129</my:tabsequence>
</entry>
```
```json
{
	"id":"77",
	"xn_id":"77",
	"xn_application":"admin",
	"xn_type":"tabs",
	"title":"admin",
	"published":"2019-11-26 09:32:35",
	"updated":"2019-11-26 09:32:35",
	"author":"q5s71tfc18d",
	"childmodule":"",
	"presence":"0",
	"tabid":"114",
	"tablabel":"公告",
	"tabname":"Announcements",
	"my:tabsequence":"129"
}
```
一个简单的文档数据，用xml与json分别展示文档数据记录。

## Content 有固定的系统字段
   id： 数值型自增字端，<br>
   xn_id： 与id完全相同，兼容需要，<br>
   xn_application： 字符型数据，所属应用<br>
   xn_type: 字符型数据，所属数据库表<br>
   title: 字符型数据，数据标题<br>
   published: 日期型数据，记录创建时间<br>
   updated: 日期型数据，记录最后更新时间<br>
   author: 字符型数据，记录创建者，与Profile关联<br>
   datatype: 数值型数据，数据表类型，如按年，按月，队列，等多种类型<br>
   
   
## Content 特性
  * 所有的content都有唯一的ID,关联时，不需要知道表名，只需要知道ID即可
  * 固定的基本字段，简化了程序开发
  * 每条记录的字段数灵活，写入的是什么，读出的就是什么
  * 字段动态生成，不需要进行数据库管理，简化数据库兼容性管理
  * 字段支持数组写入，同时支持数组查询，简化数据库设计
  
     
   
   
   
   