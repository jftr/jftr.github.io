---
layout: post
title: Spriting with Compass
tags: [Sass, Compass]
permalink: spriting-with-compass
---

### [Spriting with Compass](http://compass-style.org/help/tutorials/spriting/)

Imagine that in your project's image folder there are four icons:

<p class="indent">
images/my-icons/new.png<br>
images/my-icons/edit.png<br>
images/my-icons/save.png<br>
images/my-icons/delete.png
</p>

Each is an icon that is 32px square.

\* Note: The use of `my-icons` is only for this example, "my-icons" represents the folder name that contains your sprites.

Sprites stored in a nested folder will use the last folder name in the path as the sprite name.

The simplest way to use these icon sprites is to let compass give you a class for each sprite:

{% highlight scss %}
@import "compass/utilities/sprites";
@import "themes/my-icons/*.png";
@include all-my-icons-sprites;
{% endhighlight %}

CSS output:

{% highlight css %}
.my-icons-sprite,
.my-icons-delete,
.my-icons-edit,
.my-icons-new,
.my-icons-save   { background: url('/images/my-icons-s34fe0604ab.png') no-repeat; }

.my-icons-delete { background-position: 0 0; }
.my-icons-edit   { background-position: 0 -32px; }
.my-icons-new    { background-position: 0 -64px; }
.my-icons-save   { background-position: 0 -96px; }
{% endhighlight %}

If you want control over what selectors are generated, in this example, this is done by using the `my-icons-sprite` mixin.

{% highlight scss %}
@import "my-icons/*.png";

.actions {
  .new    { @include my-icons-sprite(new);    }
  .edit   { @include my-icons-sprite(edit);   }
  .save   { @include my-icons-sprite(save);   }
  .delete { @include my-icons-sprite(delete); }
}
{% endhighlight %}

And your stylesheet will compile to:

{% highlight css %}
.my-icons-sprite,
.actions .new,
.actions .edit,
.actions .save,
.actions .delete { background: url('/images/my-icons-s34fe0604ab.png') no-repeat; }

.actions .new    { background-position: 0 -64px; }
.actions .edit   { background-position: 0 -32px; }
.actions .save   { background-position: 0 -96px; }
.actions .delete { background-position: 0 0;     }
{% endhighlight %}

You can get a unit value by using the magical dimension functions `<map>-sprite-height` and `<map>-sprite-width` If you are looking to just return the dimensions see the [docs](http://compass-style.org/reference/compass/utilities/sprites/base/#mixin-sprite-dimensions).

{% highlight scss %}
@import "my-icons/*.png";
$box-padding: 5px;
$height: my-icons-sprite-height(some_icon);
$width: my-icons-sprite-width(some_icon);

.somediv {
  height: $height + $box-padding;
  width: $width + $box-padding;
}
{% endhighlight %}

