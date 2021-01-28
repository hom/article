Web 网站的用户登录注册方式有用户名密码登录、验证码登录、OAuth 第三方授权登录等。

常用的第三方登录有 QQ、微信、微博、GitHub、知乎等，一般用户常用微信扫码授权的登录方式，今天介绍一下网站接入微信登录的方法。

## 应用申请

网站应用中接入微信登录是基于OAuth2.0协议标准构建的微信OAuth2.0授权登录系统。

 在进行微信OAuth2.0授权登录接入之前，需要在微信开放平台注册开发者帐号，并拥有一个已审核通过的网站应用，并获得相应的AppID和AppSecret，申请微信登录且通过审核后，才能开始接入微信登录流程。

![wechat-open-platform-to-add-application](https://cdn.pongj.com/uPic/20210128-1611814943024-vtVpKW.jpg)

在管理中心-网站应用-创建网站应用中完善网站的基本信息，在第 2 步中完善网站的内容和运营者信息，提交给微信开放平台审核即可。

网站应用审核通过后会为网站应用生成 AppID 和 AppSecret，在接下来的接入流程中需要使用到 AppID 和 AppSecret。

![wechat-open-platform-application](https://cdn.pongj.com/uPic/20210128-1611814910094-MHQgWM.png)

## 接入微信

微信开放平台的[网站应用文档](https://developers.weixin.qq.com/doc/oplatform/Website_App/WeChat_Login/Wechat_Login.html)中详细讲解了如何为应用接入微信登录，下面我们以实际应用的方式来详细介绍一下如何接入微信登录，我的小站已经接入了微信登录，想看效果的看官可以移步[这里](https://zi.pongj.com)。

接入微信登录需要获取到用户的 `openid` 和 `unionid`，简单来说分为三步：

1. 调用开放接口获取授权
2. 通过授权后的 code 获取 access_token
3. 使用access_token获取用户信息

### 获取授权

获取授权的过程就是让微信用户使用手机等移动设备扫码网站提供的 OAuth 标准的二维码链接，然后用户在微信中授权应用来使用用户的个人信息。

下图是微信开放平台提供的获取 `access_token` 的时序图：

![](https://res.wx.qq.com/op_res/D0wkkHSbtC6VUSHX4WsjP5ssg5mdnEmXO8NGVGF34dxS9N1WCcq6wvquR4K_Hcut)

接下来对图中的步骤进行简要的说明：

1. 请求登录第三方应用

   即用户从浏览器中搜索网站关键字，或者输入网站地址进入到我们的网站应用。

2. 请求微信 OAuth2.0 授权登录

   这一步，我们只需要在网站的登录页面中添加微信授权登录的超链接即可，在链接的地址中添加上网站应用在微信开放平台中的 AppID 和授权成功后重定向的网站地址。

   链接的形式：

   ```
   https://open.weixin.qq.com/connect/qrconnect?appid=APPID&redirect_uri=REDIRECT_URI&response_type=code&scope=SCOPE&state=STATE#wechat_redirect
   ```

   其中：

   - appid：应用的 AppID

   - redirect_uri：用户允许授权之后微信重定向回网站的地址，需要在微信开放平台的网站应用中配置“授权回调域”。

     比如我的网站应用中的回调域配置的是网站的域名地址，因此回调的页面只要在该域名下就可以：

     ![wechat-open-platform-config-page](https://cdn.pongj.com/uPic/20210128-1611814870842-XLwET4.png)

   - response_type：请求用户授权的地址中这里填写 `code`。
   - scope：应用授权作用域，拥有多个作用域用逗号（,）分隔，网页应用目前仅填写snsapi_login即可。

   - state：该参数可选，用于保持请求和回调的状态，授权请求后原样带回给第三方。该参数可用于防止csrf攻击（跨站请求伪造攻击），建议第三方带上该参数，可设置为简单的随机数加session进行校验。

   我的网站应用中的链接地址如下：

   ```
   https://open.weixin.qq.com/connect/qrconnect?appid=wxb6a3d3490ab4c2cd&redirect_uri=https://zi.pongj.com/oauth/wechat/login&response_type=code&scope=snsapi_login&state=STATE#wechat_redirect
   ```

   然后在登录的页面中将链接地址添加超链接：

   ```
   <a
     href="https://open.weixin.qq.com/connect/qrconnect?appid=wxb6a3d3490ab4c2cd&redirect_uri=https://zi.pongj.com/oauth/wechat/login&response_type=code&scope=snsapi_login&state=STATE#wechat_redirect"
   >
     <img
       title="微信"
       alt="微信"
       src="//sf6-scmcdn2-tos.pstatp.com/xitu_juejin_web/img/wechat.e0ff124.svg"
       class="oauth-btn"
     />
   </a>
   ```

   ![login-page](https://cdn.pongj.com/uPic/20210128-1611814839838-bABCAD.png)

3. 请求用户确认

   在登录页面中添加了微信登录的超链接，用户点击微信登录的按钮之后就进入到了微信的域中，页面中会出现网站应用的基本信息和授权的二维码请求用户进行扫码授权。

   ![request-wechat-user-to-scan](https://cdn.pongj.com/uPic/20210128-1611814802453-ZccgDn.png)

   可以从页面中看到，地址栏中的地址信息包含了我们配置的地址信息，页面中的二维码将我们的网站应用的名称显示在二维码的下方。

   此时用户扫描二维码之后，该二维码会同步显示用户的授权状态：

   ![request-wechat-user-to-authorize](https://cdn.pongj.com/uPic/20210128-1611814770888-rsH68y.png)

   同时在微信客户端中，我们也看到了应用的名称和 Logo 的基本信息：

   <img src="https://cdn.pongj.com/uPic/20210128-1611814715941-szt4KH.PNG" alt="request-wechat-user-" style="zoom:25%;" />

4. 用户确认

   用户在手机中“同意”授权之后，网站应用中的微信登录页面会跳转到我们在链接地址中配置的 `redirect_url` 的页面

5. 拉起第三方应用或重定向到第三方，带上授权的临时票据（`code`）

   用户同意授权之后，微信登录页面在重定向到 `redirect_uri` 的页面时，会在 `redirect_uri` 地址后添加上临时的 `code`，我们在开发 `redirect_uri` 页面的时候可以判断地址中是否包含 `code` 来确定用户是否授权。

   比如我的网站回调页面就会变成：

   ```bash
   https://zi.pongj.com/oauth/login/wechat?code=code&state=state
   ```

6. 通过 `code` 加上 AppID 和 AppSecret 来获取 `access_token`

   我们在 `redirect_uri` 的页面中检查到地址中包含了 `code` 的参数，并且用户已授权，然后我们就可以使用 `code` 来获取 `access_token`。

   需要注意的是，由于 AppSecret 在应用中属于私密数据，所以此处获取 access_token 需要在服务器中调用，千万不要在浏览器端调用而导致 AppSecret 泄露。

   

### 获取用户信息

下面是我作为开发者在微信开放平台的时序图的基础上补充了网站应用的前后端数据交互过程：

![wechat-oauth-login](https://cdn.pongj.com/uPic/20210128-1611812794239-HfhHOi.png)

在获取到用户授权，也就是获取到 `code` 之后，接下来网站应用的步骤就是从上图中的 5-11 步骤所示，之前的步骤在上面已经介绍过了，接下来详细的介绍一下 5-11 步骤操作：

**第 5 步：**

在网站应用的 `redirect_uri` 页面中添加路经检测逻辑，检查是否带有 `code` 参数：如果带有 `code` 参数，表明用户已同意授权；如果未带有 `code` 参数，则说明用户拒绝或关闭了授权页面，此时需要重定向到登录页面，并提醒用户登录失败。

下面是我的 Nuxt.js 项目中的校验代码块：

```javascript
const { code } = this.$route.query
if (!code) {
  this.$notify.warning('请重新登录')
  return this.$router.push('/login')
}
```

**第 6 步：**

获取到了 `code` 参数，然后就需要获取授权的 `access_token` ，获取 `access_token` 需要使用 AppID 和 AppSecret，由于涉及到 AppSecret 的安全性，因此我们将请求发送到后端进行操作。

**第 7 步：**

通过传到后端的 `code` 参数，以及保存在环境变量或者配置文件中的 AppSecret 来获取 access_token。

获取 access_token 的请求地址格式如下：

```bash
https://api.weixin.qq.com/sns/oauth2/access_token?appid=APPID&secret=SECRET&code=CODE&grant_type=authorization_code
```

其中：

- appid：应用唯一标识，在微信开放平台提交应用审核通过后获得
- secret：应用密钥AppSecret，在微信开放平台提交应用审核通过后获得
- code：填写获取到的code参数
- grant_type：填authorization_code

在 Node.js 中使用 `request` 或者 `got` 等模块向微信开发平台发送 `GET` 请求。

**第 8 步：**

请求发送成功之后，微信开放平台会返回包含有 `access_token` 的返回值。

返回结果：

```json
{ 
  "access_token":"ACCESS_TOKEN", 
  "expires_in":7200, 
  "refresh_token":"REFRESH_TOKEN",
  "openid":"OPENID", 
  "scope":"SCOPE",
  "unionid": "o6_bmasdasdsad6_2sgVt7hMZOPfL"
}
```

其中，`access_token`是调用授权关系接口的调用凭证，由于`access_token`有效期（目前为2个小时）较短，当`access_token`超时后，可以使用`refresh_token`进行刷新，刷新的操作只需要加上 `refresh_token` 并调用接口即可，详细的操作可以查看[官方文档](https://developers.weixin.qq.com/doc/oplatform/Website_App/WeChat_Login/Wechat_Login.html)

可以看到返回的结果中包含了用户的 `openid` 和 `unionid`，这两个字段用户对于网站应用是固定不变的，因此我们可以在此处通过 `openid` 和 `unionid` 来判断该微信用户是否在我们的网站中已经注册过，如果注册过，直接生成合法的 `token` 值返回到前端页面即可；如果用户未在网站中注册，那么我们需要先获取到用户的个人信息，然后再生成 `token`

**第 9 步：**

获取到 `access_token` 之后，并判断用户未在网站应用中注册，我们就需要获取用户信息，来保存用户的授权登录信息。

获取用户信息，需要调用下面的 API 接口：

```bash
https://api.weixin.qq.com/sns/userinfo?access_token=access_token&openid=openid
```

其中：

- access_token：填写我们获取到的 `access_token`
- openid：用户的个人信息 `openid`，在上一步中的返回结果中包含了 `openid`

**第 10 步：**

微信开放平台请求校验通过后会返回用户的基本个人信息，包括昵称、头像、性别等。

返回结果：

```json
{
  "openid":"OPENID",
  "nickname":"NICKNAME",
  "sex":1,
  "province":"PROVINCE",
  "city":"CITY",
  "country":"COUNTRY",
  "headimgurl": "https://thirdwx.qlogo.cn/mmopen/g3MonUZtNHkdmzicIlibx6iaFqAc56vxLSUfpb6n5WKSYVY0ChQKkiaJSgQ1dZuTOgvLLrhJbERQQ4eMsv84eavHiaiceqxibJxCfHe/0",
  "privilege":[
  "PRIVILEGE1",
  "PRIVILEGE2"
  ],
  "unionid": " o6_bmasdasdsad6_2sgVt7hMZOPfL"

}
```

到这一步，我们已经获取到了用户的个人信息，下面我们就需要将用户的信息保存在我们的数据库中，在下一次用户扫码微信登录的时候，可以直接返回用户的登录 `token`，而不需要再从微信平台中获取个人信息了。

如果网站应用还需要用户补充其他的个人信息，那么我们可以在此步骤中先将用户的微信信息存储起来，然后将请求重定向到补充信息的页面中，提示用户补充额外的信息。

由于我的网站中需要使用用户的邮箱地址和手机号信息来通知，因此我在回调的地址中添加了补充信息的页面，想看效果的的同学可以[尝试一下](https://zi.pongj.com)。

第 11 步：

数据库中已经生成了用户的登录授权信息，系统生成合法的 `token` 值返回给前端页面，前端页面来标识用户已登录成功，并跳转到网站的首页。

```javascript
if (result.token) {
  await this.$store.dispatch('user/oauth', result.token)
  this.$notify.success('登陆成功')
  setTimeout(() => {
    this.$router.push('/')
  }, 3000)
  return
}

this.$notify.success('请重新登录')
setTimeout(() => {
  this.$router.push('/login')
}, 3000)
```

## 参考

- 微信开放平台网站应用官方文档[地址](https://developers.weixin.qq.com/doc/oplatform/Website_App/WeChat_Login/Wechat_Login.html)