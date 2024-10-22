# 区块链 技术简介


 [1. 什么是区块链？ - 区块链简介、相关术语](#h10)

 [2. 区块链是如何操作的？ - 动手实验，实例演示区块链的功能](#h20)

 [3. 专家讲堂 - 深入探讨区块链的各个模组](#h30)

 [4. 技能培训 - 由浅入深，区块链系列免费课程](#h40)

 [5. 问与答 - 区块链常见问题解答](#h50)


## <a name="h10">1. 什么是区块链？ - 区块链简介、相关术语 
### 区块链 技术术语
<div>
<table border="1px" bordercolor="#000000" cellspacing="0px" >
                <tr>
                    <th width="15%">英文</th>
                    <th width="15%">中文</th>
                    <th>解释</th>
                </tr>
                <tr>
                    <td><b>Anchor Peer </b></td>
                    <td><b>锚节点</b></td>
                    <td>所有其他peer可以发现并与之通信的channel上的一个peer。channel上的每个Member都有一个（或者对个，以防止单点故障）Anchor Peer，允许属于不同Member的peer发现channel上的现有其他peer。</td>
                </tr>
                <tr>
                    <td><b>Block </b></td>
                    <td><b>区块</b></td>
                    <td>在一个channel上与前一个block加密连接的一组有序交易集。</td>
                </tr>
                <tr>
                    <td><b>Chain </b></td>
                    <td><b>链</b></td>
                    <td>chain就是block之间以hash连接为结构的交易日志。peer从order service接收交易block，并根据背书策略和并发冲突标记block上的交易是否有效，然后将该block追加到peer文件系统中的hash chain上。</td>
                </tr>
                <tr>
                    <td><b>Chaincode </b></td>
                    <td><b>链码</b></td>
                    <td>Chaincode是一个运行在ledger上的软件，对资产和交易指令（业务逻辑）编码来修改资产。</td>
                </tr>
                <tr>
                    <td><b>Channel </b></td>
                    <td><b>通道</b></td>
                    <td>channel是在Fabric网络中的私有区块链区域，实现了数据的隔离和保密。channel特定的ledger在该channel上的所有 peer之间共享，交易方必须有对该channel正确的认证才能与该ledger交互。channel由Configuration Block定义。</td>
                </tr>
                <tr>
                    <td><b>Commitment </b></td>
                    <td><b>提交</b></td>
                    <td>一个channel中的每个peer都会验证交易的有序block，然后将block提交（写或追加）至该channel上ledger的各个副本。peer还会标记每个block中的每个交易是否有效。</td>
                </tr>
                <tr>
                    <td><b>Concurrency Control Version Check </b></td>
                    <td><b>CCVC</b></td>
                    <td>CCVC是一种channel中各peer间保持状态同步的方法。peer并行执行交易，在提交至ledger之前会检查在执行期间读到的数据有没 有被修改。如果读取的数据在执行和提交之间被改变，就会引发CCVC冲突，该交易就会被标记为无效，值不会更新到状态数据库中。</td>
                </tr>
                <tr>
                    <td><b>Configuration Block </b></td>
                    <td><b>配置区块</b></td>
                    <td>包含 system chain (ordering service) 或 channel 的Member和策略配置数据。对某个channel或整个网络的任何修改（比如，Member离开或加入）都将导致一个新的Configuration Block追加到适当的chain中。这个Configuration Block会包含 genesis block的内容加上增量。</td>
                </tr>
                <tr>
                    <td><b>Consensus </b></td>
                    <td><b>共识</b></td>
                    <td>Consensus是贯穿整个交易流程的广义术语，其用于产生对于order的共识和确认构成block的所有交易的正确性。</td>
                </tr>
                <tr>
                    <td><b>Current State </b></td>
                    <td><b>当前状态</b></td>
                    <td>ledger的current state表示其chain交易log中所有key的最新值。peer会将处理过的block中的每个交易对应的修改value提交到ledger的 current state，由于current state表示channel所知的所有最新的k-v，所以current state也被称为World State。Chaincode执行交易proposal就是针对的current state。</td>
                </tr>
                <tr>
                    <td><b>Dynamic Membership </b></td>
                    <td><b>动态成员</b></td>
                    <td>Fabric支持动态添加/移除members、peers和ordering服务节点，而不会影响整个网络的操作性。当业务关系调整或因各种原因需添加/移除实体时，Dynamic Membership至关重要。</td>
                </tr>
                <tr>
                    <td><b>Endorsement </b></td>
                    <td><b>背书</b></td>
                    <td>Endorsement 是指一个peer执行一个交易并返回YES/NO给生成交易proposal的client app 的过程。chaincode具有相应的endorsement policies，其中指定了endorsing peer。</td>
                </tr>
                <tr>
                    <td><b>Endorsement policy </b></td>
                    <td><b>背书策略</b></td>
                    <td>Endorsement policy定义了依赖于特定chaincode执行交易的channel上的peer和响应结果（endorsements）的必要组合条件（即返回 Yes或No的条件）。Endorsement policy可指定对于某一chaincode，可以对交易背书的最小背书节点数或者最小背书节点百分比。背书策略由背书节点基于应用程序和对抵御不良行 为的期望水平来组织管理。在install Chaincode（deploy tx）时需要指定背书策略。</td>
                </tr>
                <tr>
                    <td><b>Genesis Block </b></td>
                    <td><b>初始区块</b></td>
                    <td>Genesis Block是初始化区块链网络或channel的配置区块，也是链上的第一个区块。</td>
                </tr>
                <tr>
                    <td><b>Gossip Protocol </b></td>
                    <td><b>Gossip协议</b></td>
                    <td>Gossip数据传输协议有三项功能：1）管理peer发现和channel成员；2）channel上的所有peer间广播账本数据；3）channel上的所有peer间同步账本数据。</td>
                </tr>
                <tr>
                    <td><b>Initialize </b></td>
                    <td><b>初始化</b></td>
                    <td>一个初始化chaincode程序的方法。</td>
                </tr>
                <tr>
                    <td><b>Install </b></td>
                    <td><b>安装</b></td>
                    <td>将chaincode放到peer的文件系统的过程。（译注：即将ChaincodeDeploymentSpec信息存到chaincodeInstallPath/chaincodeName.chainVersion文件中）</td>
                </tr>
                <tr>
                    <td><b>Instantiate </b></td>
                    <td><b>实例化</b></td>
                    <td>启动chaincode容器的过程。（译注：在lccc中将ChaincodeData保存到state中，然后deploy Chaincode并执行Init方法）</td>
                </tr>
                <tr>
                    <td><b>Invoke </b></td>
                    <td><b>调用</b></td>
                    <td>用于调用chaincode内的函数。Chaincode invoke就是一个交易proposal，然后执行模块化的流程（背书、共识、 验证、 提交）。invoke的结构就是一个函数和一个参数数组。</td>
                </tr>
                <tr>
                    <td><b>Leading Peer </b></td>
                    <td><b>主导节点</b></td>
                    <td>每一个Member在其订阅的channel上可以拥有多个peer，其中一个peer会作为channel的leading peer代表该Member与ordering service通信。ordering service将block传递给leading peer，该peer再将此block分发给同一member下的其他peer。</td>
                </tr>
                <tr>
                    <td><b>Ledger </b></td>
                    <td><b>账本</b></td>
                    <td>Ledger是个channel的chain和由channel中每个peer维护的world state。（这个解释有点怪）</td>
                </tr>
                <tr>
                    <td><b>Member </b></td>
                    <td><b>成员</b></td>
                    <td>拥有网络唯一根证书的合法独立实体。像peer节点和app client这样的网络组件会链接到一个Member。</td>
                </tr>
                <tr>
                    <td><b>Membership Service Provider </b></td>
                    <td><b>MSP</b></td>
                    <td>MSP是指为client和peer提供证书的系统抽象组件。Client用证书来认证他们的交易；peer用证书认证其交易背书。该接口与系统的交易处理组件密切相关，旨在使已定义的成员身份服务组件以这种方式顺利插入而不会修改系统的交易处理组件的核心。</td>
                </tr>
                <tr>
                    <td><b>Membership Services </b></td>
                    <td><b>成员服务</b></td>
                    <td>成员服务在许可的区块链网络上认证、授权和管理身份。在peer和order中运行的成员服务的代码都会认证和授权区块链操作。它是基于PKI的MSP实现。fabric-ca组件实现了成员服务，来管理身份。特别的，它处理ECert和TCert的颁发和撤销。ECert是长期的身份凭证；TCert是短期的身份凭证，是匿名和不可链接的。</td>
                </tr>
                <tr>
                    <td><b>Ordering Service </b></td>
                    <td><b>排序服务或共识服务</b></td>
                    <td>将交易排序放入block的节点的集合。ordering service独立于peer流程之外，并以先到先得的方式为网络上所有的channel作交易排序。ordering service支持可插拔实现，目前默认实现了SOLO和Kafka。ordering service是整个网络的公用binding，包含与每个Member相关的加密材料。</td>
                </tr>
                <tr>
                    <td><b>Peer </b></td>
                    <td><b>节点</b></td>
                    <td>一个网络实体，维护ledger并运行Chaincode容器来对ledger执行read/write操作。peer由Member拥有和维护。</td>
                </tr>
                <tr>
                    <td><b>Policy </b></td>
                    <td><b>策略</b></td>
                    <td>有背书策略，校验策略，区块提交策略，Chaincode管理策略和网络/通道管理策略。</td>
                </tr>
                <tr>
                    <td><b>Proposal </b></td>
                    <td><b>提案</b></td>
                    <td>一种针对channel中某peer的背书请求。每个proposal要么是Chaincode instantiate要么是Chaincode invoke。</td>
                </tr>
                <tr>
                    <td><b>Query </b></td>
                    <td><b>查询</b></td>
                    <td>对于current state中某个key的value的查询请求。</td>
                </tr>
                <tr>
                    <td><b>Software Development Kit </b></td>
                    <td><b>SDK</b></td>
                    <td>SDK为开发人员提供了一个结构化的库环境，用于编写和测试链码应用程序。SDK完全可以通过标准接口实现配置和扩展，像签名的加密算法、日志框架 和state存储这样的组件都可以轻松地实现替换。SDK API使用gRPC进行交易处理，成员服务、节点遍历以及事件处理都是据此与fabric通信。目前SDK支持Node.js、Java和Python。</td>
                </tr>
                <tr>
                    <td><b>State Database </b></td>
                    <td><b>stateDB</b></td>
                    <td>为了从Chaincode中高效的读写，Current state 数据存储在stateDB中，包括levelDB和couchDB。</td>
                </tr>
                <tr>
                    <td><b>System Chain </b></td>
                    <td><b>系统链</b></td>
                    <td>包含在系统级定义网络的配置区块。系统链存在于ordering service中，与channel类似，具有包含以下信息的初始配置：MSP信息、策略和信息配置。对整个网络的任何变化（例如新的Org加入或者添加 新的Ordering节点）将导致新的配置区块被添加到系统链。系统链可看做是一个channel或一组channel的公用binding。例如，金融机构的集合可以形成一个财团（以system chain表示），然后根据其相同或不同的业务创建channel。</td>
                </tr>
                <tr>
                    <td><b>Transaction </b></td>
                    <td><b>交易</b></td>
                    <td>Chaincode的invoke或instantiate操作。Invoke是从ledger中请求read/write set；Instantiate是请求在peer上启动Chaincode容器。</td>
                </tr>
    </table>
</div>

## <a name="h20">2. 区块链是如何操作的？ - 动手实验，实例演示区块链的功能 

<div> <table border="1px" bordercolor="#000000" cellspacing="0px" >
<tr>
<td style="width: 5%;"><strong><span style="font-size:10px;">No</span></strong></td>
<td style="width: 55;"><strong><span style="font-size:10px;">内容概要</span></strong></td>
<td style="width: 20%;"><strong><span style="font-size:10px;">视频回放及讲义</span></strong></td>
<td style="width: 20%;"><strong><span style="font-size:10px;">练习及答案</span></strong></td>
</tr>

<tr>
<td>01</td>
<td><b>区块链－开启全新商业模式.</b>
最初区块链这种技术是随着数字货币被热炒而被逐渐关注，之后人们也开始探讨区块链在金融、制造业、物联网、保险等各个领域的应用场景。那么，区块链的核心价值是什么？区块链这项“黑科技”如何在产业中得以运用？IBM对于区块链的商用之道有什么看法?
</td>
<td>
<a href="http://ibm.biz/hyperledger01" target="_blank">区块链商用之道</a>
<br>
<a href="try-on-Bluemix/区块链第一讲.pdf"> 区块链第一讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1135778/87b7" target="_blank">课后练习</a>
<br>12345, 13, 235
</td>
</tr>

<tr>
<td>02</td>
<td><b>HyperLedger－Linux基金会下的开源区块链项目.</b>
超级账本 （HyperLedger）区块链联盟是Linux基金会于2015年发起的推进区块链数字技术和交易验证的开源项目联盟，成员包括以IBM为代表的技术 厂商以及各大型银行、航空等100多家公司，其中有超过1/4的成员都来自中国，是世界上最流行的开源区块链解决方案之一。最初区块链这种技术是随着数字货币被热炒而被逐渐关注，之后人们也开始探讨区块链在金融、制造业、物联网、保险等各个领域的应用场景。那么，区块链的核心价值是什么？区块链这项“黑科技”如何在产业中得以运用？IBM对于区块链的商用之道有什么看法？
</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjYyMTU0MzEwMA==.html" target="_blank">HyperLedger项目与社区概览</a>
<br>
<a href="try-on-Bluemix/区块链第二讲.pdf"> 区块链第二讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1135778/87b7" target="_blank">课后练习</a>
<br>13, 24, 2
</td>
</tr>

<tr>
<td>03</td>
<td><b>HyperLedger Fabric －区块链的基石.</b>
介绍HyperLedger Fabric架构从0.6到1.0的演进，包括：总体架构、运行时架构，特点等等，讲解HyperLedger Fabric的安装过程，最后演示IBM Bluemix上的区块链服务。
</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjY1MTAxNjY0NA==.html" target="_blank">HyperLedger Fabric架构解读(上)</a>
<br>
<a href="http://v.youku.com/v_show/id_XMjY1MTIzODk0NA==.html" target="_blank">HyperLedger Fabric架构解读(下)</a>
<br>
<a href="try-on-Bluemix/区块链第三讲.pdf"> 区块链第三讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1188794/d618" target="_blank">课后练习</a>
<br>3333, 4444, 1
</td>
</tr>

<tr>
<td>04</td>
<td><b>ChainCode －智能合约的代码实现.</b>
详细介绍Fabric0.6中Chaincode运行的基本原理以及开发调试步骤，简单介绍目前Fabric1.0中关于Chaincode开发的基本内容，并对比0.6介绍相关变化。
</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjY2Njg2NDM0OA==.html" target="_blank">ChainCode实战</a>
<br>
<a href="try-on-Bluemix/区块链第四讲.pdf"> 区块链第四讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1212449/7ae7" target="_blank">课后练习</a>
<br>2除外, 12, 1
</td>
</tr>

<tr>
<td>05</td>
<td><b>Ledger －不可篡改伪造的“共享帐本”.</b>
主要介绍Fabric v1.0中共享账本的实现原理与机制，同时也会指出v1.0相比v0.6增加的新功能和使用方法的变化。</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjY3OTE1NTA2OA==.html" target="_blank">HyperLedger Fabric中的共享账本</a>
<br>
<a href="try-on-Bluemix/区块链第五讲.pdf"> 区块链第五讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1227477/ded6" target="_blank">课后练习</a>
<br>123, 1, 3
</td>
</tr>

<tr>
<td>06</td>
<td><b>共识机制 －多节点达成一致的算法.</b>
区块链上的共识机制主要解决由谁来构造区块，以及如何维护区块链统一的问题。共识机制，是驱动区块链运转的发动机，决定着区块链项目的性能和结构。主要介绍HyperLedger共识机制，包括Hyperledger记账方式，共识参与方和共识算法。</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjY5MzI0MTM3Mg==.html" target="_blank">HyperLedger Fabric中的共识机制</a>
<br>
<a href="try-on-Bluemix/区块链第六讲.pdf"> 区块链第六讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1266480/9e4c" target="_blank">课后练习</a>
<br>23, 123, 23
</td>
</tr>

<tr>
<td>07</td>
<td><b>隐私与安全 －区块链商用的关键.</b>
如何保障交易数据的不可更改／如何保障交易的私密性／如何保障交易的可监管能力／如何保护交易隐私</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjcwNzY1ODgyNA==.html" target="_blank">HyperLedger Fabric中的隐私与安全</a>
<br>
<a href="try-on-Bluemix/区块链第七讲.pdf"> 区块链第七讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1272847/7f82">课后练习</a>
<br>·3, 1, 4
</td>
</tr>

<tr>
<td>08</td>
<td><b>HyperLedger应用案例赏析.</b>
介绍HyperLedger的几个典型的应用案例，包括场景、架构、优势等等。</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjcyMDc0MzQzNg==.html" target="_blank">HyperLedger Fabric应用案例赏析</a>
<br>
<a href="try-on-Bluemix/区块链第八讲.pdf"> 区块链第八讲.pdf</a>
</td>
<td >
<a href="https://wj.qq.com/s/1310989/bad7">课后练习</a>
</td>
</tr>

<tr>
<td>09</td>
<td><b>Hyperledger Fabric SDK解析.</b>
主要介绍fabric SDK的设计思想和基本功能，以及如何使用fabric SDK，在使用sdk进行开发时应该考虑的一些问题。</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjczMzQ3ODg2MA==.html" target="_blank">Fabric实战补充：Hyperledger Fabric SDK解析</a>
<br>
<a href="try-on-Bluemix/区块链第九讲.pdf"> 区块链第九讲.pdf</a>
</td>
<td>
</td>
</tr>

<tr>
<td>10</td>
<td><b>Hyperledger Fabric 研究心得.</b>
开发者分享：1.研究心得2.Node SDK 是要怎么看啊！3.Golang Chaincode的新玩儿</td>
<td>
<a href="http://v.youku.com/v_show/id_XMjc1NTIyODk0MA==.html" target="_blank">Hyperledger Fabric 研究心得</a>
<br>
<a href="try-on-Bluemix/区块链第十讲.pdf"> 区块链第十讲.pdf</a>
</td>
<td>
</td>
</tr>

</table>
</div>


## <a name="h40">4. 技能培训 - 由浅入深，区块链系列免费课程 

* [区块链技术基础：分布式账本简介](https://www.ibm.com/developerworks/cn/cloud/library/cl-blockchain-basics-intro-bluemix-trs/)
* [IBM Blockchain 101：开发人员快速入门指南](http://www.ibm.com/developerworks/cn/cloud/library/cl-ibm-blockchain-101-quick-start-guide-for-developers-bluemix-trs/index.html)
* [使用 Go 编写智能合约](https://www.ibm.com/developerworks/cn/cloud/library/cl-ibm-blockchain-chaincode-development-using-golang/index.html)
* [IBM Blockchain for developers(英文)](https://developer.ibm.com/courses/all-courses/blockchain-for-developers)


## <a name="h50">5. 问与答 - 区块链常见问题解答

* 能通俗的解释一下什么是区块链吗？

>答：通俗一点说，区块链技术就指一种全民参与记账的方式。所有的系统背后都有一个数据库，你可以把数据库看成是就是一个大账本。那么谁来记这个账本就变得很重要。目前就是谁的系统谁来记账，微信的账本就是腾讯在记，淘宝的账本就是阿里在记。但现在区块链系统中，系统中的每个人都可以有机会参与记账。在一定时间段内如果有任何数据变化，系统中每个人都可以来进行记账，系统会评判这段时间内记账最快最好的人，把他记录的内容写到账本，并将这段时间内账本内容发给系统内所有的其他人进行备份。这样系统中的每个人都了一本完整的账本。这种方式，我们就称它为区块链技术

* 区块链解决了什么问题吗？

>答：区块链最重要的是解决了中介信用问题。在过去，两个互不认识和信任的人要达成协作是难的，必须要依靠第三方。比如支付行为，在过去任何一种转账，必须要有银行或者支付宝这样的机构存在。但是通过区块链技术，比特币是人类第一次实现在没有任何中介机构参与的情况下，完成双方可以互信的转账行为。这是区块链的重大突破。

* 区块链是比特币吗？或者比特币就是区块链吗？

>答：区块链技术是比特币的底层技术，在早期并没有太多人注意到比特币的底层技术。但是当比特币在没有任何中心化机构运营和管理的情况下，在多年里非常稳定的运行，并且没有出现过任何问题。所以很多人注意到，该底层技术技术也许有很大的机制，而且不仅仅可以在比特币中使用，也许可以在许多领域都能够应用这种技术。于是把比特币技术抽象提取出来，称之为区块链技术，或者分布式账本技术。所以从某个角度来看，比特币可以看成是区块链第一个应用，而区块链更类似于TCP/IP这样的底层技术，以后会扩展到越来越多的行业中。

* 什么是公有链？什么是私有链？什么是联盟链？

>公有链是任何节点都是向任何人开放的，每个人都可以参与到这个区块链中参与计算，而且任何人都可以下载获得完整区块链数据（全部账本）。但是有些区块链的应用场景下，并不希望这个系统任何人都可以参与，任何人都可以查看所有数据，只有被许可的节点才可以参与并且查看所有数据。那么这种区块链结构我们称为私有链。

>联盟链是指参与每个节点的权限都完全对等，大家在不需要完全互信的情况下就可以实现数据的可信交换，R3组成的银行区块链联盟要构建的就是典型的联盟链。

>但是随着区块链技术的快速发展，不排除以后公有链和私有链的界限会变得比较模糊。因为每个节点的可以有较为复杂的读写权限，也许有部分权限的节点会向所有人开发，而部分记账或者核心权限的节点只能向许可的节点开放，那就会不再是纯粹的公有链或者私有链。

* 区块链 和业务应用是什么关系 ？


* 区块链 目前有几种版本? 各运行在哪些运行平台上？

* 对于支持编写 Chaincode, 有哪几种 SDK ？ 

* Chaincode 支持哪些语言的编写，如何发布 ？

* 使用Bluemix平台上的区块链, 有什么好处 ?

* What is Blockchain?
>Blockchain is a shared, replicated ledger that underpins technology such as Bitcoin. Blockchain's reach is wider than cryptocurrency however, as it sets out to provide the foundation for a new generation of transactional applications that establish trust and transparency, while streamlining business processes.

 
* What is IBM doing about Blockchain?
>IBM is offering code, intellectual property and development resource to the Linux Foundation Hyperledger project. This includes a contribution of 44,000 lines of IBM blockchain code, which will help developers explore the use of blockchain in the enterprise as they build secure distributed ledgers.
>Blockchain services are available on IBM BlueMix to help developers create private and secure digital assets and transaction instructions. Internet of Things (IoT) data is enabled on blockchain, such as RFID-based location data, barcode-scan event data or device-reported data which can be used with the blockchain fabric.

>It is also helping clients and IBMers understand and adopt blockchain through a dedicated engagement team and a set of IBM garages for blockchain application design and implementation in London, New York, Singapore and Tokyo.

 
* How do I enable my clients for Blockchain?

>The engagement team's goal is to help IMTs get up to speed on Blockchain so that they feel comfortable with enabling clients, i.e. leading clients through the initial conversation and demonstration, a hands-on proof of technology and through to first (paid) project. Specifically, the process can be summarised as follows.

>1. IBM account lead or IMT lead learns the "Blockchain Explained" deck and demo (see links below).
>2. **Conversation:** IBM account lead or IMT lead delivers "Blockchain Explained" conversation and demonstration. The enablement team can provide remote assistance for any outstanding questions. (During the conversation, it's good practice to offer a hands-on proof of technology. If the customer is interested in this, please let the enablement team know and supply a salesconnect number.)
>3. IBM account lead or IMT lead learns the Proof of Technology material (see links below). The enablement team can provide remote assistance for any outstanding questions.
>4. **Blockchain Hands-On:**  IBM account lead works with IMT lead to deliver Proof of Technology. This is a one day hands-on lab with the morning suitable for business and technical people, and getting more technical as the day goes on.
>5. IBM account lead contacts the Blockchain Engagement team to help identify delivery team for a first (paid) project. The blockchain deal board will help ensure that the correct resources are in place to support the project.
>6. **First Project:**  The project delivery team delivers first project. This starts with a two day design thinking workshop and planning iteration followed by a number of follow-on agile iterations.
>7. IBM account lead works with client to identify initial deployment.

>The engagement team is running regular IMT workshops to help the process of IBM enablement, but can also be done on request.

>Don't be tempted to short-cut the Conversation > Hands-on > First project engagement model! Importantly, it's designed to progressively qualify an opportunity so you don't waste time and effort early on. And always start with IBM's point of view; if a customer has prior experience of blockchain this can put them at a disadvantage as they can sometimes make assumptions about blockchain that is different from IBM's (business-oriented) opinion. If the customer really does know blockchain then great - you can go through the steps more quickly.

>More details on the engagement process can be found in "Blockchain Engaged for IBMers" presentation on Box: <https://ibm.box.com/v/BlockEng>. Start by reading this, educating yourself and if necessary, contact your *local expert*.

 
* What is the difference between Bitcoin, Blockchain, Hyperledger, Open Blockchain and IBM Blockchain?

>**Bitcoin** is an unregulated, censorship resistant cryptocurrency. It uses a blockchain in order to track transfers, and was the first mainstream blockchain application. IBM is not interested in cryptocurrency use-cases.

>**Blockchain** is a shared, replicated ledger that can record asset transfers. The term 'blockchain fabric' is often used to describe the platform that user applications connect to in order to interact with such a ledger, as well as the ledger itself. Examples of blockchain fabrics include Bitcoin, Ethereum, Open Blockchain and Hyperledger.

>**Hyperledger** is the name of the Linux Foundation project to produce an open blockchain platform that is ready for business. It will provide an implementation of the shared ledger, smart contracts, privacy and consensus mechanisms. It will not provide any value added services (like monitoring or cloud hosting). IBM is one of many sponsors of the Hyperledger project.

>**Hyperledger Fabric:** One of two incubator projects being run by the Linux Foundation to test out blockchain capabilities, and consists of contributions by IBM, DAH and others. The other incubator project is called Sawtooth Lake and is sponsored by Intel.

>**Open Blockchain** (OBC) was the name of the open source project started by IBM in 2015 to explore the development of a blockchain which supports specific business attributes including; permissions, privacy, confidentiality and auditability. It is written in Go. It implemented a pluggable design (consensus, storage, key management) and a flexible way to write business logic (chaincode). IBM has incorporated much of this code into Hyperledger Fabric.

>**IBM Blockchain** is the (current) name of IBM's blockchain offering suite. Today this consists of the IBM Blockchain DevOps Service on Bluemix, which is a beta service and free of charge. The service is currently based on Hyperledger Fabric. IBM also has a limited availability blockchain service on LinuxOne.

 
* Where can I go for more information?

>The community website <http://ibm.biz/BlockchainGang> is the one place for all IBMer enablement of Blockchain. The customer website is <http://www.ibm.com/blockchain>.

>The Blockchain Explained deck is one of the most important (and well used) presentations for telling everyone about Blockchain and IBM's point of view: <https://ibm.box.com/BlockExp>. More details can be found on the Blockchain Customer Engagement page of this wiki. The box share that contains all presentations is here: <https://ibm.box.com/BlockchainBox>.

>For technical FAQs please go to <http://ibm.biz/BlockTechFAQ>

>The blockchain engagement team can be reached over email at [WW Blockchain/UK/IBM](mailto: WW Blockchain/UK/IBM).

 
* Where do I go for more education?

>External, DeveloperWorks Online Blockchain Training
>Aimed at education developers but starts of at a high level and drills down over 6 hours

>- [Blockchain For Developers] (https://developer.ibm.com/courses/all-courses/blockchain-for-developers/)

>IBM Internal, Online Blockchain Training
With new material before going to External site & IBM Confidential Material

>- [Blockchain 101] (https://developer.ibm.com/courses/all-courses/blockchain-for-developers/)

