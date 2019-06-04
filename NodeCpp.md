[TOC]

# 1 - Hello World

### Project Setup

- Init project, run `npm init`
- Add other libraries, edit `package.json`

```json
# add "dependencies": node-addon-api, node-gyp, bindings
# add "gypfile": true
{
  "name": "addon",
  "version": "1.0.0",
  "description": "",
  "main": "hello.js",
  "scripts": {
    "test": "node hello.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "node-addon-api": "^1.6.3",  
    "node-gyp": "^4.0.0",
    "bindings": "^1.5.0"		//"*"
  },
  "gypfile": true
}
```

- Add files : `binding.gyp`, ` <name>.cc`,  `<name>.js `

  - binding.gyp

    ```json
    {
      "targets": [
        {
          "target_name": "<name>",
          "cflags!": [ "-fno-exceptions" ],
          "cflags_cc!": [ "-fno-exceptions" ],
          "sources": [ "<name>.cc" ],
          "include_dirs": [
            "<!@(node -p \"require('node-addon-api').include\")"
          ],
          'defines': [ 'NAPI_DISABLE_CPP_EXCEPTIONS' ],
        }
      ]
    }
    ```
    
- <name>.cc
  
    ```c
    #include <napi.h>
        
    Napi::String Method(const Napi::CallbackInfo& info) {
      Napi::Env env = info.Env();
      return Napi::String::New(env, "world");
    }
        
    Napi::Object Init(Napi::Env env, Napi::Object exports) {
      exports.Set(Napi::String::New(env, "hello"),
    		Napi::Function::New(env, Method));
      return exports;
    }
        
    NODE_API_MODULE(hello, Init)
    ```
    
  - <name>.js
  
    ```js
    var addon = require('bindings')('hello');
    console.log(addon.hello()); // 'world'
    ```

- Run `npm install` to build project
- Test the code:
  - (if not first build) run `node-gyp rebuild` before test
  - Run `npm test` to test, then get `'world'` printed in console

### Error

- `node-gyp rebuild` : build error - older 'node-addon-api' version don't have <napi.h>

> ```
> gyp info spawn args   '-Goutput_dir=.' ]
> internal/modules/cjs/loader.js:582
>     throw err;
>     ^
>     Error: Cannot find module 'node-addon-api'
>     at Function.Module._resolveFilename (internal/modules/cjs/loader.js:580:15)
>     at Function.Module._load (internal/modules/cjs/loader.js:506:25)
>     at Module.require (internal/modules/cjs/loader.js:636:17)
>     at require (internal/modules/cjs/helpers.js:20:18)
>     at [eval]:1:1
>     at Script.runInThisContext (vm.js:96:20)
>     at Object.runInThisContext (vm.js:303:38)
>     at Object.<anonymous> ([eval]-wrapper:6:22)
>     at Module._compile (internal/modules/cjs/loader.js:688:30)
>     at evalScript (internal/bootstrap/node.js:582:27)
> gyp: Call to 'node -p "require('node-addon-api').gyp"' returned exit status 1 while in binding.gyp. while trying to load binding.gyp
> gyp ERR! configure error
> ```
>
> Solution:  `npm install` latest version



# 2 - Function Arguments







# Reference

- [nodes/node-addon-api github](https://github.com/nodejs/node-addon-api#examples)

- [node-gyp github](https://github.com/nodejs/node-addon-api/blob/master/doc/setup.md)
