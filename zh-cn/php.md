## Application

#### 读取Application
```php
XN_Application::$CURRENT_URL = "admin";
$app = XN_Application::load();
echo $app->debugString();
```

#### 创建Application
```php
XN_Profile::$VIEWER = null;
$application = 'admin';
$props = array('name' => $application,'description' => 'oldhand '.date("Y-m-d H:i:s").' create.');
$app = XN_Application::create($application,$props);  
```
application 为纯英文字母的应用关键词<br>
description 为当应用的描述<br>
#### 修改Application
```php
XN_Application::$CURRENT_URL = "admin";
$app = XN_Application::load();
$app->trialtime = "2020-01-01"; //应用有效时间
$app->active = "true";  //应用激活
$app->owner = XN_Profile::$VIEWER; //应用创建者
$app->save("application");
echo $app->debugString();
```

## Profile
#### 创建Profile
```php
$email = date("YmdHis")."@tezan.cn";
$password = "123qwe";
$mobile = "159".date("dHis");
$username = "admin_".date("Y_m_d_H_i_s"); 	
try 
{
	$profile = XN_Profile::create ( strtolower(trim($email)), $password );  //用户邮箱，唯一
	$profile->fullname = strtolower($username); //用户登录账号 唯一
	$profile->mobile = trim($mobile);  //用户手机号码
	$profile->status = 'True';	 
	$profile->type = "register";
	$profile->save ("profile");
	echo  '测试创建用户['.$username.']成功<br>';
}
catch ( XN_Exception $e ) 
{
	echo  '测试创建用户['.$username.']失败['.$e->getMessage().']!<br>';
	die();
} 
```
#### 读取Profile
```php
try 
{
	$profileid = "q5s71tfc18d"; //用户ID, 自动生成，36进制数字，短唯一字符串。
	$profile_info = XN_Profile::load ($profileid,'id',"profile");	
	echo "测试获取用户[".$profileid."]成功!<br>";
}
catch(XN_Exception $e){
    echo "测试获取用户[".$profileid."]失败[".$e->getMessage()."]!<br>";
} 
```
#### 批量读取Profile
```php
try 
{
	$ids = array("q5s71tfc18d","hx5eyjjmlg6");
	$profiles = XN_Profile::loadMany ($ids,'id',"profile");	
}
catch(XN_Exception $e){
    echo "测试获取用户失败[".$e->getMessage()."]!<br>";
} 
```

#### 修改Profile
```php
try 
{
	$profileid = "q5s71tfc18d";
	$profile_info = XN_Profile::load ($profileid,'id',"profile");	
	$profile_info->password = date("YmdHis");	  
	$profile_info->givenname = "admin";       
	$profile_info->save();	
	echo "测试保存用户[".$profileid."]成功!<br>";
}
catch(XN_Exception $e){
    echo "测试保存用户[".$profileid."]失败[".$e->getMessage()."]!<br>";
} 
```

#### 条件查询Profile
```php
try{
	$profiles = XN_Query::create ( 'Profile' ) ->tag("profile")
					 	 ->filter ( 'published', '>=', '2018-01-01 00:00:00' )
						 ->filter ( 'published', '<=', date("Y-m-d").' 23:59:59' )
						 ->order("published",XN_Order::DESC)
				   	     ->begin(0)
				   	     ->end(5)
						 ->execute();

	 if (count($profiles) > 0)
	 {
		 echo '通过查询,测试获取用户成功<br>'; 
		 foreach($profiles as $profile_info )
		 {
			 echo '通过查询,测试获取用户数据ID:'.$profile_info->profileid . ' =>  '.$profile_info->givenname.'<br>';
		 }
	 }
}
catch(XN_Exception $e){
  	 echo "通过查询,测试获取用户失败 : ".$e->getMessage() . '<br>'; 
} 
```

#### 统计Profile记录数
```php
try{ 
	$query = XN_Query::create ( 'Profile_Count' ) ->tag("profile")
		->filter ( 'published', '>=', '2018-01-01 00:00:00' )
		->filter ( 'published', '<=', date("Y-m-d").' 23:59:59' ) 
		->end(-1);
	$query->execute(); 
	echo "统计用户记录个数成功 : ".$query->getTotalCount(). '<br>'; 
}
catch(XN_Exception $e){
  	echo "统计用户记录个数失败 :".$e->getMessage() . '<br>'; 
}  
```

#### 分组统计Profile
```php
try{ 
		$query = XN_Query::create('Profile_Count')->tag('profile') 
			->filter ( 'published', '>=', '2015-01-01 00:00:00' )
			->filter ( 'published', '<=', date("Y-m-d").' 23:59:59' ) 
			->filter('type','!=','')
			->rollup()
			->group('type')
			->order("count",XN_Order::DESC_NUMBER) 
			->order("type",XN_Order::ASC);    
		$query->begin(0);
		$query->end(10);
	    $statistics = $query->execute(); 
	 echo '分组统计用户记录个数成功<br>'; 
	 foreach($statistics as $statistic_info )
	 {
		 echo '分组统计用户记录个数获得数据ID:'.$statistic_info->my->type . ' =>  ' . $statistic_info->my->count . '<br>';
	 } 
}
catch(XN_Exception $e){
  	 echo "分组统计用户记录个数失败 :".$e->getMessage() . '<br>'; 
}  
```


## Content
#### 创建Content

```php
try{ 
	$profileid = '1234';
	$newcontent = XN_Content::create('friends','',false); //friends 为数据库表名
	$newcontent->my->tabid = '10000';
	$newcontent->my->profileid = $profileid;
	$newcontent->my->fieldid = '10000'; 
	$newcontent->my->fieldname = 'test';
	$newcontent->my->visible = '0'; 
    $newcontent->my->readonly = '1';  
	$newcontent->save('friends');  //friends 为缓存标签，创建数据时，需要清除相关的缓存标签
	echo "向Content插入记录成功 : ".$newcontent->id . '<br>'; 
}
catch(XN_Exception $e){
  echo "向Content插入记录失败 :".$e->getMessage() . '<br>'; 
}

```
**注意create创建函数的参数**
```php
/**     
 * @param $type string the content type 
 * @param $title string an optional title
 * @param $anonymous Whether to save it as anonymous or not
 * @param $datatype 0 => content, 1 => bigcontent, 2 => mq,4 => maincontent,5 => schedule 
 * @param $datatype 6 => message,7 => yearcontent,9 => yearmonthcontent
 */
public static function create($typeOrNode, $titleOrXpath = null, $anonymous = true,$datatype = 0) 
```
$datatype代表不同的Content表类型
 * 0 => content,  全索引表，适合数据量小的场景
 * 1 => bigcontent,  按天存储自定义索引表
 * 2 => mq, 消息队列，具体用法附后
 * 4 => maincontent,  自定义索引表，索引需要自己配置
 * 5 => schedule  调度表，当你需要自行写SQL进行操作时，具体用法附后
 * 6 => message,  消息通知表
 * 7 => yearcontent,  按年存储的自定义索引表
 * 9 => yearmonthcontent 按月存储的自定义索引表




####  通过ID读取Content

```php
try{
	$contentid = 1234; // 每条记录有唯一的ID, 请确保记录存在
	$info = XN_Content::load($contentid,'tabs'); //tabs为缓存标签
	echo "获取记录成功 : ".$info->id . '<br>'; 
}
catch(XN_Exception $e){
  echo "获取记录失败 :".$e->getMessage() . '<br>'; 
}

```
**注意load函数的参数**
```php
/**     
     * @param $content string|XN_Content|array a string content ID, XN_Content object
     * @param $datatype 0 => content, 1 => bigcontent, 2 => mq,4 => maincontent,5 => schedule 
	 * @param $datatype 6 => message,7 => yearcontent,9 => yearmonthcontent
     */
public static function load($content,$tag = null,$datatype=0)  
```
$datatype代表不同的Content表类型,与Content创建函数相同。
 
####  批量读取Content
```php
try{
	$ids = array("1111","2222","3333");
	$orders = XN_Content::loadMany($ids,"mall_orders");
}
catch(XN_Exception $e){
  echo "获取记录失败 :".$e->getMessage() . '<br>'; 
}

```

####  修改并保存Content

```php
	try{
		$contentid = 1234; // 每条记录有唯一的ID, 请确保记录存在
		$info = XN_Content::load($contentid,'tabs');
		$info->my->visible = 'true'; 
	    $info->my->readonly = 'false'; 
		$info->save('tabs');
		echo "更新记录成功 : ".$info->id . '<br>'; 
	}
	catch(XN_Exception $e){
	  echo "更新记录失败 :".$e->getMessage() . '<br>'; 
	} 

```



## 按年分表的Content

## 按月分表的Content

## 按天分表的Content



## 自定义SQL调度(schedule)

## 消息队列(MQ)


