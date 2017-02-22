# XHRCreep.js

A complete wrapper for XMLHttpRequest (and ActiveX - for some reason) that provides hooks to override and monitor method calls and events on XHR.

XHRCreep works by re-writing and re-assigning XMLHttpRequest (or ActiveX) with a wrapper class and inserting hooks. The benefit of this is that you can change read-only properties and override and monitor all requests for debugging or analytics purposes. The drawback of this is that it's really easy to tie your code in knots if not used properly.

All by itself, XHRCreep does absolutely nothing. All it does is expose hooks that can be set to be called when other methods/events are called/fired.

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

 Provides a set of set of hooks which will be called whenever the equivalent function is called on an XHR instance. Inside these functions, `this` refers to the XHR wrapper. The same arguments passed to the XHR method are passed to the notify function as well.

    XHRCreep.methods.notify.open=function(){
		console.log("Requesting "+arguments[0]);
    } 

### XHRCreep.methods.override

 Provides a set of set of hooks which will be called whenever the equivalent function is called on an XHR instance. Inside these functions, `this` refers to the XHR wrapper. The same arguments passed to the XHR method are passed to the notify function as well. When these functions are used, the wrapper library no longer calls the equivalent function on the real XHR instance, it must be done in the callback itself. The wrapped XHR object is located in `this._xhr`.

    XHRCreep.methods.override.open=function(){
		console.log("Requesting "+arguments[0]);
		this._xhr.open.apply(_this, arguments);
    }

### XHRCreep.events

 Provides a set of set of methods which will be called whenever the equivalent event occurs on an XHR instance. Inside these functions, `this` refers to the XHR object being wrapped. If `false` is returned from these methods the original event will be overriden (not fired).

## Example

Aside from the example given, there is a more complex one [here](https://github.com/Pamblam/jSQL/tree/master/plugins/xhrCache), which uses XHRCreep to cache AJAAX responses.

## License & Legal

License info is available [here](https://github.com/Pamblam/jSQL/wiki/License).
