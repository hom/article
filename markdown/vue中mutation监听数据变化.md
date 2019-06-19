### 需求
在`vue`的`store`中我们可以通过提交`state.***`的`mutations`修改数据，如果只修改某个数据的某个属性应该怎么提交

### 解决
由于`vue`是通过监听对象的`set`和`get`来实现动态绑定，我们如果添加属性，`vue`无法得知你修改的对象，我们可以提前将要添加的属性设置默认值，然后再修改即可
```js
state.***.*** = ***;
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTM5NDI4NTg2OF19
-->