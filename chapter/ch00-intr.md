

# [导言](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)

## 英文介绍

[git history](https://www.welcometothejungle.com/en/articles/btc-history-git)

### In the beginning

Up until April 2005 Torvalds had managed the contributions of a large, disparate team of volunteer developers to  Linux Kernel—the increasingly popular open-source, UNIX-like operating  system—using [BitKeeper](http://www.bitkeeper.org/) (BK). This was a proprietary and paid-for tool at the time, but the  Linux development crew were allowed to use it for free… until BK founder Larry McVoy took issue with one of the Linux developers over  inappropriate use of BK.

From [Torvalds’s announcement](https://marc.info/?l=linux-kernel&m=111280216717070&w=2) to the Linux mailing list about his plan to take a working “vacation”  to decide what to do about finding a new VCS for Linux, it is clear that he liked BK, was frustrated that Linux could no longer use it, and that he was unimpressed by the competition. As mentioned, the outcome of  that vacation was Git. There are several theories why Torvalds called it Git, but the reason is actually just that he liked the word, which he’d learned from the Beatles song [I’m So Tired](https://genius.com/The-beatles-im-so-tired-lyrics) (verse two).

> *“The in-joke was that I name all my projects after myself, and this one was named ‘Git’. Git is [British slang](https://dictionary.cambridge.org/dictionary/english/git) for ‘stupid person’,”* Torvalds tells us. *“There’s a made-up acronym for it, too—Global Information Tracker—but that’s  really a ‘backronym’, [something] made up after the fact.”*

So, is Torvalds surprised by Git's monumental success? *“I’d be lying if I said I saw it coming. I absolutely didn’t. But Git really did get all the fundamentals right. Were there things that could have  been done better? Sure. But in the big picture, Git really finally  solved some of the really hard problems with VCS,”* he says.

### Defining Git's goals

Traditionally, version control was client server, so the code sits in a single  repository —or repo—on a central server. Concurrent Versions System  (CVS), [Subversion](https://en.wikipedia.org/wiki/Apache_Subversion) and Team Foundation Version Control (TFVC) are all examples of client-server systems.

A client-server VCS works fine in a corporate environment, where  development is tightly controlled and is undertaken by an in-house  development team with good network connections. It doesn't work so well  if you have a collaboration involving hundreds or thousands of  developers, working voluntarily, independently, and remotely, all eager  to try out new things with the code, which is all typical with open  source software (OSS) projects such as Linux.

Distributed VCS,  pioneered by BK, broke that mould. Git, Mercurial, and Monotone all  followed this example. With distributed VCS, a copy of the most current  version of the code resides on each developer's device, making it easier for developers to work independently on changes to the code. *“BK  was the big conceptual influence for the usage model, and really should  get all the credit. For various reasons, I wanted to make the Git  implementation and logic completely different from BK, but the  conceptual notion of ‘distributed VCS’ really was the number one goal,  and BK taught me the importance of that,”* says Torvalds. *“Being truly distributed means forks are non-issues, and anybody can fork a  project and do their own development, and then come back a month or a  year later and say, ‘Look at this great thing I’ve done.’”*

Another major drawback with client-server VCS, especially for open-source  projects, is whoever hosted the central repository on their server  "owned" the source code. With distributed VCS, however, there is no  central repository, just lots of clones, so nobody owns or controls the  code.

*“[This is what makes] sites like GitHub possible. When  there is no central ‘master’ location that contains the source code, you can suddenly host things without the politics that go along with that  ‘one repo to rule them all’ concept,”* says Torvalds.

Another  central goal was to reduce the pain of merging new branches into the  main source code or "tree" (the directory that makes up the source  code's hierarchy). Key to this is assigning a cryptographic hash—a  unique and secure number—to index every object. Using hashes wasn't  unique, but Git took it to a new level, not just applying them to every  new version of file contents, but also using them to identify how they  relate to each other, including trees and the commits. This meant that,  by using 'git diff', Git could very quickly identify all the changes  between new/proposed versions of branches and the source code, even  entire trees, by comparing the two indexes of hashes. *“The real  reason for the Git index is to act as that intermediate step for  merging, so that you can incrementally fix conflicts,”* says Torvalds.

This concept of the intermediate step or staging area to allow comparisons  of versions and fix any problems between the main source code and the  additions, before going ahead with the full merge, was revolutionary.  However, it was not universally appreciated by those used to other VCS.

### Appointing a maintainer

Having written Git, Torvalds threw it open to the open-source community for  review and contributions. Of those who stepped up, one developer in  particular shone through: Junio Hamano. So much so, that after only a  few months, Torvalds could take [a step back](https://marc.info/?l=git&m=112243466603239) and concentrate on Linux, passing over responsibility for maintaining Git to Hamano. *“He had that obvious and all-important but hard-to-describe ‘good taste’ when it came to code and features,”* says Torvalds. *“Junio really should get pretty much all the credit for Git—I started it, and  I’ll take credit for the design, but as a project, Junio is the person  who has maintained it and made it be such a pleasant tool to use.”*

Clearly he was a good choice because he is still leading/maintaining Git 15 years later, as a [benevolent dictator](http://oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel), which means he controls the direction of Git and has the final say on  changes to the code, and he holds the record for the most commits.

### Widening Git's appeal

Some of the volunteer contributors who supported Hamano in the early days  still contribute today, although they are often now employed to do it  full time by the companies that rely on Git and want to invest in its  upkeep and improvement.

One of these volunteers was Jeff King,  known as Peff, who started contributing when he was a student. His first commit was in 2006, having spotted and fixed a bug in [git-cvsimport](https://git-scm.com/docs/git-cvsimport), when moving his repositories from CVS to Git. *“I was a graduate student in computer science at the time,”* he says, *“so I spent a lot of time lurking on Git’s mailing list, answering  questions and fixing bugs—sometimes things that bothered me, sometimes  in response to other people’s reports. By around 2008, I had become one  of the main contributors, quite by accident.”* King has been employed by GitHub since 2011, both working on the website and contributing to Git itself.

King singles out the exemplary work of two fellow contributors to Git, who  both started in 2006 and helped to expand its influence beyond the Linux community: Shawn Pearce for his work on [JGit](https://gerrit.googlesource.com/jgit/), which opened up Git to the Java and Android ecosystem, and Johannes  Schindelin, for his work on Git for Windows, which opened up Git to the  Windows community. They subsequently went to work at Google and  Microsoft respectively.

*“[Shawn Pearce] was an early contributor to Git and implemented [git-gui](https://git-scm.com/docs/git-gui), the first graphical interface for Git. But more important is his work on JGit, a pure-Java implementation of Git,”* says King. *“This enabled a whole other ecosystem of Git users and allowed an Eclipse  plugin, which was a key part of the Android project selecting Git as  their version control system. He also wrote [Gerrit](https://www.gerritcodereview.com/) [when at Google], a code-review system based around Git that’s used for Android and many other projects. Sadly, [Shawn passed away in 2018](https://sfconservancy.org/blog/2018/jan/30/shawn-pearce/).”*

Schindelin remains the maintainer of the [Git for Windows distribution](https://gitforwindows.org/) today. *“Because of the way Git grew out of the kernel community, Windows support was mostly an afterthought,”* says King. *“Git has been ported to a lot of platforms, but most of them are vaguely  Unix-ish. Windows was by far the biggest challenge. There were not only  portability issues in the C code, but also the challenges of shipping an application with parts written in Bourne shell, Perl, and so on. Git  for Windows wrangles all of that complexity into a single binary  package, and has had a big impact on the growth of Git for Windows  developers.”*

According to [somsubhra.com](https://www.somsubhra.com/github-release-stats/?username=git-for-windows&repository=git), Git for Windows has been downloaded more than 18m times to date.  

### Sold

Despite this, the acquisition caused some concern among those GitHub  clients that remember the old Microsoft under the stewardship of the  open-source community's bête noire, Ballmer. Both Bitbucket and GitLab  claim to have seen a spike in projects moving from GitHub to their  platforms.

That concern is not shared by Torvalds, though. *“I  don’t have any reservations about the MS acquisition, partly because of  the whole fundamental distributed nature of Git—it avoids the political  issues, and it avoids the scary ‘hosting company controls the projects’  part. The other reason I’m not worried is I think MS is a different  company today… Microsoft and open source simply aren’t enemies,”*he says. *"On a purely personal level, when I heard that MS spent a lot of money on  GitHub, it just made me say, 'Now two of the projects I've started have  become billion-dollar industries.' Not a lot of people can say that. Nor am I just a 'one-hit wonder.''
“It is part of the ‘life well lived’  thing. It makes me happy that I have made a positive and meaningful  influence on the world. I may not have made any money personally from  Git directly, but it makes it possible for me to do my real job and  passion, [Linux]. And I am not a starving student anymore—I’m doing  quite well as a respected programmer. So other people being successful  with Git in no way upsets me.”*


## 中文简介

### 在一开始的时候

​       直到 2005 年 4 月，Torvalds 一直使用 BitKeeper (BK) 管理一个庞大的、不同的志愿者开发团队对  Linux Kernel（日益流行的开源、类 UNIX 操作系统）的贡献。当时这是一个专有的付费工具，但 Linux  开发人员被允许免费使用它……[直到 BK 创始人 Larry McVoy 就 BK 的不当使用向其中一位 Linux 开发人员提出异议](https://medium.com/@willhayjr/the-architecture-and-history-of-git-a-distributed-version-control-system-62b17dd37742)。(注：此为澳大利亚计算机程序员 Andrew Tridgell([Samba](https://en.wikipedia.org/wiki/Samba_(software)) [file server](https://en.wikipedia.org/wiki/File_server)的作者) 对 BitKeeper 的源代码进行了逆向工程并违反了其许可证)

​       从  Torvalds 向 Linux [邮件](https://lwn.net/Articles/130681/)列表发布关于他计划休假来决定如何为 Linux 寻找新的 VCS 的公告，很明显他喜欢 BK，对  Linux 无法再使用它感到沮丧，并且他对比赛不感兴趣。如前所述，那个假期的结果是 Git。Torvalds 将其称为 Git  的原因有多种说法，但实际上只是因为他喜欢这个词，这是他从甲壳虫乐队的歌曲“我太累了”（第二节）中学到的。

> “开玩笑的是，我所有的项目都以我自己的名字命名，而这个项目被命名为‘Git’。Git 是英国俚语，意思是“愚蠢的人”，托瓦兹告诉我们。 “它也有一个编造的首字母缩略词——全球信息追踪器——但这确实是一个‘缩略词’，[东西]事后编造的。”

​        那么，Torvalds 是否对 Git 的巨大成功感到惊讶？ “如果我说我看到它来了，那我就是在撒谎。我绝对没有。但是 Git  确实掌握了所有的基础知识。有没有可以做得更好的事情？当然。但从大局来看，Git 最终确实解决了 VCS 的一些非常棘手的问题，”他说。

### 定义 Git 的目标

​         传统上，版本控制是客户端服务器，因此代码位于中央服务器上的单个存储库或存储库中。并发版本系统 (CVS)、Subversion 和 Team Foundation 版本控制 (TFVC) 都是客户端 - 服务器系统的示例。

​         客户端 - 服务器 VCS  在公司环境中运行良好，在该环境中开发受到严格控制并由具有良好网络连接的内部开发团队进行。如果您的协作涉及成百上千的开发人员，他们自愿、独立和远程工作，都渴望用代码尝试新事物，这在开源软件 (OSS) 项目中都是典型的。例如 Linux。

​        由 BK 开创的分布式 VCS 打破了这种模式。Git、Mercurial 和  Monotone 都遵循了这个例子。使用分布式 VCS，最新版本的代码副本驻留在每个开发人员的设备上，使开发人员可以更轻松地独立处理代码更改。  “BK 对使用模型的概念影响很大，真的应该得到所有的赞誉。出于各种原因，我想让 Git 实现和逻辑与 BK 完全不同，但“分布式  VCS”的概念确实是首要目标，而 BK 教会了我这一点的重要性，”Torvalds 说。  “真正的分布式意味着分叉不是问题，任何人都可以分叉一个项目并进行自己的开发，然后一个月或一年后回来说，‘看看我所做的这件伟大的事情。”

​        ”客户端 - 服务器 VCS 的另一个主要缺点，尤其是对于开源项目，是在其服务器上托管中央存储库的人“拥有”源代码。然而，对于分布式 VCS，没有中央存储库，只有大量克隆，因此没有人拥有或控制代码。

​       “[这就是使] GitHub 之类的网站成为可能的原因。当没有包含源代码的中央‘主’位置时，您可以突然托管一些没有政治的东西，这些东西与‘一个回购统治所有’的概念相一致，”托瓦兹说。

​        另一个中心目标是减少将新分支合并到主源代码或“树”（构成源代码层次结构的目录）的痛苦。其关键是分配一个加密散列——一个唯一且安全的数字——来索引每个对象。使用哈希并不是唯一的，但 Git  将其提升到一个新的水平，不仅将它们应用于文件内容的每个新版本，而且还使用它们来确定它们之间的关系，包括树和提交。这意味着，通过使用“git  diff”，Git 可以通过比较哈希的两个索引，非常快速地识别分支的新/提议版本与源代码之间的所有更改，甚至是整个树。 “Git  索引的真正原因是作为合并的中间步骤，以便您可以逐步修复冲突，”Torvalds 说。

​       在进行完全合并之前，允许比较版本并修复主要源代码和添加之间的任何问题的中间步骤或暂存区域的概念是革命性的。然而，习惯了其他 VCS 的人并没有普遍欣赏它。

### 任命维护者

​       编写 Git 后，Torvalds 将其公开给开源社区以供审查和贡献。在那些挺身而出的人中，一位特别出色的开发人员：Junio  Hamano。如此之多，以至于仅仅几个月后，Torvalds 就可以退后一步，专注于 Linux，将维护 Git 的责任移交给 Hamano。Torvalds 说：“在代码和功能方面，他有着明显而重要但难以描述的‘好品味’。” “Junio 真的应该为 Git  赢得几乎所有的荣誉——我开始了它，我将把设计归功于我，但作为一个项目，Junio 是维护它的人，并使它成为一个如此令人愉快的工具使用。”

​        显然他是一个不错的选择，因为 15 年后他仍然在领导/维护 Git，作为一个仁慈的独裁者，这意味着他控制着 Git 的方向，对代码的更改拥有最终决定权，并且他保持着最多的记录提交。

### 扩大 Git 的吸引力

​        一些早期支持 Hamano 的志愿者贡献者今天仍在贡献，尽管他们现在经常被依赖 Git 并希望投资于其维护和改进的公司全职工作。其中一位志愿者是杰夫·金（Jeff King），他被称为 Peff，他在学生时代就开始做出贡献。他的第一次提交是在 2006 年，当时他发现并修复了 git-cvsimport  中的一个错误，当时他将他的存储库从 CVS 移到了 Git。 “当时我是计算机科学专业的研究生，”他说，“所以我花了很多时间潜伏在 Git  的邮件列表上，回答问题和修复错误——有时是困扰我的事情，有时是为了回应其他人的报告。到 2008  年左右，我成为主要贡献者之一，这完全是偶然的。”自 2011 年以来，King 一直受雇于 GitHub，既在网站上工作，又为 Git  本身做出贡献。

​       King 列举了两位 Git 贡献者的模范工作，他们都始于 2006 年，并帮助将其影响力扩大到 Linux 社区之外：Shawn Pearce 为他在 JGit 上的工作，为 Java 和 Android 生态系统打开了 Git，以及 Johannes  Schindelin，因为他在 Windows 版 Git 上的工作，这使 Git 向 Windows  社区开放。随后，他们分别去了谷歌和微软工作。

​        “[Shawn Pearce] 是 Git 的早期贡献者，并实现了 git-gui，这是 Git  的第一个图形界面。但更重要的是他在 JGit 方面的工作，JGit 是 Git 的纯 Java 实现，”King 说。 “这启用了一个完整的  Git 用户生态系统，并允许使用 Eclipse 插件，这是选择 Git 作为其版本控制系统的 Android 项目的关键部分。他还编写了  Gerrit [在谷歌时]，这是一个基于 Git 的代码审查系统，用于 Android 和许多其他项目。可悲的是，肖恩于 2018 年去世了。

​       ”今天，Schindelin 仍然是 Git for Windows 发行版的维护者。 “由于 Git 从内核社区发展而来的方式，Windows  支持大多是事后才想到的，”King 说。 “Git 已经被移植到很多平台上，但其中大部分都是模糊的 Unix-ish。Windows  是迄今为止最大的挑战。不仅存在 C 代码中的可移植性问题，而且使用用 Bourne shell、Perl 等编写的部分传送应用程序也存在挑战。Windows 版 Git 将所有这些复杂性整合到一个二进制包中，并对 Windows 开发人员的 Git 增长产生了重大影响。”

​       据 somsubhra.com 称，迄今为止，Windows 版 Git 的下载量已超过 1800 万次

### 收购

​          尽管如此，微软的收购还是引起了那些 GitHub 客户的一些担忧，这些客户还记得在开源社区的黑名单鲍尔默的管理下的旧微软。Bitbucket 和 GitLab 都声称已经看到从 GitHub 转移到他们的平台的项目激增。

​        不过，Torvalds 并不认同这种担忧。 “我对 MS 的收购没有任何保留，部分原因是 Git  的整个基本分布式性质——它避免了政治问题，并且避免了可怕的‘托管公司控制项目’的部分。我不担心的另一个原因是我认为今天的 MS  是一家不同的公司……微软和开源根本不是敌人，”他说。 “纯粹就个人而言，当我听说 MS 在 GitHub  上花了很多钱时，我只想说，'现在我开始的两个项目已经成为十亿美元的产业。' 不是很多人能做到比如说。我也不仅仅是一个“一击必杀的奇迹”。

>​       “这是‘过得好生活’的一部分。我对世界产生了积极而有意义的影响，这让我很高兴。我个人可能没有直接从 Git  赚到钱，但它让我有可能做我真正的工作和热情，[Linux]。我不再是一个挨饿的学生——作为一个受人尊敬的程序员，我做得很好。所以其他人在 Git 上取得成功绝不会让我感到不安。”

[git help book](https://git-scm.com/book/en/v2)