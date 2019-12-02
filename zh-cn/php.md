## Application

* 读取Application
```php
XN_Application::$CURRENT_URL = "admin";
$app = XN_Application::load();
echo $app->debugString();
```

* 创建Application
```php
XN_Profile::$VIEWER = null;
$application = 'admin';
$props = array('name' => $application,'description' => 'oldhand '.date("Y-m-d H:i:s").' create.');
$app = XN_Application::create($application,$props);  
```

* 修改Application
```php
XN_Application::$CURRENT_URL = "admin";
$app = XN_Application::load();
$app->trialtime = "2020-01-01";
$app->active = "true";
$app->owner = XN_Profile::$VIEWER;
$app->save("application");
echo $app->debugString();
```

## Profile
* 创建Profile
```php
$email = date("YmdHis")."@tezan.cn";
$password = "123qwe";
$mobile = "159".date("dHis");
$username = "admin_".date("Y_m_d_H_i_s"); 	
try 
{
	$profile = XN_Profile::create ( strtolower(trim($email)), $password );
	$profile->fullname = strtolower($username);
	$profile->mobile = trim($mobile);
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
* 读取Profile
```php
try 
{
	$profileid = "q5s71tfc18d";
	$profile_info = XN_Profile::load ($profileid,'id',"profile");	
	echo "测试获取用户[".$profileid."]成功!<br>";
}
catch(XN_Exception $e){
    echo "测试获取用户[".$profileid."]失败[".$e->getMessage()."]!<br>";
} 
```
* 批量读取Profile
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

* 修改Profile
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

* 条件查询Profile
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

* 统计Profile记录数
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

* 分组统计Profile
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
* 创建Content

```php
try{ 
	$profileid = '1234';
	$newcontent = XN_Content::create('friends','',false);
	$newcontent->my->tabid = '10000';
	$newcontent->my->profileid = $profileid;
	$newcontent->my->fieldid = '10000'; 
	$newcontent->my->fieldname = 'test';
	$newcontent->my->visible = '0'; 
    $newcontent->my->readonly = '1';  
	$newcontent->save('friends');  
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
 * 2 => mq,   消息队列
 * 4 => maincontent,  自定义索引表，索引需要自己配置
 * 5 => schedule  调度表，当你需要自行写SQL进行操作时，具体用法附后
 * 6 => message,  消息通知表
 * 7 => yearcontent,  按年存储的自定义索引表
 * 9 => yearmonthcontent 按月存储的自定义索引表
