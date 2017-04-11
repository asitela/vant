<style>
@component-namespace demo {
  @b toast {
    .zan-button {
      margin: 15px;
    }
  }
}
</style>

<script>
import { Toast } from 'src/index';

export default {
  methods: {
    showSimpleToast() {
      Toast('我是提示文案，建议不超过十五字~');
    },
    showLoadingToast() {
      Toast.loading();
    },
    showSuccessToast() {
      Toast.success('成功文案');
    },
    showFailToast() {
      Toast.fail('失败文案');
    },
    showForbidClickToast() {
      Toast({
        message: '背景不能点击',
        forbidClick: true
      })
    },
    showCustomizedToast(duration) {
      let leftSec = duration / 1000;
      let toast = Toast({
        duration: duration + 1000,
        type: 'success',
        message: leftSec.toString()
      });
      const id = window.setInterval(() => {
        if (leftSec <= 1) {
          window.clearInterval(id);
          toast.message = '跳转中...'
          return;
        }
        toast.message = (--leftSec).toString();
      }, 1000);
    },
    showToast() {
      this.toast = Toast('我是提示文案，建议不超过十五字~');
    },
    closeToast() {
      this.toast.clear();
    },
    showHtmlToast() {
      Toast({
        type: 'html',
        message: '<em>HTML<em>'
      })
    }
  }
};
</script>

## Toast 轻提示

### 使用指南

`Toast`和其他组件不同，不是通过HTML结构的方式来使用，而是通过函数调用的方式。使用前需要先引入它。

```js
import { Toast } from '@youzan/zanui-vue';
```

### 代码演示

#### 基础用法

:::demo 基础用法
```html
<zan-button @click="showSimpleToast">普通文字提示</zan-button>
<zan-button @click="showLoadingToast">加载Toast</zan-button>
<zan-button @click="showSuccessToast">成功</zan-button>
<zan-button @click="showFailToast">失败</zan-button>
<zan-button @click="showForbidClickToast">背景不能点击</zan-button>
<zan-button @click="showCustomizedToast(5000)">倒数5秒</zan-button>

<script>
import { Toast } from 'src/index';

export default {
  methods: {
    showSimpleToast() {
      Toast('我是提示文案，建议不超过十五字~');
    },
    showLoadingToast() {
      Toast.loading();
    },
    showSuccessToast() {
      Toast.success('成功文案');
    },
    showFailToast() {
      Toast.fail('失败文案');
    },
    showForbidClickToast() {
      Toast({
        message: '背景不能点击',
        forbidClick: true
      })
    },
    showCustomizedToast(duration) {
      let leftSec = duration / 1000;
      let toast = Toast({
        duration: duration + 1000,
        type: 'success',
        message: leftSec.toString()
      });
      const id = window.setInterval(() => {
        if (leftSec <= 1) {
          window.clearInterval(id);
          toast.message = '跳转中...'
          return;
        }
        toast.message = (--leftSec).toString();
      }, 1000);
    }
  }
};
</script>
```
:::

#### 手动关闭

:::demo 手动关闭
```html
<zan-button @click="showToast">打开</zan-button>
<zan-button @click="closeToast">关闭</zan-button>

<script>
import { Toast } from 'src/index';

export default {
  methods: {
    showToast() {
      Toast('我是提示文案，建议不超过十五字~');
    },
    closeToast() {
      Toast.clear();
    }
  }
};
</script>
```
:::


#### 传入html

:::demo 手动关闭
```html
<zan-button @click="showHtmlToast">打开</zan-button>

<script>
import { Toast } from 'src/index';

export default {
  methods: {
    showHtmlToast() {
      Toast({
        type: 'html',
        message: '<em>HTML<em>'
      })
    }
  }
};
</script>
```
:::


### 基础用法

#### Toast(options)

| 参数       | 说明      | 类型       | 默认值       | 可选值       |
|-----------|-----------|-----------|-------------|-------------|
| type | 类型 | String  | 'text' | 'text', 'loading', 'success', 'fail', 'html'  |
| message | 内容 | String  | '' | - |\| message | 内容 | String  | '' | - 
| forbidClick | 不允许背景点击 | Boolean  | false | true, false|
| duration | 时长(ms) | Number  | 3000ms | -|

### 快速用法

#### Toast(message) || Toast(message, options)

| 参数       | 说明      | 类型       | 默认值       | 可选值       |
|-----------|-----------|-----------|-------------|-------------|
| message | 内容 | String  | '' | - |
| forbidClick | 不允许背景点击 | Boolean  | false | true, false|
| duration | 时长(ms) | Number  | 3000ms | -|

#### Toast.loading() || Toast.loading(message, options)

| 参数       | 说明      | 类型       | 默认值       | 可选值       |
|-----------|-----------|-----------|-------------|-------------|
| forbidClick | 不允许背景点击 | Boolean  | false | true, false|
| duration | 时长(ms) | Number  | 3000ms | -|

#### Toast.success(message) || Toast.success(message, options)

| 参数       | 说明      | 类型       | 默认值       | 可选值       |
|-----------|-----------|-----------|-------------|-------------|
| type | 类型 | String  | 'text' | 'text', 'loading', 'success', 'failure'  |
| forbidClick | 不允许背景点击 | Boolean  | false | true, false|
| duration | 时长(ms) | Number  | 3000ms | -|

#### Toast.fail(message) || Toast.fail(message, options)

| 参数       | 说明      | 类型       | 默认值       | 可选值       |
|-----------|-----------|-----------|-------------|-------------|
| type | 类型 | String  | 'text' | 'text', 'loading', 'success', 'failure'  |
| forbidClick | 不允许背景点击 | Boolean  | false | true, false|
| duration | 时长(ms) | Number  | 3000ms | -|

#### Toast.clear()

关闭toast。