### 简单实现AMD功能

```javascript
(function (global) {

    var AMD = {};

    // 模块缓存池
    var moduleStorage = {};


    /**
     * 模块定义
     * @name define
     * @param {String} name 模块名字
     * @param {Array} dependencies 模块依赖
     * @param {Function} factory 模块方法
     * @returns {Object}
     */
    AMD.define = function define(name, dependencies, factory) {
        const that = this;

        let _name, _dependencies, _factory;
        let _exec = false;

        // 三个参数都齐全
        if (factory) {
            _name = name;
            _dependencies = dependencies;
            _factory = factory;
        } else {
            // 俩个参数
            if (dependencies) {
                // name 和 factory
                if (typeof name === "string" && typeof dependencies === 'function') {
                    _name = name;
                    _dependencies = [];
                    _factory = dependencies;
                }
                // dependencies 和 factory, 同时函数自执行
                else if (name instanceof Array && typeof dependencies === 'function') {
                    _dependencies = name;
                    _factory = dependencies;
                    _name = 'temp-' + new Date().getTime();
                    _exec = true;
                }
            } else {
                // 只有一个参数时，模块代码自执行
                if (typeof name === 'function') {
                    _name = `temp-${new Date().getTime()}`;
                    _dependencies = [];
                    _factory = name;
                    _exec = true;
                } else return false;
            }
        }

        if (!moduleStorage.hasOwnProperty(_name)) {
            var _module = {
                name: _name,
                dependencies: _dependencies,
                factory: _factory
            };

            moduleStorage[_name] = _module;
        }

        if (_exec) that.emit(_name);
        else return moduleStorage[_name];
    }

    /**
     * 发射模块
     * @name emit
     * @param {String} name 模块名字
     * @returns {} 
     */
    AMD.emit = function emit(name) {
        const that = this;

        let module = moduleStorage[name];

        if (typeof module.entity === 'undefined') {
            let _args = [];

            for (var i = 0, len = module.dependencies.length; i < len; i++) {
                var _entity = module.dependencies[i].entity;

                if (typeof _entity !== 'undefined') {
                    _args.push(_entity);
                    console.log('_entity', _entity);
                } else {
                    _args.push(that.emit(module.dependencies[i]));
                    console.log(that.emit(module.dependencies[i]));
                }
            }
            module.entity = module.factory.apply(function () { }, _args);
        }
        return module.entity;
    }

    /**
     * 模块获取
     * @name require
     * @param {String} name 
     */
    AMD.require = function require(name) {
        return this.emit(name);
    }

    global.define = function (name, dependencies, factory) {
        AMD.define(name, dependencies, factory);
    }

    global.require = function (name) {
        return AMD.require(name);
    }

})(window)
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>define-demo</title>
</head>
<body>
<script src="amd-define.js"></script>
<script>
    define("test-1", [], function(){
        return {
            name : "test-1",
            func : function(){
                console.log("test-1");
                document.write("<p>test-1</p>");
            }
        }
    });

    define("test-2", function(){
        return {
            name : "test-2",
            func : function(){
                console.log("test-2");
                document.write("<p>test-2</p>");
            }
        }
    });

    define(["test-1", "test-2"], function(t1, t2){
        console.log("exec module-1");
        document.write("<p>exec module-1</p>");
        t1.func();
        t2.func();
    });

    define(function(){
        console.log("exec module-2");
        document.write("<p>exec module-2</p>");
    })

</script>
</body>

</html>
```

