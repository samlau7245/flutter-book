
* [BoxFit Class](https://api.flutter.dev/flutter/painting/BoxFit-class.html)

#contain

<img src="/assets/images/flutter/36.png"/>

`child`在`FittedBox`范围内尽可能大，但是不能超出其尺寸。【`contain`是在保持着`child`宽高比不变的大前提下尽可能的填满，一般是宽度或者高度达到最大值时就会停止缩放。】


# cover

<img src="/assets/images/flutter/37.png"/>

按照原始尺寸填充整个容器，内容可能会超过容器范围|

# fill

<img src="/assets/images/flutter/38.png"/>

不按照宽高比填充，直接填满但是不会超过容器范围|

# fitHeight

<img src="/assets/images/flutter/39.png"/>

按照高度填充整个容器|

# fitWidth

<img src="/assets/images/flutter/40.png"/>

按照宽度填充整个容器|

# none

<img src="/assets/images/flutter/41.png"/>

没有任何填充|

# scaleDown

<img src="/assets/images/flutter/42.png"/>

根据情况缩小范围，内容不会超过容器范围，有时和`contain`一样有时和`none`一样
