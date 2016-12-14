# XHRCreep.js

A complete wrapper for XMLHttpRequest (and ActiveX) that provides hooks to override and monitor method calls and events on the XHR contructor.

## Bird's Eye View:

XHRCreep looks like this... 

    XHRCreep = {
            methods:{
    			notify: {
    				open: function(){},
    				send: function(){},
    				setRequestHeader: function(){},
    				overrideMimeType: function(){},
    				getResponseHeader: function(){},
    				getAllResponseHeaders: function(){},
    				abort: function(){}
    			},
    			override: {
    				open: false,
    				send: false,
    				setRequestHeader: false,
    				overrideMimeType: false,
    				getResponseHeader: false,
    				getAllResponseHeaders: false,
    				abort: false
    			}
    		},
    		events:{
    			onreadystatechange: function(){ return true; },
    			onabort: function(){ return true; },
    			onerror: function(){ return true; },
    			onload: function(){ return true; },
    			onloadstart: function(){ return true; },
    			ontimeout: function(){ return true; },
    			onloadend: function(){ return true; }
    		}
        }
        
### XHRCreep.methods.notify

 Provides a set of set of methods which will be called whenever the equivalent function is called on an XHR instance. Inside these functions, `this` refers to the XHR wrapper. The same arguments passed to the XHR method are passed to the notify function as well.
 
### XHRCreep.methods.override

 Provides a set of set of methods which will be called whenever the equivalent function is called on an XHR instance. Inside these functions, `this` refers to the XHR wrapper. The same arguments passed to the XHR method are passed to the notify function as well. When these functions are used, the wrapper library no longer performs the test required by the function, it must be done in the callback itself. The wrapped XHR object is located in `this._xhr`.

### XHRCreep.events

 Provides a set of set of methods which will be called whenever the equivalent event occurs on an XHR instance. Inside these functions, `this` refers to the XHR object being wrapped. If `false` is returned from these methods the original event will be overriden (not fired).

## Example

Aside from the example given, there is a more complex one [here](https://github.com/Pamblam/jSQL/tree/master/plugins/xhrCache), which uses XHRCreep to cache AJAAX responses.

## License & Legal

License info is available [here](https://github.com/Pamblam/jSQL/wiki/License).
