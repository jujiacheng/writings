# 'Send files or execute commands over SSH' changed build result to UNSTABLE 的可能性

## 情况一：输出路径不对

![img](../../assets/工具/06_jenkins报错/01.png)

![img](../../assets/工具/06_jenkins报错/02.png)

这里全局的 Remote Directory 是绝对路径

![img](../../assets/工具/06_jenkins报错/03.png)

工程内部的 Remote Directory 是相对路径，和全局的 Remote Directory 两者拼接后为打
包后的输出路径，切记切记
