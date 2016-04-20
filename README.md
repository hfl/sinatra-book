Sinatra 宝典
============

这是一本针对 Sinatra 开发者而写的具有新手指南和各种秘籍的宝典。

如何编译此书
---------------------

在您开始将此书转换成各种格式之前需要安装依赖的软件。

    gem install bundler
    bundle install

然后在根目录里，执行下面的 Rake 任务：

    bundle exec rake book:build

将会在 output 文件夹内生成一本 PDF 版本的图书。

您也可以运行内建的图书 sinatra 应用程序来浏览：

    rackup

然后访问：http://localhost:9292/

如何参与贡献
-----------------

想要为 [Sinatra Book][sinatra-book] 的秘籍或者新手指南贡献代码吗？

Check out the [Sinatra Recipes][sinatra-recipes] project for all of
the recent additions from the community.

If you're looking for something to work on be sure to check the [issue
tracker][issues] first, then read up on the [styling
guidelines][styling-guidelines].

Once you have [forked the project][forking], feel free to send us a [pull
request][pull-requests].

Join us on IRC (#sinatra at irc.freenode.org) if you need help with anything.


[sinatra-book]: http://github.com/sinatra/sinatra-book
[sinatra-recipes]: http://recipes.sinatrarb.com/
[issues]: http://github.com/sinatra/sinatra-book/issues
[styling-guidelines]: http://github.com/sinatra/sinatra-book-contrib/wiki/Style-Guidelines
[forking]: http://help.github.com/forking/
[pull-requests]: http://help.github.com/pull-requests/

授权协议
-----------------

The MIT License (MIT)

Copyright (c) 2015 Sinatra

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
