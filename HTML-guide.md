### Html编码规范

- 默认要使用2个空格缩进，特殊情况特殊考虑

- class命名，避免驼峰，避免下划线，避免BEM，尽量单词全字母小写，单词间以连字符 “ - ” 分隔，class 需要代表相应模块或部件的内容或功能，不得以样式信息进行命名（框架提供的样式除外）

-  在所有标签的属性中，杜绝单引号，杜绝无引号，仅允许使用双引号，若双引号中需要存在值，则值使用单引号；如：

        <div ng-if="true == 'true'"></div>

- 当一个元素属性过多时，一定要将每一个属性单独书写一行，保持结构上的美观与可读性，且属性的排列方式，从基础的class/id/name等原生属性排列至H5自定义属性，例：

        <!-- Angular程序中某下拉菜单所使用的属性 -->
        <select 
          required
          class="form-control" 
          name="organizations"
          ng-if="organizations.length > 0"
          ng-model="lesson.organization_id" 
          ng-options="organization.id as organization.name for organization in organizations"
          ng-disabled="!!lesson_id && !!lesson.organization_id && organization_is_not_undefined"
          ng-readonly="!!lesson_id && !!lesson.organization_id && organization_is_not_undefined"
          validator="required" 
          required-error-message="请选择所属机构">
          <option disabled selected value>- 选择机构 -</option>
        </select>

-  禁止为了 hook 脚本，创建无样式信息的 class不，允许 class 只用于让 JavaScript 选择某些元素，class 应该具有明确的语义和样式；否则容易导致 CSS class 泛滥。使用 id、属性选择作为 hook 是更好的方式。

- 同一页面，应避免使用相同的 name 与 id，元素ID仅供JS/Dom操作使用，与样式无关，且ID必须全局唯一

- 标签名必须使用小写字母

- 对于无需自闭合的标签，不允许自闭合（即去掉标签后的 " / " ），例：

        <!-- good code -->
        <input type="text" name="title">

        <!-- bad code -->
        <input type="text" name="title" />

- 标签使用必须符合标签嵌套规则，[祥参](http://www.cs.tut.fi/~jkorpela/html5.dtd)

        比如 div 不得置于 p 中，tbody 必须置于 table 中

- 在 CSS 可以实现相同需求的情况下，不要再使用表格进行布局

- 布尔类型的属性，可以不添加属性值，例：

        <input type="text" disabled>
        <input type="checkbox" value="1" checked>

- 使用 HTML5 的 doctype 来启用标准模式，使用大写的 DOCTYPE，例：

        <!DOCTYPE html>

- 为图片添加Alt属性

- 在元信息中，设置baseurl

- href/src 出现链接的地方都可以省略请求协议
