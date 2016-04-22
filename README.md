# DBmanger
能用的服务器管理包

```php
//这几行代码仅调试的时候需要,真正生产环境时就不需要了
spl_autoload_register("auto_load_src");

function auto_load_src($class_name)
{
    $class_name = str_replace("rayful\\", "", $class_name);  //支持命名空间
    $class_name = str_replace("\\", "/", $class_name);  //支持命名空间
    $class_path = __DIR__ . "/../src/" . $class_name . ".php";
    if (file_exists($class_path))
        require_once $class_path;
}
//----------------------------------

define("MONGO_HOST", "127.0.0.1");  //或者这里改成读取配置文件的方法
define("MONGO_DB", "xiyanghui");    //或者这里改成读取配置文件的方法

//打印全部职位名称
$Jobs = new \Job\Jobs();
foreach ($Jobs as $Job) {
    echo $Job . "\n";
}

//按照一个条件,次序去找
$Jobs = new \Job\Jobs();
$Jobs->find(['title'=>'行政助理']);
foreach ($Jobs as $Job) {
    echo $Job . "\n";
}

$Jobs = new \Job\Jobs();
$Jobs->find(['used'=>true])->sort(['sequence'=>1])->limit(3);
echo $Jobs->paginate();
foreach ($Jobs as $Job) {
    echo $Job->title.":".$Job->desc . "\n\n";
}
```