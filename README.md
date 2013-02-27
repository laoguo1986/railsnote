#创建程序
##创建
rails new bjjl -d=mysql

cd bjjl 

##编辑gemfile

<pre>
source 'http://ruby.taobao.org'

gem 'rails', '3.2.12'
gem 'bootstrap-sass', '2.1'
gem 'bcrypt-ruby', '3.0.1'
gem 'faker', '1.0.1'
gem 'will_paginate', '3.0.3'
gem 'bootstrap-will_paginate', '0.0.6'
gem 'jquery-rails', '2.0.2'

group :development, :test do
  gem 'mysql2'
  gem 'rspec-rails', '2.11.0'
  gem 'guard-rspec', '1.2.1'
  gem 'guard-spork', '1.2.0'  
  gem 'spork', '0.9.2'
end

group :assets do
  gem 'sass-rails',   '3.2.5'
  gem 'coffee-rails', '>= 3.2.2'
  gem 'uglifier', '1.2.3'
end

group :test do
  gem 'capybara', '1.1.2' # 使用类似英语中的句法编写模拟与应用程序交互的代码
  gem 'factory_girl_rails', '4.1.0'
  gem 'cucumber-rails', '1.2.1', :require => false
  gem 'database_cleaner', '0.7.0'
end

group :production do
  gem 'pg', '>= 0.12.2' #pg 是用来连接 PostgreSQL 数据库的，Heroku 使用这个数据库
end

</pre>

<pre>
bundle install
rake db:create
</pre>

#静态页面
##创建控制器及页面
<pre>
rails generate controller StaticPages home help about contact
</pre>

##编辑路由
<pre>
  root to: 'static_pages#home'
  match '/help',    to: 'static_pages#help'
  match '/about',   to: 'static_pages#about'
  match '/contact', to: 'static_pages#contact'
</pre>

###删除index.html
<pre>
rm public/index.html
</pre>
##Bootstrap
###添加gem 
<pre>
gem 'bootstrap-sass', '2.0.4' 
</pre>

bootstrap-sass 会将 LESS 转换成 Sass 格式

##自定义css

app/assets/stylesheets,是 asset pipeline 的一部分,这个目录中的所有样式表都会自动的包含在网站的 application.css 中。

创建自定义css:app/assets/stylesheets/custom.css.scss
<pre>
/* 引入整个 Bootstrap CSS 框架 */
@import "bootstrap";

/* mixins, variables, etc. */

$grayMediumLight: #eaeaea;

@mixin box_sizing {
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
}

/* universal */

html {
  overflow-y: scroll;
}

body {
  padding-top: 60px;
}

section {
  overflow: auto;
}

textarea {
  resize: vertical;
}

.center {
  text-align: center;
  h1 {
    margin-bottom: 10px;
  }
}

/* typography */

h1, h2, h3, h4, h5, h6 {
  line-height: 1;
}

h1 {
  font-size: 3em;
  letter-spacing: -2px;
  margin-bottom: 30px;
  text-align: center;
}

h2 {
  font-size: 1.7em;
  letter-spacing: -1px;
  margin-bottom: 30px;
  text-align: center;
  font-weight: normal;
  color: $grayLight;
}

p {
  font-size: 1.1em;
  line-height: 1.7em;
}


/* header */

#logo {
  float: left;
  margin-right: 10px;
  font-size: 1.7em;
  color: white;
  text-transform: uppercase;
  letter-spacing: -1px;
  padding-top: 9px;
  font-weight: bold;
  line-height: 1;
  &:hover {
    color: white;
    text-decoration: none;
  }
}

/* footer */

footer {
  margin-top: 45px;
  padding-top: 5px;
  border-top: 1px solid $grayMediumLight;
  color: $grayLight;
  a {
    color: $gray;
    &:hover { 
      color: $grayDarker;
    }
  }  
  small { 
    float: left; 
  }
  ul {
    float: right;
    list-style: none;
    li {
      float: left;
      margin-left: 10px;
    }
  }
}

/* miscellaneous */

.debug_dump {
  clear: both;
  float: left;
  width: 100%;
  margin-top: 45px;
  @include box_sizing;
}

/* sidebar */

aside {
  section {
    padding: 10px 0;
    border-top: 1px solid $grayLighter;
    &:first-child {
      border: 0;
      padding-top: 0;
    }
    span {
      display: block;
      margin-bottom: 3px;
      line-height: 1;
    }
    h1 {
      font-size: 1.6em;
      text-align: left;
      letter-spacing: -1px;
      margin-bottom: 3px;
    }
  }
}

.gravatar {
  float: left;
  margin-right: 10px;
}

.stats {
  overflow: auto;
  a {
    float: left;
    padding: 0 10px;
    border-left: 1px solid $grayLighter;
    color: gray;
    &:first-child {
      padding-left: 0;
      border: 0;
    }
    &:hover {
      text-decoration: none;
      color: $blue;
    }
  }
  strong {
    display: block;
  }
}

.user_avatars {
  overflow: auto;
  margin-top: 10px;
  .gravatar {
    margin: 1px 1px;
  }
}

/* forms */

input, textarea, select, .uneditable-input {
  border: 1px solid #bbb;
  width: 100%;
  height: auto;
  margin-bottom: 15px;
  @include box_sizing;  
}

#error_explanation {
  color: #f00;
  ul {
    list-style: none;
    margin: 0 0 18px 0;
  }
}

.field_with_errors {
  @extend .control-group;
  @extend .error;
}

/* users index */

.users {
  list-style: none;
  margin: 0;
  li {
    overflow: auto;
    padding: 10px 0;
    border-top: 1px solid $grayLighter;
    &:last-child {
      border-bottom: 1px solid $grayLighter;
    }
  }
}

/* microposts */

.microposts {
  list-style: none;
  margin: 10px 0 0 0;

  li {
    padding: 10px 0;
    border-top: 1px solid #e8e8e8;
  }
}
.content {
  display: block;
}
.timestamp {
  color: $grayLight;
}
.gravatar {
  float: left;
  margin-right: 10px;
}
aside {
  textarea {
    height: 100px;
    margin-bottom: 5px;
  }
}
</pre>
##编辑 app/views/layouts/ 下文件

### application.html.erb
<pre>
<!DOCTYPE html>
<html>
  <head>
    <title><%= full_title(yield(:title)) %></title>
    <%= stylesheet_link_tag    "application", media: "all" %>
    <%= javascript_include_tag "application" %>
    <%= csrf_meta_tags %>
    <%= render 'layouts/shim' %>
  </head>
  <body>
    <%= render 'layouts/header' %>
    <div class="container">
      <% flash.each do |key, value| %>
        <%= content_tag(:div, value, class: "alert alert-#{key}") %>
      <% end %>
      <%= yield %>
      <%= render 'layouts/footer' %>
      <%= debug(params) if Rails.env.development? %>
    </div>
  </body>
</html>
</pre>
###app/helpers/application_helper.rb 
其中，<title><%= full_title(yield(:title)) %></title>中调用了 app/helpers/application_helper.rb 
<pre>
module ApplicationHelper

  # Returns the full title on a per-page basis.
  def full_title(page_title)
    base_title = 'BJJL'
    if page_title.empty?
      base_title
    else
      "#{base_title} | #{page_title}"
    end
  end
end
</pre>
###<%= render 'layouts/shim' %> 
Rails 3 默认会使用 HTML5（如 <!DOCTYPE html> 所示），因为 HTML5 标准还很新，有些浏览器（特别是较旧版本的 IE 浏览器）还没有完全支持，所以我们加载了一些 JavaScript 代码（称作“HTML5 shim”）来解决这个问题：
<pre>
<!--[if lt IE 9]>
<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->

</pre>

### <%= render 'layouts/header' %>
<pre>
<header class="navbar navbar-fixed-top">
  <div class="navbar-inner">
    <div class="container">
      <%= link_to "sample app", root_path, id: "logo" %>
      <nav>
        <ul class="nav pull-right">
          <li><%= link_to "Home",    root_path %></li>
          <li><%= link_to "Help",    help_path %></li>
          <% if signed_in? %>
            <li><%= link_to "Users", users_path %></li>
            <li id="fat-menu" class="dropdown">
              <a href="#" class="dropdown-toggle" data-toggle="dropdown">
                Account <b class="caret"></b>
              </a>
              <ul class="dropdown-menu">
                <li><%= link_to "Profile", current_user %></li>
                <li><%= link_to "Settings", edit_user_path(current_user) %></li>
                <li class="divider"></li>
                <li>
                  <%= link_to "Sign out", signout_path, method: "delete" %>
                </li>
              </ul>
            </li>
          <% else %>
            <li><%= link_to "Sign in", signin_path %></li>
          <% end %>
        </ul>
      </nav>
    </div>
  </div>
</header>
</pre>
header 标签的意思是放在网页顶部的内容。我们为 header 标签指定了两个 CSS class3，navbar 和 navbar-fixed-top

###footer
<pre>
<footer class="footer">
  <small>
    <a href="http://railstutorial.org/">Rails Tutorial</a>
    by Michael Hartl
  </small>
  <nav>
    <ul>
      <li><%= link_to "About",   about_path %></li>
      <li><%= link_to "Contact", contact_path %></li>
      <li><a href="http://news.railstutorial.org/">News</a></li>
    </ul>
  </nav>
</footer>
</pre>
#mysql
##常用命令
###安装

sudo apt-get install mysql-server mysql-client #中途会让你输入一次root用户密码

###进入mysql

mysql -u root -p

#修改 MySQL 的管理员密码

sudo mysqladmin -u root password newpassword；

##无法登录错误
###第一种办法
steve@steve:~$ mysql --user=root --pass mysql
Enter password:

mysql> update user set Password=PASSWORD('new-password-here') WHERE User='root';
Query OK, 2 rows affected (0.04 sec)
Rows matched: 2  Changed: 2  Warnings: 0

mysql> flush privileges;
Query OK, 0 rows affected (0.02 sec)

mysql> exit
Bye

###重设密码

sudo /etc/init.d/mysql stop

sudo /usr/bin/mysqld_safe --skip-grant-tables &

sudo mysql --user=root mysql

mysql> update user set Password=PASSWORD('new-password-here') WHERE User='root';

mysql> flush privileges;

mysql> exit

#git github
##git 第一次运行时设置
```sh
$ git config --global user.name "Your Name"
$ git config --global user.email your.email@example.com
$ git config --global core.editor "gvim -f" #设置默认编辑器
$ git config --global alias.co checkout #用 co 代替字数较多的 checkout 命令
```
##日常应用

```sh
$ git init #新建仓库
$ git add . #把 Rails 项目中的文件添加到 git 的暂存区域（staging area）
$ git status  #查看暂存区域
$ git commit -m "评论" #用 commit 命令告诉 git 你想保存这些改动
$ git log #查看提交的历史信息
```
##文件删除与恢复
```sh
$ rm -rf app/controllers/ #删除文件或其他改动
$ git status  #查看改动
$ git checkout -f  #覆盖当前改动
```

##github
###［创建 SSH 密匙］（https://help.github.com/articles/generating-ssh-keys）

###创建公共项目并推送

git remote add origin https://github.com/laoguo1986/bjjl.git

git push -u origin master

git push  #大多数系统中我们都可以省略 origin master，只要运行 git push
##分支，编辑，提交，合并
```sh
$ git checkout -b sonbranch #创建子分支
$ git branch  #查看当前分支
$ 改动子分支
$ git checkout master  #回到主分支
$ git merge sonbranch #合并分支
$ git branch -d sonbranch #合并分支
$ git branch -D topic-branc #使用 git branch -D 放弃对从分支所做的修改,和旗标 -d 不同，即使还未合并 -D 也会删除分支。
```
###部署

$ gem install heroku 

$ heroku keys:add

$ heroku create --stack cedar #在 Heroku 上新建一个应用程序

$ git push heroku master #通过 Git 将应用程序推动到 Heroku 中

$ heroku open #通过 heroku create 命令给出的地址,查看你刚刚部署的应用程序



