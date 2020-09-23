# egg-obelisk

gRPC framework for egg

## Features

1. Support gRPC + ProtoFuf
2. Extend EGG Router To Support RPC Method
3. It Supports EGG Middleware、Plugin
4. It Supports Both HTTP、gRPC Request，Common Use Controller And Service

## QuickStart

```bash
$ npm install egg-obelisk --save
```

```json
// {app_root}/package.json
{
  "name": "user",
  ...
  "egg": {
    ...
    "framework": "egg-obelisk"
  },
  ...
}
```

```js
// {app_root}/app/router.js
'use strict';

module.exports = app => {
  const { router, controller } = app;
  router.rpc('/user/login', controller.user.login);
};
```

```js
// {app_root}/app/controller/user.js
'use strict';

const Controller = require('egg').Controller;

class UserController extends Controller {

  async login() {
    const body = this.ctx.request.body;
    const result = await this.service.user.login(body);
    this.ctx.body = result;
  }

}

module.exports = UserController;
```

```js
// {app_root}/app/service/user.js
'use strict';

const Service = require('egg').Service;

class UserService extends Service {

  async login() {
    // ...
    return { state: 'ok' };
  }

}

module.exports = UserService;
```
