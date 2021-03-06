#### WPF改变视觉树结构动画失效

项目需要在某个按钮平移动画完成后再在按钮所在的父容器内添加新的元素。其中涉及到`Children.Add()`方法。假如平移方法是`Trans()`，则`Trans()`执行完后再执行`Children.Add()`，就会导致动画还未执行，就直接将新元素添加到容器内。清除元素亦是如此。

解决方法是，在调用动画完成事件，最好是将所有动画添加到`StoryBoard`中，然后为`StoryBoard`添加`Completed`事件，在`Completed`事件中再执行`Add()`或`Clear()`方法。

因为我的项目中涉及到的按钮是封装在dll中的，而这个dll的内容会填充到主界面指定容器内。假如点击了某个按钮，是无法在主界面对应的项目中调用方法来执行相关点击事件的。

所以，在按钮所在的dll对应的点击事件中直接通过遍历视觉树来找到相关容器，之后再执行`Add()`或`Clear()`方法。