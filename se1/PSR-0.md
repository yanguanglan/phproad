PSR-0 PHP自动加载约定规范

规范
---------

* 一个标准的命名空间、类必须具备以下结构 `\<Vendor Name>\(<Namespace>\)*<Class Name>`
* 命名空间必须具备一个顶级的命名空间名称 ("Vendor Name").
* 命名空间按需求可以包含子命名空间.
* 当文件加载时，每个命名空间的分割符将转换成 `DIRECTORY_SEPARATOR`.
* 文件加载时，在类名称中的 "\_" 字符将转换成 `DIRECTORY_SEPARATOR`. 命名空间名称中的 "\_" 字符不做特殊转换.
* 一个标准的命名空间、类加载的文件后缀为 ".php".
* 包名、命名空间名称、类名称可以是任意大、小写字母.

例子
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

下划线在命名空间名称和类名称中
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

这里是PHP 5.3类自动加载的标准最基本实现.

例子
----------------------

符合以上标准的自动加载类实例

    <?php
    
    function autoload($className)
    {
        $className = ltrim($className, '\\');
        $fileName  = '';
        $namespace = '';
        if ($lastNsPos = strripos($className, '\\')) {
            $namespace = substr($className, 0, $lastNsPos);
            $className = substr($className, $lastNsPos + 1);
            $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
        }
        $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';
    
        require $fileName;
    }

SplClassLoader 实践
-----------------------------

PHP 5.3 类自动加载实践

* [http://gist.github.com/221634](http://gist.github.com/221634)