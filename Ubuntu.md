# Ubuntu 笔记

1. **使用防火墙对端口进行控制**
sudo ufw status
sudo ufw allow 80
sudo ufw enable
sudo ufw reload
2. **jupyter安装后访问不到的原因**
小飞机哈哈哈哈
3. **tensorflow虽然安装成功但是导入不成功**
实验室的机器太老不支持avx指令，但是现在的tensorflow都是用avx编译的，如果非要用可以尝试从源代码进行编译。
