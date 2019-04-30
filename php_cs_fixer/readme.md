#####  环境准备
- windows 10
- phpstorm 2017.2
- composer

##### 开始配置
- 全局安装
    
  `  composer global require fabpot/php-cs-fixer`
  
**配置**
 - 在phpstorm的File > Settings > Tools > External Tools菜单内进行php-cs-fixer的配置
   
       1. name和description可自行填写
       2. program需要填写php-cs-fixer的可执行文件地址，Windows上是用户目录\Roaming\Composer\composer\vendor\bin\php-cs-fixer.bat，linux和mac上是~/.composer/vendor/bin/php-cs-fixer
       3.parameters填--rules=@Symfony --verbose fix "$FileDir$/$FileName$"，其中 rules 字段具体可以查看 php-cs-fixer 的官方文档，但是由于 Windows 的 cmd 有诸多限制，所以只能传入一些简单的规则，如果需要配置复杂规则建议使用配置文件来完成。
       4.working directory填$ProjectFileDir$
-  插件配置好后，到 File > Settings > Keymap 设置快捷键，快捷键设置好后就可以找个文件试一试了。我设置了快捷键crrl+shift+;   

**使用配置文件**
- 由于 Windows 的 cmd 有诸多限制，所以只能传入一些简单的规则，如果需要配置复杂规则建议使用配置文件来完成

- 将我们的配置文件.php_cs.dist放在某一目录下， 我选择放在D:\phpStudy\php\.php_cs.dist

        <?php
         /**
          * Created by PhpStorm.
          * User: gcg
          * Date: 2018/9/27
          * Time: 11:04
          */
         
         $finder = PhpCsFixer\Finder::create()
             ->files()
             ->name('*.php')
             ->exclude('vendor')
             ->in(__DIR__)
             ->ignoreDotFiles(true)
             ->ignoreVCS(true);
         $fixers = array(
             '@PSR2'                                      => true,
             'single_quote'                               => true, //简单字符串应该使用单引号代替双引号；
             'no_unused_imports'                          => true, //删除没用到的use
             'no_singleline_whitespace_before_semicolons' => true, //禁止只有单行空格和分号的写法；
             'self_accessor'                              => true, //在当前类中使用 self 代替类名；
             'no_empty_statement'                         => true, //多余的分号
             'no_extra_consecutive_blank_lines'           => true, //多余空白行
             'no_blank_lines_after_class_opening'         => true, //类开始标签后不应该有空白行；
             'include'                                    => true, //include 和文件路径之间需要有一个空格，文件路径不需要用括号括起来；
             'no_trailing_comma_in_list_call'             => true, //删除 list 语句中多余的逗号；
             'no_leading_namespace_whitespace'            => true, //命名空间前面不应该有空格；
             'standardize_not_equals'                     => true, //使用 <> 代替 !=；
             'binary_operator_spaces'                     => ['default' => 'align_single_space'] //等号对齐、数字箭头符号对齐
         );
         return PhpCsFixer\Config::create()
             ->setRules($fixers)
             ->setFinder($finder)
             ->setUsingCache(false);
