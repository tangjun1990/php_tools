# php_tools

整理一些php开发中好用的工具

* 一 git commit时自动检查你的php代码

为了控制php项目发布的风险，理论上可以在jenkins build阶段引入phpcs，phpmd等插件检查代码风格和代码逻辑，引入phpunit做单测的覆盖度检查。

考虑到目前项目的实际情况，暂时无法在build阶段强制性检查代码，考虑使用该折中方案适度控制代码风险：开发者在本地检查后再提交代码。

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
