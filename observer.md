## 观察者模式
[参考汤姆大叔博客](https://www.cnblogs.com/TomXu/archive/2012/03/02/2355128.html)

```javascript

function Observer () {
    this._evts = {}
    this._uid = -1
}

Observer.prototype = {
    on : function (eventName, cb) {
        if(!this._evts[eventName]) {
            this._evts[eventName] = []
        }
        var token = this._uid++
        this._evts[eventName].push({
            fnc: cb,
            token
        })
        return token
    },

    trigger: function(eventName,arg,ctx) {
        if(!this._evts[eventName]) {
            return false
        }
        setTimeout( ()=> {
            var evt = this._evts[eventName]
            var len = this._evts[eventName].length
            while(len--) {
                evt[len].fnc.call(ctx,arg)
            }
        },0)
    },

    off: function(token) {
        var evts = this._evts
        for (let evtName in evts) {
            for(let i = 0; i < evts[evtName].length; i++ ) {
                if(evts[evtName][i].token === token) {
                    evts[evtName].splice(i,1)
                    return 
                }
            }
        }
    }
}

var observer = new Observer()
var token1 = observer.on('eg1', function(data) {
    console.log(`eg1data: ${data}`)
})

observer.on('eg2', function(data) {
    console.log(`eg2data: ${data}`)
})

observer.trigger('eg1','demoeg1data')
observer.off(token1)
observer.trigger('eg1','demoeg1data22222222')
```