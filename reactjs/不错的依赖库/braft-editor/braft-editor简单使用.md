# [braft-editor](https://github.com/margox/braft-editor)

这是一个基于  [draft-js](https://draftjs.org/)的Web富文本编辑器，适用于React框架，兼容主流现代浏览器。 

## 简单封装使用

```js
	
	import React, { Component } from 'react'

// 引入编辑器以及编辑器样式
import BraftEditor from 'braft-editor'
import 'braft-editor/dist/braft.css'
import styles from './index.less'

class Editor extends Component {

  constructor(props) {
    super(props);
    this.state = {}

  }

  /**
   * 获取编辑器内容
   */
  handleEditerHTMLChange = (value) => {
    const { onChange } = this.props;
    onChange && onChange(value);
  }



  render() {
    const { value } = this.props;
    const editorProps = {
      height: 500,
      initialContent: value ? value : '<p>hello world!<p>',
      contentFormat: "html",
      language: "zh-cn",
      onHTMLChange: this.handleEditerHTMLChange,
      placeholder: "请输入文章内容",
      media: {
        image: true, // 开启图片插入功能
        video: false, // 开启视频插入功能
        audio: false, // 开启音频插入功能
        validateFn: null, // 指定本地校验函数，说明见下文
        uploadFn: uploadFn // 指定上传函数，说明见下文
      }
    }

    return (
      <div className={styles.box}>
        <BraftEditor {...editorProps} />
      </div>
    )
  }
}

export default Editor;

```

```css
.box{
  :global{
    .BraftEditor-controlBar {
      border: 1px solid #bbb;
      
    }
    .DraftEditor-editorContainer {
      border: 1px solid #bbb;
    }
  }
}

```















