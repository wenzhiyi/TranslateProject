如何让黑客远离你的 Linux 第三部分：问题回答
============================================================

 ![Computer security](https://www.linux.com/sites/lcom/files/styles/rendered_file/public/keep-hackers-out.jpg?itok=lqgHDxDu "computer security") 
Mike Guthrie 最近在 Linux 基金会的网络研讨会上回答了一些安全相关的问题。随时观看免费的研讨会。[Creative Commons Zero][1]

这个系列的[第一篇][6]和[第二篇][7]文章覆盖了 5 个最简单的方法来让你的 Linux 远离黑客，并且知道他们是否已经进入。这一次，我将回答一些我最近在 Linux 基金会网络研讨会上收到的很好的安全性问题。[随时观看免费网络研讨会][8]。

**如果系统自动使用私钥认证，如何存储密钥密码？**

这个很难。这是我们一直在斗争的事情，特别是我们在做 “Red Teams” 的时候，因为我们有自动回调它的东西。我使用 Expect，但我倾向于在这上面使用老方法。你将要编写脚本，是的，将密码存储在系统上将是艰难的，当你这么做时你需要加密它。

我的 Expect 脚本加密了存储的密码，然后解密，发送密码，并在完成后重新加密。我意识到这有一些缺陷，但它比使用无密码的密钥更好。

如果你有一个无密码的密钥，并且你确实需要使用它。我建议你最大化地限制需要它的用户。例如，如果你正在进行一些自动日志传输或自动化软件安装，则只给那些需要执行这些功能的程序权限。

你可以通过 SSH 运行命令，所以不要给它们一个 shell，使它只能运行那个命令，这样就能防止某人窃取了这个密钥并做其他事情。

**你对密码管理器如 KeePass2 怎么看？**

对我而言密码管理器是一个非常好的目标。随着 GPU 破解的出现和 EC2 的一些破解能力，这些很容易就变成过去。我一直在窃取密码库。

现在，我们在破解这些库的成功率是一个不同的故事。我们仍然有 10% 左右的破解成功率。如果人们不能为他们的密码库保留一个安全密码，那么我们就会进入并会获得大量的成功。它没有什么好，但是你仍需要保护好这些资产。如你保护其他密码一样保护好密码库。

**你认为从安全的角度来看，除了创建具有更高密钥长度的主机密钥之外，创建一个新的 “Diffie-Hellman” moduli 并限制 2048 位或更高值得么？**

值得的。以前在 SSH 产品中存在弱点，你可以做到解密数据包流。有了它，你可以拉取各种数据。作为一种加密机制，人们不假思索使用这种方式来传输文件和密码。使用健壮的加密并且改变你的密钥是很重要的。 我会轮换我的 SSH 密钥 - 这不像我的密码那么频繁，但是我每年会轮换一次。是的，这是一个麻烦，但它让我安心。我建议尽可能地使你的加密技术健壮。

**使用完全随机的英语单词（大概 10 万个）作为密码合适么？**

当然。我的密码实际上是一个完整的短语。它是带标点符号和大小写一句话。我不再使用其他任何东西。

我是有一个你可以记住的密码而不用写下来或者放在密码库的大大的支持者。一个你可以记住不必写下来的密码比你需要写下来的密码更安全。

使用短语或使用你可以记住的四个随机单词比那些需要经过几次转换的一串数字和字符的字符串更安全。我目前的密码长度大约是 200 个字符。这是我可以快速打出来并且记住的。

**在物联网情景下对保护基于 Linux 的嵌入式系统有什么建议么？**

物联网是一个新的空间，它是系统和安全的前沿。它每一天都是不同的。现在，我尽量都保持离线。我不喜欢人们把我的灯光和冰箱搞乱。我故意没有购买已经联网的冰箱，因为我有朋友是黑客，我知道我每天早上醒来都会看到不适当的图片。封住它，锁住它，隔离它。

目前物联网设备的恶意软件取决于默认密码和后门，所以只需要对你所使用的设备进行一些研究，并确保没有其他人可以默认访问。然后确保这些设备的管理接口受到防火墙或其他此类设备的良好保护。

**你可以提一个可以在 SMB 和大型环境中使用的防火墙/UTM（OS 或应用程序）么？**

我使用 pfSense，它是 BSD 的衍生产品。我很喜欢它。它有很多模块，实际上现在它有商业支持，这对于小企业来说这是非常棒的。对于更大的设备、更大的环境，这取决于你有哪些管理员。

我一直都是 CheckPoint 管理员，但是 Palo Alto 也越来越受欢迎了。这些类型的安装与小型企业或家庭使用很不同。我在任何小型网络中都使用 pfSense。

**云服务有什么内在问题么？**

并没有云，只有其他人的电脑。云服务存在内在的问题。只知道谁访问了你的数据，你在上面放了什么。要知道当你向 Amazon 或 Google 或 Microsoft 上传某些东西时，你将不再完全控制它，并且该数据的隐私是有问题的。

**要获得 OSCP 你建议需要准备些什么？**

我现在准备通过这个认证。我的整个团队是这样。阅读他们的材料。要记住 OSCP 将成为令人反感的安全基准。你一切都要使用 Kali。如果不这样做 - 如果你决定不使用 Kali，请确保已安装所有工具来模拟 Kali 实例。

这将是一个基于工具的重要认证。这是一个很好的方法论。看看一些名为“渗透测试框架”的内容，因为这将为你提供一个很好的测试流程，他们的实验室似乎是很棒的。这与我家里的实验室非常相似。

_[随时免费观看完整的网络研讨会][3]。查看这个系列的[第一篇][4]和[第二篇][5]文章获得 5 个简单的贴士来让你的 Linux 机器安全。_

_Mike Guthrie 为能源部工作，负责 “Red Team” 的工作和渗透测试。_

--------------------------------------------------------------------------------

via: https://www.linux.com/news/webinar/2017/how-keep-hackers-out-your-linux-machine-part-3-your-questions-answered

作者：[MIKE GUTHRIE][a]
译者：[geekpi](https://github.com/geekpi)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]:https://www.linux.com/users/anch
[1]:https://www.linux.com/licenses/category/creative-commons-zero
[2]:https://www.linux.com/files/images/keep-hackers-outjpg
[3]:http://portal.on24.com/view/channel/index.html?showId=1101876&showCode=linux&partnerref=linco
[4]:https://www.linux.com/news/webinar/2017/how-keep-hackers-out-your-linux-machine-part-1-top-two-security-tips
[5]:https://www.linux.com/news/webinar/2017/how-keep-hackers-out-your-linux-machine-part-2-three-more-easy-security-tips
[6]:https://www.linux.com/news/webinar/2017/how-keep-hackers-out-your-linux-machine-part-1-top-two-security-tips
[7]:https://www.linux.com/news/webinar/2017/how-keep-hackers-out-your-linux-machine-part-2-three-more-easy-security-tips
[8]:http://portal.on24.com/view/channel/index.html?showId=1101876&showCode=linux&partnerref=linco