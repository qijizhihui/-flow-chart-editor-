# flow-chart-editor


### npm 安装

推荐使用 npm 安装

```
npm i 
"flow-chart-editor": "git+https://github.com/qijizhihui/-flow-chart-editor-.git",
```

### 脚本引用

```
require('flow-chart-editor');
```

### 例子：
[演示文档 Demo](flow-chart-editor/dist/index.html)
```
  // 画布
  initEditor(editor) {
    var that = this;
    /* window.onload = function () { */
    var fce = that.fce = new FCE({
      el: editor,
      rightMenus: [{
        id: "id_alert",
        content: "弹出窗",
        tooltipText: "弹出窗",
        selector: "node,edge", //当在node,edge元素上右键时才显示
        onClickFunction: function (evt) { //点击后触发事件
          var target = evt.target || evt.cyTarget;
          alert('弹出信息！');
        },
        hasTrailingDivider: true
      }],
      toolbars: [{
          name: 'rectangle',
          icon: require('../../../contents/images/conf/rectangle.png'),
          className: '',
          title: '矩形',
          exec: function (evt, clickType, obj) {
            const label = prompt('请输入节点名称：'),
              data = {
                id: new Date().getTime(),
                label: label
              };
            if (!label) return;
            if (clickType === 'node') {
              data.parent = obj.id;
            }
            this.addNode(data, 'rectangle');
          },
        },
        {
          name: 'rounded_rectangle',
          icon: require('../../../contents/images/conf/rounded_rectangle.png'),
          className: '',
          title: '圆角矩形',
          exec: function (evt, clickType, obj) {
            const label = prompt('请输入节点名称：'),
              data = {
                id: new Date().getTime(),
                label: label
              };
            if (!label) return;
            if (clickType === 'node') {
              data.parent = obj.id;
            }
            this.addNode(data, 'roundrectangle');
          },
        },
        {
          name: 'choice',
          icon: require('../../../contents/images/conf/choice.png'),
          className: '',
          title: '菱形',
          exec: function (evt, clickType, obj) {
            const label = prompt('请输入节点名称：'),
              data = {
                id: new Date().getTime(),
                label: label
              };
            if (!label) return;
            if (clickType === 'node') {
              data.parent = obj.id;
            }
            this.addNode(data, 'diamond');
          },
        },
        {
          name: 'round',
          icon: require('../../../contents/images/conf/round.png'),
          className: '',
          title: '圆形',
          exec: function (evt, clickType, obj) {
            const label = prompt('请输入节点名称：'),
              data = {
                id: new Date().getTime(),
                label: label
              };
            if (!label) return;
            if (clickType === 'node') {
              data.parent = obj.id;
            }
            this.addNode(data, 'ellipse');
          },
        },
        {
          name: 'download-json',
          icon: require('../../../contents/images/conf/download.png'),
          className: '',
          title: '下载json文件',
          click: function (bar) {
            this.exportFile('json', '导出JSON文件');
            bar.cancelActive(); //取消自身选中
          },
        },
      ],
    });

    fce.addListener('add_click', function () {
      console.log('编辑器被点击！');
    });

    fce.addListener('context_menus_rename', function (evt, clickType, data) {
      const label = prompt('请输入节点新名称：', data.label);
      if (label) {
        data.label = label;
        this.rename(data);
      }
    });

    fce.addListener('context_menus_remove', function (evt, clickType, data) {
      if (confirm('您确定要删除该节点吗？')) {
        this.remove(data.id);
      }
    });
    /*    }; */
  },

```
