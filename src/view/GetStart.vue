<template>
  <article class="markdown-body">
    <h1>
      开始使用
    </h1>

    <p>请先<a href="#/doc/install">安装</a>本组件库。</p>
    <p>然后在你的代码中写入下面的代码</p>
    <pre><code>import {Button} from 'wind-ui-1'</code><br/><code>import 'wind-ui-1/dist/lib/wind-ui.css'</code></pre>
    就可以使用我提供的组件了。
    <br/>
    <br/>
    <strong>注意：在使用库文件时，以下组件代码示例中的 <code>'../lib/index'</code> 全部替换为 <code>'wind-ui-1'</code></strong>
    <h2>Vue 单文件组件</h2>
    <p>代码示例：</p>
    <pre><code>&lt;template&gt;
  &lt;div&gt;&lt;Button&gt;按钮&lt;/Button&gt;&lt;/div&gt;
&lt;/template&gt;
&lt;script&gt;
  import {Button} from 'wind-ui-1'
  import 'wind-ui-1/dist/lib/wind-ui.css'
  export default {
    components: {Button}
  }
&lt;/script&gt;
 </code></pre>

  </article>
</template>

<script>
export default {
  name: "GetStart"
}
</script>

<style scoped>

</style>