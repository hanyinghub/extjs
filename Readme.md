# Sencha Extjs

this is sencha Extjs framework package, you can download all extjs all version from release.

Header link:

```xml
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="../extjs4.2/resources/css/ext-all-neptune.css">
    <script src="../extjs4.2/ext-all.js"></script>
    <script src="../extjs4.2/ext-theme-neptune.js"></script>
    <script src="../extjs4.2/locale/ext-lang-zh_CN.js"></script>
</head>
```


Useage as :

```xml
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="../extjs4.2/resources/css/ext-all-neptune.css">
    <script src="../extjs4.2/ext-all.js"></script>
    <script src="../extjs4.2/ext-theme-neptune.js"></script>
    <script src="../extjs4.2/locale/ext-lang-zh_CN.js"></script>
</head>
<body>
<script>
    Ext.onReady(function () {

        var itemsPerPage = 4;   // 设置您希望看到的每页的条目数量
        Ext.define('User', {
            extend: 'Ext.data.Model',
            fields: [
                {name: 'name', type: 'string'},
                {name: 'email',  type: 'string'},
                {name: 'phone',  type: 'string'}
            ]
        });
        var store = Ext.create('Ext.data.Store', {
            id: 'simpsonsStore',
            autoLoad: false,
            model: 'User',
            //fields: ['name', 'email', 'phone'],
            pageSize: itemsPerPage, // 每页的条目数量
//            proxy: {
//                type: 'ajax',
//                url: 'pagingstore.js',  // 一个url，将加载start和limit参数并返回期望的数据
//                reader: {
//                    type: 'json',
//                    root: 'dat',
//                    totalProperty: 'total'
//                }
//            }
            data:{'total':1000,'dat':[
                { 'name': 'Lisa',  "email":"lisa@simpsons.com",  "phone":"555-111-1224"  },
                { 'name': 'Bart',  "email":"bart@simpsons.com",  "phone":"555-222-1234" },
                { 'name': 'Homer', "email":"home@simpsons.com",  "phone":"555-222-1244"  },
                { 'name': 'Marge', "email":"marge@simpsons.com", "phone":"555-222-1254"  }
            ]},
            proxy: {
                type: 'memory',
                reader: {
                    type: 'json',
                    root: 'dat',
                    totalProperty: 'total'
                }
            }
        });
        // 指定要加载的页
        store.loadPage(1);
        //Ext.data.StoreManager.lookup('simpsonsStore').loadPage(1)
        var grid = Ext.create('Ext.grid.Panel', {
//            title: 'Simpsons',
            store: store,
            columns: [
                {header: 'Name', dataIndex: 'name'},
                {header: 'Email', dataIndex: 'email', flex: 1},
                {header: 'Phone', dataIndex: 'phone'}
            ],
            dockedItems: [{
                xtype: 'pagingtoolbar',
                store: store,   // GridPanel使用相同的数据源
                dock: 'bottom',
                displayInfo: true
            }]
        });


        Ext.create("Ext.container.Viewport", {
            layout: 'border',
            items: [{
                region: 'north',
                html: 'xx系统',
                bodyPadding: 20,
                border: false,
                height: 80
            },
                {
                    region: 'east',
                    title: 'east title',
                    split: true,
                    width: 300
                },
                {
                    region: 'south',
                    title: 'south title',
                    header: true,
                    height: 80
                },
                {
                    region: 'west',
                    title: 'west title',
                    split: true,
                    collapsible: true,
                    width: 300
                },
                {
                    region: 'center',
                    xtype: 'tabpanel', // TabPanel本身没有title属性
                    activeTab: 0,      // 配置默认显示的激活面板
                    closable: true,

                    items: [{
                        title: 'Default Tab',
                        layout: 'fit',
                        items: [grid]
                    }, {
                        title: 'Tab22222',
                        closable: true,
                        html: 'The first tab\'s content. Others may be added dynamically'
                    }, {
                        title: 'Tab33333',
                        closable: true,
                        html: 'The first tab\'s content. Others may be added dynamically'
                    }]
                }
            ]
        });
    });
</script>
</body>

</html>
```