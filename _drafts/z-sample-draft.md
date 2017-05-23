---
layout: post
title: A sample post
date: 2017-05-19
categories: test
---
Here's a sampe Jekyll / github pages post.

Copy to the posts directory with a date format to publish.

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}
