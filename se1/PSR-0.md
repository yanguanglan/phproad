PSR-0 PHP�Զ�����Լ���淶

�淶
---------

* һ����׼�������ռ䡢�����߱����½ṹ `\<Vendor Name>\(<Namespace>\)*<Class Name>`
* �����ռ����߱�һ�������������ռ����� ("Vendor Name").
* �����ռ䰴������԰����������ռ�.
* ���ļ�����ʱ��ÿ�������ռ�ķָ����ת���� `DIRECTORY_SEPARATOR`.
* �ļ�����ʱ�����������е� "\_" �ַ���ת���� `DIRECTORY_SEPARATOR`. �����ռ������е� "\_" �ַ���������ת��.
* һ����׼�������ռ䡢����ص��ļ���׺Ϊ ".php".
* �����������ռ����ơ������ƿ����������Сд��ĸ.

����
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

�»����������ռ����ƺ���������
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`

������PHP 5.3���Զ����صı�׼�����ʵ��.

����
----------------------

�������ϱ�׼���Զ�������ʵ��

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

SplClassLoader ʵ��
-----------------------------

PHP 5.3 ���Զ�����ʵ��

* [http://gist.github.com/221634](http://gist.github.com/221634)