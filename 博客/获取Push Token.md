**【需求】**

- 获取 Push Token

**【文档】**

- <https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/push-get-token-V5>

**【代码】**

```typescript
// EntryAbility.ets 文件

import { pushService } from '@kit.PushKit'

export default class EntryAbility extends UIAbility {
  onCreate(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    hilog.info(0x0000, 'testTag', '%{public}s', 'Ability onCreate')
    getPushToken()
  }
}

/**
 * 获取Push Token
 */
async function getPushToken() {
  try {
    const pushToken: string = await pushService.getToken()
    hilog.info(
      0x0000,
      'testTag',
      `Succeeded in getting push token: ${pushToken}`
    )
    // 上报Push Token并上报到您的服务端
  } catch (err) {
    let e: BusinessError = err as BusinessError
    hilog.error(
      0x0000,
      'testTag',
      'Failed to get push token: %{public}d %{public}s',
      e.code,
      e.message
    )
  }
}
```

**【报错一】**

1\. 报错 1000900010 APP 身份验证失败
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/563d0563869b4390bb1928b673940823.png)

2\. 文档：<https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/push-error-code-V5#section3835124673016>

3\. 跟据文档提示配置应用签名
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/4c04a1c1b59c4ca59b8318699d98604c.png)

【报错二】

1\. 报错（1000900012 未开通推送服务权益）
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/03f85865fadd4d61aef6f4b26d7e9f15.png)

2\. 文档：<https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/push-config-setting-V5#section13206419341>

3\. 开通推送服务权益（根据文档开通）

3.1. 登录[AppGallery Connect](https://developer.huawei.com/consumer/cn/service/josp/agc/index.html)网站，选择“我的项目”。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/3a76faf685624d3cb1d581be6c693cc0.png)

3.2. 在项目列表中找到您的项目，在项目下的应用列表中选择需要配置推送服务参数的应用。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/c12c82a4d2e14afe98da07be014505f2.png)

3.3. 在左侧导航栏选择“增长 > 推送服务”，点击“立即开通”，在弹出的提示框中点击“确定”。至此，您已可以向应用推送通知消息。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/99fd214e461a41e193a0bf82edf93e3d.png)

3.4. 在“项目设置 > API 管理”中，确认已经开启“推送服务”开放能力，并完成[手动签名](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-signing-V5#section297715173233)。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/3bab0122134d4951af4d47203f59718a.png)

**【测试】**

重新运行项目，已经能获取 push token 了
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/08a6c9b6634b463182825f4ed5933d39.png)
