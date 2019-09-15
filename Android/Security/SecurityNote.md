# 安卓开发注意事项

## Activity

Activity有四种启动模式，通过Activity的launchMode属性来控制task和Activity实例的创建。在不指定Activity的launchMode属性时，默认为standard模式。
| 启动模式  | 描述     |
| -------- | ---------|
| standard | 标准模式，standard是活动的默认启动模式。在standard模式下，每当启动一个新的活动，它就会在返回栈中入栈，并处于栈顶位置。不管活动是否已在返回栈中存在，每次调用startActivity()就会产生一个新的Activity实例，但不会创建新的task。|
| SingleTop | 如果已经有一个Activity实例位于task栈顶时，则直接使用该实例，不会再创建新实例；如果不位于栈顶，就等同于standard模式。 |
| SingleTask | Activity第一次启动时，会在一个新的task中创建实例，以后每次调用都会使用已生成的Activity实例，不再产生新的实例。 |
| singleInstance | 启动时与singleTask一样，与它的区别就是: singleInstance下的Activity会单独占用一个Task栈，具有全局唯一性。以singleInstance模式启动的Activity在整个系统中是单例的，如果在启动这样的Activiyt时，已经存在了一个实例，那么会把它所在的任务调度到前台，重用这个实例 |

注意事项：
- 对于涉及敏感数据的私有Activity，禁止配置launchMode。若将launchMode设置为singleTask或singleInstance，则可能会创建新的task，task间传送Intent消息时，Intent消息存在被其它应用读取到的可能，造成泄漏。
- 启动私有Activity的Intent设置flag时，也要禁止设置launchMode属性。

