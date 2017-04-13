- 不要一个page一个无所不能的controller包含所有页面逻辑。

       > Angularjs ng-controller旨在将业务逻辑的区分，更推荐按照业务逻辑的划分controller，做到业务功能的高内聚，controller的单一原则SRP。

- View中包含尽量少的逻辑

      >  就像jsp，asp这类服务端模板引擎一样，我们应该把尽量少的逻辑放在view中，因为这样会导致view和逻辑的紧耦合性，view在软件开发中是最易变化的，而表现层逻辑却相对于view是相对稳定的行为。同时也导致的view中的逻辑不能被自动化测试，持续集成所覆盖，这将导致以后修改重构和模块的集成的痛苦。很明显的就是太多的angularjs的ng-switch，ng-when和页面计算表达式等等。

- 在controller和service中绝对不能出现html的DOM和CSS代码

       > 这会导致逻辑的混杂耦合，对于angularjs自身的绑定对html操作，很多时候你会分不清是view的影响源，导致修复bug，和新增功能，重构的艰难，常常出现很多的诡异行为。最好的实践模式则是把必须的dom，css操作移向angular的Directive，或者view中。在angularjs模式中只有directive和view才能出现dom和css的逻辑操作。

- controller中公用的逻辑推向service（factory，value，config)，采用IOC的注入，提高代码的重用度，修改的单一点，开闭原则。

- controller应该只包含业务逻辑，对于数据模型的格式化过滤尽量交给angular框架filter等处理。

- viewmodel中最好建立一个通用属性比如vm，它承载view渲染的最小量化model，对于model的变形事件则在vm之外scope之上。这才是MVVM推荐方式。事件相当于WPF中的command，负责模型事件的传递修改模型，从而从模型的改变通知view的强制更新（WPF中model必须实现INotifyPropertyChange接口）。同时这样vm属性也便于数据的填充和收集回发服务端。

- IOC注入优先，有助于良好的设计，逻辑的可重用和单元模块的可测试性，面向对象的“开闭原则”，修改的单一点。

- 良好的分层设计，对于view的交互采用controller通过viewmode（scope）的推送，与服务器的交互推向service层次，利用angularjs的$resource或者$http获取更新数据model，以及与服务端交互。层次划分属于纵向分割，将相同功能逻辑的接口放在一起，架构层次，而model则从业务的逻辑横向分离。

- 服务端的服务的接口需要考虑表现层客户端的应用提供，这是一个良好的SOA服务设计的准则，这里不用多余的描述，具体请移步[架构篇](http://www.cnblogs.com/whitewolf/category/379884.html)。

- 如果你的公司应用了敏捷开发则，TDD的开发是必备的，angularjs本也是解决javascript测试驱动开发项目。

- scope的纯净性，scope上的每一个函数和属性必须为view所用（事件传递或者属性绑定），不用的可以作为工具函数或者service处置.

- 对controller之间如果不是强依赖，只是弱引用则最好用事件$emit,$on,$broadcast,是的controller之间低耦合（Angularjs Controller 间通信机制）。

- [angularjs的的模块管理参见如何组织大型JavaScript应用中的代码？](http://kb.cnblogs.com/page/176541/)
