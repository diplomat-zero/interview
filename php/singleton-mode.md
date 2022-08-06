```php
class Singleton {
    //私有属性，用于保存实例
    private static $instance;

    //构造方法私有化，防止外部创建实例
    private function __construct(){}
    
    //克隆方法私有化，防止复制实例
    private function __clone(){}
    
    //公有方法，用于获取实例
    public static function getInstance(){
        //判断实例有无创建，没有的话创建实例并返回，有的话直接返回
        if(!(self::$instance instanceof self)){
            self::$instance = new self();
        }
        return self::$instance;
    }
}
```