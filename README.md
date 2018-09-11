# php_tools

整理一些php开发中好用的工具

* git commit时自动检查你的php代码

当你在命令行git commit你的代码时，以下操作可以帮你自动扫描代码风格和逻辑。

具体实施步骤如下：

    1.安装phpcs，phpcbf

        1.使用composer安装： composer global require "squizlabs/php_codesniffer=*"

        2.安装后可执行文件位置：~/.composer/vendor/bin/phpcs

    2.安装phpmd

        1.使用composer安装： composer global require phpmd/phpmd

        2.安装后可执行文件位置：~/.composer/vendor/bin/phpmd

    3.编写git pre-commit钩子

        1.vim .git/hooks/pre-commit，加入脚本内容：https://github.com/tangjun1990/php_tools/blob/master/pre-commit （注意修改脚本中的目录哟！）

        2.chmod +x .git/hooks/pre-commit

    4.那么，在你每次进行git commit操作的时候，pre-commit钩子中的shell就会自动帮你检查代码啦！相应的错误信息就会输出到终端

    5.当然，如果你不喜欢用hook这种方式，也可以在你每次提交代码之前，手动执行命令来检查

        1.~/.composer/vendor/bin/phpcs dirOrFile --standard=PSR2

        2.~/.composer/vendor/bin/phpmd dirOrFile text codesize,unusedcode,naming

    6.最重要的来了，那就是针对检查结果改代码，改代码，改代码
