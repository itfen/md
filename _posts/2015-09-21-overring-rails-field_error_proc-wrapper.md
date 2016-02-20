---
layout: post
title:  "自定义 Rails 的 field_error_proc"
categories:
comments: true
share: true
---

Rails 的数据验证配合表单帮助方法会自动为出错的表单信息产生一个 input 的 html 包裹元素，默认是一个 class="field-with-errors" 的 div，详情：[Displaying Validation Errors in Views](http://guides.rubyonrails.org/active_record_validations.html#displaying-validation-errors-in-views)。但是很多前端框架有自己自定义的错误样式，所以需要覆盖 field_error_proc 来自定义错误表单。

方法1：如果只需要修改此包裹元素，找到 `config/application.rb` 在 `class Application < Rails::Application` 中添加

{% highlight ruby linenos %}
config.action_view.field_error_proc = Proc.new { |html_tag, instance|
  "<div class=\"ui input error\">#{html_tag}</div>".html_safe
}
{% endhighlight %}

方法2：如果还需要进一步修改 `.field-with-errors` 的父元素

未完待续...
