## 问题描述
小程序音频进入页面播放音频，返回上一页后重新进入播放页面，onTimeUpdate 等监听事件失效不执行。 

## 问题原因
由于 onTimeUpdate 等监听事件在再次进入页面失效不执行，二次进去界面的时候消息没办法传递出去，导致页面出错没有更新页面数据。 

## 解决方案
需使用 [my.offAudioInterruptionBegin ](https://opendocs.alipay.com/mini/00jim9)和 [my.offAudioInterruptionEnd](https://opendocs.alipay.com/mini/00jfja) 取消之前的音频监听事件然后重新监听。<br />**注意：**需将所有监听事件取消掉后再监听，且开启监听事件 `onXxx` 与取消监听事件 `offXxx` 入参需要是同一个函数的引用。<br /> 
