


# 1. Introduction
Effective communication depends on the use of a common language. This is true for humans and other animals as well as for computers. When a set of common behaviors is used with a common language, a protocol is being used. The first definition of a protocol, according to the New Oxford American Dictionary, is 

高效率的交流依赖于使用相同的语言，这是存在于人们包括动物，电脑的共同真理。当使用共同的语言规定了共同的行为，协议的概念就在这里被使用了。根据《New Oxford American Dictionary》，**protocol**是这样第一次被定义的。

**The official procedure or system of rules governing affairs of state or diplomatic occasions.**

**管理国家或外交场合事务的官方程序或规则体系。**

We engage in many protocols every day: asking and responding to questions, negotiating business transactions, working collaboratively, and so on. 

我们每天都参与许多协议：询问和回答问题，协商业务交易，协同工作等等。

Computers also engage in a variety of protocols. 

计算机还参与各种协议。

A collection of related protocols is called a engage in many protocols every day: asking and responding to questions, negotiating business transactions, working collaboratively, and so on. Computers also engage in a variety of protocols. A collection of related protocols is called a protocol suite. The design that specifies how various protocols of a protocol suite relate to each other and divide up tasks to be accomplished is called the architecture or reference model for the protocol suite.

相关协议的集合称为协议套件。指定协议套件的各种协议如何相互关联以及将要完成的任务划分的设计称为协议套件的体系结构或参考模型。 

TCP/IP is a protocol suite that implements the Internet architecture and draws its origins from the ARPANET Reference Model (ARM) [RFC0871]. The ARM was itself influenced by early work on packet switching in the United States by Paul Baran [B64] and Leonard Kleinrock [K64], in the U.K. by Donald Davies [DBSW66], and in France by Louis Pouzin [P73]. Other protocol architectures have been specified over the years (e.g., the ISO protocol architecture [Z80], Xerox’s XNS [X85], and IBM’s SNA [I96]), but TCP/IP has become the most popular. There are several interesting books that focus on the history of computer communications and the development of the Internet, such as [P07] and [W02].

TCP / IP是一种实现Internet体系结构的协议套件，其起源于ARPANET参考模型（ARM）[RFC0871]。ARM本身受到Paul Baran [B64]和Leonard Kleinrock [K64]，英国Donald Davies [DBSW66]和法国Louis Pouzin [P73]早期分组交换工作的影响。多年来已经指定了其他协议架构（例如，ISO协议架构[Z80]，Xerox的XNS [X85]和IBM的SNA [I96]），但TCP / IP已经成为最受欢迎的。有几本有趣的书籍专注于计算机通信的历史和互联网的发展，如[P07]和[W02]。

It is worth mentioning that the TCP/IP architecture evolved from work that addressed a need to provide interconnection of multiple different packet-switched computer networks [CK74]. This was accomplished using a set of gateways (later called routers) that provided a translation function between each otherwise incompatible network. The resulting “concatenated” network or catenet (later called internetwork) would be much more useful, as many more nodes offering a wide variety of services could communicate. The types of uses that a global network might offer were envisioned years before the protocol architecture was fully developed. In 1968, for example, J. C. R. Licklider and Bob Taylor foresaw the potential uses for a global interconnected communication network to support “supercommunities” [LT68]:

值得一提的是，TCP / IP架构是从满足多个不同分组交换计算机网络互连需求的工作演变而来的[CK74]。这是使用一组网关（后来称为路由器）完成的，这些网关在每个不兼容的网络之间提供转换功能。由此产生的“连接”网络或网络（后来称为互联网络）将更加有用，因为提供各种服务的更多节点可以进行通信。在协议架构完全开发之前几年，设想了全球网络可能提供的用途类型。例如，1968年，JCR Licklider和Bob Taylor预见到全球互联通信网络的潜在用途，以支持“超级社区”[LT68]：

Today the on-line communities are separated from one another functionally as well as geographically. Each member can look only to the processing, storage and software capability of the facility upon which his community is centered. But now the move is on to interconnect the separate communities and thereby transform them into, let us call it, a supercommunity. The hope is that interconnection will make available to all members of all the communities the programs and data resources of the entire supercommunity . . . The whole will constitute a labile network of networks—ever-changing in both content and configuration.

今天，在线社区在功能和地理上彼此分离。每个成员只能查看其社区所在的设施的处理，存储和软件功能。但现在正在采取措施将各个社区互连起来，从而将它们转变为超级社区，我们称之为超级社区。希望互连将为所有社区的所有成员提供整个超级社区的程序和数据资源。。。整体将构成一个不稳定的网络网络 - 内容和配置都在不断变化。

Thus, it is apparent that the global network concept underpinning the ARPANET and later the Internet was designed to support many of the types of uses we enjoy today. However, getting to this point was neither simple nor obvious. The success resulted from paying careful attention to design and engineering, innovative users and developers, and the availability of sufficient resources to move from concept to prototype and, eventually, to commercial networking products.

因此，很明显支持ARPANET和后来互联网的全球网络概念旨在支持我们今天享受的许多类型的用途。然而，达到这一点既不简单也不明显。成功的关键在于对设计和工程，创新用户和开发人员的密切关注，以及从概念到原型以及最终转向商业网络产品的足够资源的可用性。

This chapter provides an overview of the Internet architecture and TCP/IP protocol suite, to provide some historical context and to establish an adequate background for the remaining chapters. Architectures (both protocol and physical) really amount to a set of design decisions about what features should be supported and where such features should be logically implemented. Designing an architecture is more art than science, yet we shall discuss some characteristics of architectures that have been deemed desirable over time. The subject of network architecture has been undertaken more broadly in the text by Day [D08], one of few such treatments.

本章概述了Internet体系结构和TCP / IP协议套件，以提供一些历史背景并为其余章节建立适当的背景知识。架构（协议和物理）实际上相当于一组关于应该支持哪些功能的设计决策以及应该在逻辑上实现这些功能的位置。设计一个架构更多的是艺术而不是科学，但我们将讨论一段时间内被认为合乎需要的架构特征。网络架构的主题已经在Day [D08]的文本中进行了更广泛的讨论，这是少数此类处理之一。

## 1.1. ARCHITECTURAL PRINCIPLES
The TCP/IP protocol suite allows computers, smartphones, and embedded devices of all sizes, supplied from many different computer vendors and running totally different software, to communicate with each other. By the turn of the twenty-first century it has become a necessity for modern communication, entertainment, and commerce. It is truly an open system in that the definition of the protocol suite and many of its implementations are publicly available at little or no charge. It forms the basis for what is called the global Internet, or the Internet, a wide area network (WAN) of about two billion users that literally spans the globe (as of 2010, about 30% of the world’s population). Although many people consider the Internet and the World Wide Web (WWW) to be interchangeable terms, we ordinarily refer to the Internet in terms of its ability to provide basic communication of messages between computers. We refer to WWW as an application that uses the Internet for communication. It is perhaps the most important Internet application that brought Internet technology to world attention in the early 1990s.

TCP / IP协议套件允许从许多不同计算机供应商提供并运行完全不同的软件的各种规模的计算机，智能手机和嵌入式设备相互通信。到二十一世纪之交，它已成为现代通信，娱乐和商业的必需品。它是一个真正的开放系统，因为协议套件的定义及其许多实现都是公开的，很少或免费。它构成了所谓的全球互联网或互联网的基础，互联网是一个大约20亿用户的广域网（WAN），其覆盖全球（截至2010年，约占全球人口的30％）。虽然很多人认为互联网和万维网（WWW）是可互换的术语，我们通常是指在互联网上提供计算机之间消息基本通信的能力。我们将WWW称为使用Internet进行通信的应用程序。它可能是最重要的互联网应用程序，在20世纪90年代初将互联网技术引入世界关注。

Several goals guided the creation of the Internet architecture. In [C88], Clark recounts that the primary goal was to “develop an effective technique for multiplexed utilization of existing interconnected networks.” The essence of this statement is that the Internet architecture should be able to interconnect multiple distinct networks and that multiple activities should be able to run simultaneously on the resulting interconnected network. Beyond this primary goal, Clark provides a list of the following second-level goals:

几个目标指导了互联网架构的创建。在[C88]中，Clark回顾说，主要目标是“开发一种有效利用现有互连网络的有效技术。”这一陈述的实质是互联网架构应该能够互连多个不同的网络，并且多个活动应该能够在最终的互连网络上同时运行。除了这个主要目标，Clark提供了以下二级目标的列表：

• Internet communication must continue despite loss of networks or gateways.

• The Internet must support multiple types of communication services.

• The Internet architecture must accommodate a variety of networks.

• The Internet architecture must permit distributed management of its resources.

• The Internet architecture must be cost-effective.

• The Internet architecture must permit host attachment with a low level of effort.

• The resources used in the Internet architecture must be accountable.

• 尽管网络或网关丢失，仍必须继续进行Internet通信。

• Internet必须支持多种类型的通信服务。

• Internet体系结构必须适应各种网络。

• Internet体系结构必须允许对其资源进行分布式管理。

• 互联网架构必须具有成本效益。

•Internet体系结构必须以较低的工作量允许主机连接。

•Internet体系结构中使用的资源必须是负责任的。

Many of the goals listed could have been supported with somewhat different design decisions from those ultimately selected. However, a few design options were gaining momentum when these architectural principles were being formulated that influenced the designers in the particular choices they made. We will mention some of the more important ones and their consequences.

列出的许多目标都可以通过最终选择的设计决策得到支持。然而，当制定这些架构原则时，一些设计方案正在获得动力，这些原则在设计师的特定选择中受到影响。我们将提到一些更重要的及其后果。

### 1.1.1. Packets, Connections, and Datagrams
Up to the 1960s, the concept of a network was based largely on the telephone network. It was developed to connect telephones to each other for the duration of a call. A call was normally implemented by establishing a connection from one party to another. Establishing a connection meant that a circuit (initially, a physical electrical circuit) was made between one telephone and another for the duration of a call. When the call was complete, the connection was cleared, allowing the circuit to be used by other users’ calls. The call duration and identification of the connection endpoints were used to perform billing of the users. When established, the connection provided each user a certain amount of bandwidth or capacity to send information (usually voice sounds). The telephone network progressed from its analog roots to digital, which greatly improved its reliability and performance. Data inserted into one end of a circuit follows some preestablished path through the network switches and emerges on the other side in a predictable fashion, usually with some upper bound on the time (latency). This gives predictable service, as long as a circuit is available when a user needs one. Circuits allocate a pathway through the network that is reserved for the duration of a call, even if they are not entirely busy. This is a common experience today with the phone network—as long as a call is taking place, even if we are not saying anything, we are being charged for the time.

直到20世纪60年代，网络的概念主要基于电话网络。它被开发用于在通话期间将电话彼此连接。通常通过建立从一方到另一方的连接来实现呼叫。建立连接意味着在呼叫期间在一部电话和另一部电话之间建立电路（最初是物理电路）。呼叫完成后，连接被清除，允许其他用户的呼叫使用该电路。呼叫持续时间和连接端点的标识用于执行用户的计费。建立后，连接为每个用户提供一定量的带宽或容量来发送信息（通常是语音）。电话网络从模拟根源发展到数字化，这大大提高了其可靠性和性能。插入到电路一端的数据遵循通过网络交换机的一些预先建立的路径，并以可预测的方式出现在另一侧，通常在时间上有一些上限（延迟）。只要当用户需要电路时，这就可以提供可预测的服务。电路分配通过网络的路径，该路径在呼叫期间保留，即使它们并非完全忙碌。这是今天电话网络的常见体验 - 只要正在进行通话，即使我们没有说什么，我们也会收取时间费用。通常在时间上有一些上限（延迟）。只要当用户需要电路时，这就可以提供可预测的服务。电路分配通过网络的路径，该路径在呼叫期间保留，即使它们并非完全忙碌。这是今天电话网络的常见体验 - 只要正在进行通话，即使我们没有说什么，我们也会收取时间费用。通常在时间上有一些上限（延迟）。只要当用户需要电路时，这就可以提供可预测的服务。电路分配通过网络的路径，该路径在呼叫期间保留，即使它们并非完全忙碌。这是今天电话网络的常见体验 - 只要正在进行通话，即使我们没有说什么，我们也会收取时间费用。

One of the important concepts developed in the 1960s (e.g., in [B64]) was the idea of packet switching. In packet switching, “chunks” (packets) of digital information comprising some number of bytes are carried through the network somewhat independently. Chunks coming from different sources or senders can be mixed together and pulled apart later, which is called multiplexing. The chunks can be moved around from one switch to another on their way to a destination, and the path might be subject to change. This has two potential advantages: the network can be more resilient (the designers were worried about the network being physically attacked), and there can be better utilization of the network links and switches because of statistical multiplexing.

在20世纪60年代开发的一个重要概念（例如，在[B64]中）是分组交换的想法。在分组交换中，包括一定数量字节的数字信息的“组块”（分组）在某种程度上独立地通过网络传送。来自不同来源或发送者的块可以混合在一起并在以后拆开，这称为多路复用。在到达目的地的路上，块可以从一个交换机移动到另一个交换机，并且路径可能会发生变化。这有两个潜在的优势：网络可以更具弹性（设计人员担心网络受到物理攻击），并且由于统计复用，可以更好地利用网络链路和交换机。

When packets are received at a packet switch, they are ordinarily stored in buffer memory or queue and processed in a first-come-first-served (FCFS) fashion. This is the simplest method for scheduling the way packets are processed and is also called first-in-first-out (FIFO). FIFO buffer management and on-demand scheduling are easily combined to implement statistical multiplexing, which is the primary method used to intermix traffic from different sources on the Internet. In statistical multiplexing, traffic is mixed together based on the arrival statistics or timing pattern of the traffic. Such multiplexing is simple and efficient, because if there is any network capacity to be used and traffic to use it, the network will be busy (high utilization) at every bottleneck or choke point. The downside of this approach is limited predictability—the performance seen by any particular application depends on the statistics of other applications that are sharing the network. Statistical multiplexing is like a highway where the cars can change lanes and ultimately intersperse in such a way that any point of constriction is as busy as it can be.

当在分组交换机处接收分组时，它们通常存储在缓冲存储器或队列中并以先来先服务（FCFS）方式处理。这是调度数据包处理方式的最简单方法，也称为先进先出（FIFO）。FIFO缓冲区管理和按需调度很容易组合起来实现统计复用，这是用于混合来自Internet上不同源的流量的主要方法。在统计复用中，基于到达统计或业务的定时模式将业务混合在一起。这种多路复用简单而有效，因为如果要使用任何网络容量和使用它的流量，网络将在每个瓶颈或阻塞点忙碌（高利用率）。这种方法的缺点是可预测性有限 - 任何特定应用程序看到的性能取决于共享网络的其他应用程序的统计信息。统计多路复用就像一条高速公路，汽车可以改变车道，最终以任何收缩点尽可能繁忙的方式散布。

Alternative techniques, such as time-division multiplexing (TDM) and static multiplexing, typically reserve a certain amount of time or other resources for data on each connection. Although such techniques can lead to more predictability, a feature useful for supporting constant bit rate telephone calls, they may not fully utilize the network capacity because reserved bandwidth may go unused. Note that while circuits are straightforwardly implemented using TDM techniques, virtual circuits (VCs) that exhibit many of the behaviors of circuits but do not depend on physical circuit switches can be implemented atop connection-oriented packets. This is the basis for a protocol known as X.25 that was popular until about the early 1990s when it was largely replaced with Frame Relay and ultimately digital subscriber line (DSL) technology and cable modems supporting Internet connectivity (see Chapter 3).

诸如时分复用（TDM）和静态复用之类的替代技术通常为每个连接上的数据保留一定量的时间或其他资源。尽管这些技术可以带来更多的可预测性，这是一种对支持恒定比特率电话呼叫有用的功能，但它们可能无法充分利用网络容量，因为预留带宽可能未被使用。注意，虽然使用TDM技术直接实现电路，但是可以在面向连接的分组上实现表现出电路的许多行为但不依赖于物理电路交换的虚拟电路（VC）。这是称为X的协议的基础。

The VC abstraction and connection-oriented packet networks such as X.25 required some information or state to be stored in each switch for each connection. The reason is that each packet carries only a small bit of overhead information that provides an index into a state table. For example, in X.25 the 12-bit logical channel identifier (LCI) or logical channel number (LCN) serves this purpose. At each switch, the LCI or LCN is used in conjunction with the per-flow state in each switch to determine the next switch along the path for the packet. The per-flow state is established prior to the exchange of data on a VC using a signaling protocol that supports connection establishment, clearing, and status information. Such networks are consequently called connection-oriented.

VC抽象和面向连接的分组网络（例如X.25）需要为每个连接存储在每个交换机中的一些信息或状态。原因是每个数据包只携带一小部分开销信息，这些信息为状态表提供索引。例如，在X.25中，12位逻辑信道标识符（LCI）或逻辑信道号（LCN）用于此目的。在每个交换机处，LCI或LCN与每个交换机中的每个流状态一起使用，以确定沿着该分组的路径的下一个交换机。在使用支持连接建立，清除和状态信息的信令协议在VC上交换数据之前建立每流状态。因此，这种网络被称为面向连接。

Connection-oriented networks, whether built on circuits or packets, were the most prevalent form of networking for many years. In the late 1960s, another option was developed known as the datagram. Attributed in origin to the CYCLADES [P73] system, a datagram is a special type of packet in which all the identifying information of the source and final destination resides inside the packet itself (instead of in the packet switches). Although this tends to require larger packets, per-connection state at packet switches is no longer required and a connectionless network could be built, eliminating the need for a (complicated) signaling protocol. Datagrams were eagerly embraced by the designers of the early Internet, and this decision had profound implications for the rest of the protocol suite.

面向连接的网络，无论是基于电路还是数据包，都是多年来最普遍的网络形式。在20世纪60年代后期，另一种选择被称为数据报。归因于CYCLADES [P73]系统，数据报是一种特殊类型的数据包，其中源和最终目的地的所有识别信息都驻留在数据包本身内（而不是在数据包交换机中）。虽然这往往需要更大的数据包，但不再需要分组交换机的每个连接状态，并且可以构建无连接网络，从而无需（复杂的）信令协议。数据报受到早期互联网设计者的热烈欢迎，这一决定对协议套件的其余部分产生了深远的影响。

One other related concept is that of message boundaries or record markers. As shown in Figure 1-1, when an application sends more than one chunk of information into the network, the fact that more than one chunk was written may or may not be preserved by the communication protocol. Most datagram protocols preserve message boundaries. This is natural because the datagram itself has a beginning and an end. However, in a circuit or VC network, it is possible that an application may write several chunks of data, all of which are read together as one or more different-size chunks by a receiving application. These types of protocols do not preserve message boundaries. In cases where an underlying protocol fails to preserve message boundaries but they are needed by an application, the application must provide its own.

另一个相关概念是消息边界或记录标记。如图1-1所示，当应用程序向网络发送多个信息块时，通信协议可能会或可能不会保留写入多个块的事实。大多数数据报协议保留消息边界。这很自然，因为数据报本身有一个开头和一个结尾。然而，在电路或VC网络中，应用程序可能会写入几个数据块，所有这些数据块都由接收应用程序一起读取为一个或多个不同大小的块。这些类型的协议不保留消息边界。如果底层协议无法保留消息边界但应用程序需要它们，则应用程序必须提供自己的协议。

> Figure 1-1. Applications write messages that are carried in protocols. A message boundary is the position or byte offset between one write and another. Protocols that preserve message boundaries indicate the position of the sender’s message boundaries at the receiver. Protocols that do not preserve message boundaries (e.g., streaming protocols like TCP) ignore this information and do not make it available to a receiver. As a result, applications may need to implement their own methods to indicate a sender’s message boundaries if this capability is required.

> 图1-1。应用程序编写协议中携带的消息。消息边界是一次写入与另一次写入之间的位置或字节偏移。保留消息边界的协议指示发送方的消息边界在接收方的位置。不保留消息边界的协议（例如，像TCP这样的流协议）会忽略此信息，并且不会使其可用于接收方。因此，如果需要此功能，应用程序可能需要实现自己的方法来指示发送方的消息边界。

Image

![](https://learning.oreilly.com/library/view/tcpip-illustrated-volume/9780132808200/graphics/01fig01.jpg)

### 1.1.2. The End-to-End Argument and Fate Sharing
When large systems such as an operating system or protocol suite are being designed, a question often arises as to where a particular feature or function should be placed. One of the most important principles that influenced the design of the TCP/IP suite is called the end-to-end argument [SRC84]:

The function in question can completely and correctly be implemented only with the knowledge and help of the application standing at the end points of the communication system. Therefore, providing that questioned function as a feature of the communication itself is not possible. (Sometimes an incomplete version of the function provided by the communication system may be useful as a performance enhancement.)

This argument may seem fairly straightforward upon first reading but can have profound implications for communication system design. It argues that correctness and completeness can be achieved only by involving the application or ultimate user of the communication system. Efforts to correctly implement what the application is “likely” to need are doomed to incompleteness. In short, this principle argues that important functions (e.g., error control, encryption, delivery acknowledgment) should usually not be implemented at low levels (or layers; see Section 1.2.1) of large systems. However, low levels may provide capabilities that make the job of the endpoints somewhat easier and consequently may improve performance. A nuanced reading reveals that this argument suggests that low-level functions should not aim for perfection because a perfect guess at what the application may require is unlikely to be possible.

The end-to-end argument tends to support a design with a “dumb” network and “smart” systems connected to the network. This is what we see in the TCP/IP design, where many functions (e.g., methods to ensure that data is not lost, controlling the rate at which a sender sends) are implemented in the end hosts where the applications reside. The selection of which functions are implemented together in the same computer or network or software stack is the subject of another related principle known as fate sharing [C88].

Fate sharing suggests placing all the necessary state to maintain an active communication association (e.g., virtual connection) at the same location with the communicating endpoints. With this reasoning, the only type of failure that destroys communication is one that also destroys one or more of the endpoints, which obviously destroys the overall communication anyhow. Fate sharing is one of the design philosophies that allows virtual connections (e.g., those implemented by TCP) to remain active even if connectivity within the network has failed for a (modest) period of time. Fate sharing also supports a “dumb network with smart end hosts” model, and one of the ongoing tensions in today’s Internet is what functions reside in the network and what functions do not.

### 1.1.3. Error Control and Flow Control
There are some circumstances where data within a network gets damaged or lost. This can be for a variety of reasons such as hardware problems, radiation that modifies bits while being transmitted, being out of range in a wireless network, and other factors. Dealing with such errors is called error control, and it can be implemented in the systems constituting the network infrastructure, or in the systems that attach to the network, or some combination. Naturally, the end-to-end argument and fate sharing would suggest that error control be implemented close to or within applications.

Usually, if a small number of bit errors are of concern, a number of mathematical codes can be used to detect and repair the bit errors when data is received or while it is in transit [LC04]. This task is routinely performed within the network. When more severe damage occurs in a packet network, entire packets are usually resent or retransmitted. In circuit-switched or VC-switched networks such as X.25, retransmission tends to be done inside the network. This may work well for applications that require strict in-order, error-free delivery of their data, but some applications do not require this capability and do not wish to pay the costs (such as connection establishment and potential retransmission delays) to have their data reliably delivered. Even a reliable file transfer application does not really care in what order the chunks of file data are delivered, provided it is eventually satisfied that all chunks are delivered without errors and can be reassembled back into the original order.

As an alternative to the overhead of reliable, in-order delivery implemented within the network, a different type of service called best-effort delivery was adopted by Frame Relay and the Internet Protocol. With best-effort delivery, the network does not expend much effort to ensure that data is delivered without errors or gaps. Certain types of errors are usually detected using error-detecting codes or checksums, such as those that might affect where a datagram is directed, but when such errors are detected, the errant datagram is merely discarded without further action.

If best-effort delivery is successful, a fast sender can produce information at a rate that exceeds the receiver’s ability to consume it. In best-effort IP networks, slowing down a sender is achieved by flow control mechanisms that operate outside the network and at higher levels of the communication system. In particular, TCP handles this type of problem, and we shall discuss it in detail in Chapters 15 and 16. This is consistent with the end-to-end argument: TCP, which resides at the end hosts, handles rate control. It is also consistent with fate sharing: the approach allows some elements of the network infrastructure to fail without necessarily affecting the ability of the devices outside the network to communicate (as long as some communication path continues to operate).

## 1.2. DESIGN AND IMPLEMENTATION
Although a protocol architecture may suggest a certain approach to implementation, it usually does not include a mandate. Consequently, we make a distinction between the protocol architecture and the implementation architecture, which defines how the concepts in a protocol architecture may be rendered into existence, usually in the form of software.

Many of the individuals responsible for implementing the protocols for the ARPANET were familiar with the software structuring of operating systems, and an influential paper describing the “THE” multiprogramming system [D68] advocated the use of a hierarchical structure as a way to deal with verification of the logical soundness and correctness of a large software implementation. Ultimately, this contributed to a design philosophy for networking protocols involving multiple layers of implementation (and design). This approach is now called layering and is the usual approach to implementing protocol suites.

### 1.2.1. Layering
With layering, each layer is responsible for a different facet of the communications. Layers are beneficial because a layered design allows developers to evolve different portions of the system separately, often by different people with somewhat different areas of expertise. The most frequently mentioned concept of protocol layering is based on a standard called the Open Systems Interconnection (OSI) model [Z80] as defined by the International Organization for Standardization (ISO). Figure 1-2 shows the standard OSI layers, including their names, numbers, and a few examples. The Internet’s layering model is somewhat simpler, as we shall see in Section 1.3.

Figure 1-2. The standard seven-layer OSI model as specified by the ISO. Not all protocols are implemented by every networked device (at least in theory). The OSI terminology and layer numbers are widely used.

Image

![](https://learning.oreilly.com/library/view/tcpip-illustrated-volume/9780132808200/graphics/01fig02.jpg)

Although the OSI model suggests that seven logical layers may be desirable for modularity of a protocol architecture implementation, the TCP/IP architecture is normally considered to consist of five. There was much debate about the relative benefits and deficiencies of the OSI model, and the ARPANET model that preceded it, during the early 1970s. Although it may be fair to say that TCP/IP ultimately “won,” a number of ideas and even entire protocols from the ISO protocol suite (protocols standardized by ISO that follow the OSI model) have been adopted for use with TCP/IP (e.g., IS-IS [RFC3787]).

As described briefly in Figure 1-2, each layer has a different responsibility. From the bottom up, the physical layer defines methods for moving digital information across a communication medium such as a phone line or fiber-optic cable. Portions of the Ethernet and Wireless LAN (Wi-Fi) standards are here, although we do not delve into this layer very much in this text. The link or data-link layer includes those protocols and methods for establishing connectivity to a neighbor sharing the same medium. Some link-layer networks (e.g., DSL) connect only two neighbors. When more than one neighbor can access the same shared network, the network is said to be a multi-access network. Wi-Fi and Ethernet are examples of such multi-access link-layer networks, and specific protocols are used to mediate which stations have access to the shared medium at any given time. We discuss these in Chapter 3.

Moving up the layer stack, the network or internetwork layer is of great interest to us. For packet networks such as TCP/IP, it provides an interoperable packet format that can use different types of link-layer networks for connectivity. The layer also includes an addressing scheme for hosts and routing algorithms that choose where packets go when sent from one machine to another. Above layer 3 we find protocols that are (at least in theory) implemented only by end hosts, including the transport layer. Also of great interest to us, it provides a flow of data between sessions and can be quite complex, depending on the types of services it provides (e.g., reliable delivery on a packet network that might drop data). Sessions represent ongoing interactions between applications (e.g., when “cookies” are used with a Web browser during a Web login session), and session-layer protocols may provide capabilities such as connection initiation and restart, plus checkpointing (saving work that has been accomplished so far). Above the session layer we find the presentation layer, which is responsible for format conversions and standard encodings for information. As we shall see, the Internet protocols do not include a formal session or presentation protocol layer, so these functions are implemented by applications if needed.

The top layer is the application layer. Applications usually implement their own application-layer protocols, and these are the ones most visible to users. There is a wide variety of application-layer protocols, and programmers are constantly inventing new ones. Consequently, the application layer is where there is the greatest amount of innovation and where new capabilities are developed and deployed.

### 1.2.2. Multiplexing, Demultiplexing, and Encapsulation in Layered Implementations
One of the major benefits of a layered architecture is its natural ability to perform protocol multiplexing. This form of multiplexing allows multiple different protocols to coexist on the same infrastructure. It also allows multiple instantiations of the same protocol object (e.g., connections) to be used simultaneously without being confused.

Multiplexing can occur at different layers, and at each layer a different sort of identifier is used for determining which protocol or stream of information belongs together. For example, at the link layer, most link technologies (such as Ethernet and Wi-Fi) include a protocol identifier field value in each packet to indicate which protocol is being carried in the link-layer frame (IP is one such protocol). When an object (packet, message, etc.), called a protocol data unit (PDU), at one layer is carried by a lower layer, it is said to be encapsulated (as opaque data) by the next layer down. Thus, multiple objects at layer N can be multiplexed together using encapsulation in layer N - 1. Figure 1-3 shows how this works. The identifier at layer N - 1 is used to determine the correct receiving protocol or program at layer N during demultiplexing.

>  Figure 1-3. Encapsulation is usually used in conjunction with layering. Pure encapsulation involves taking the PDU of one layer and treating it as opaque (uninterpreted) data at the layer below. Encapsulation takes place at each sender, and decapsulation (the reverse operation) takes place at each receiver. Most protocols use headers during encapsulation; a few also use trailers.

Image

![](https://learning.oreilly.com/library/view/tcpip-illustrated-volume/9780132808200/graphics/01fig03.jpg)

In Figure 1-3, each layer has its own concept of a message object (a PDU) corresponding to the particular layer responsible for creating it. For example, if a layer 4 (transport) protocol produces a packet, it would properly be called a layer 4 PDU or transport PDU (TPDU). When a layer is provided a PDU from the layer above it, it usually “promises” to not look into the contents of the PDU. This is the essence of encapsulation—each layer treats the data from above as opaque, uninterpretable information. Most commonly a layer prepends the PDU with its own header, although trailers are used by some protocols (not TCP/IP). The header is used for multiplexing data when sending, and for the receiver to perform demultiplexing, based on a demultiplexing (demux) identifier. In TCP/IP networks such identifiers are commonly hardware addresses, IP addresses, and port numbers. The header may also include important state information, such as whether a virtual circuit is being set up or has already completed setup. The resulting object is another PDU.

One other important feature of layering suggested by Figure 1-2 is that in pure layering not all networked devices need to implement all the layers. Figure 1-4 shows that in some cases a device needs to implement only a few layers if it is expected to perform only certain types of processing.

Figure 1-4. Different network devices implement different subsets of the protocol stack. End hosts tend to implement all the layers. Routers implement layers below the transport layer, and switches implement link-layer protocols and below. This idealized structure is often violated because routers and switches usually include the ability to act as a host (e.g., to be managed and set up) and therefore need an implementation of all of the layers even if they are rarely used.

Image
In Figure 1-4, a somewhat idealized small internet includes two end systems, a switch, and a router. In this figure, each number corresponds to a type of protocol at a particular layer. As we can see, each device implements a different subset of the layer stack. The host on the left implements three different link-layer protocols (D, E, and F) with corresponding physical layers and three different transport-layer protocols (A, B, and C) that run on a single type of network-layer protocol. End hosts implement all the layers, switches implement up to layer 2 (this switch implements D and G), and routers implement up to layer 3. Routers are capable of interconnecting different types of link-layer networks and must implement the link-layer protocols for each of the network types they interconnect.

The internet of Figure 1-4 is somewhat idealized because today’s switches and routers often implement more than the protocols they are absolutely required to implement for forwarding data. This is for a number of reasons, including management. In such circumstances, devices such as routers and switches must sometimes act as hosts and support services such as remote login. To do this, they usually must implement transport and application protocols.

Although we show only two hosts communicating, the link- and physical-layer networks (labeled as D and G) might have multiple hosts attached. If so, then communication is possible between any pair of systems that implement the appropriate higher-layer protocols. In Figure 1-4 we can differentiate between an end system (the two hosts on either side) and an intermediate system (the router in the middle) for a particular protocol suite. Layers above the network layer use end-to-end protocols. In our picture these layers are needed only on the end systems. The network layer, however, provides a hop-by-hop protocol and is used on the two end systems and every intermediate system. The switch or bridge is not ordinarily considered an intermediate system because it is not addressed using the internetworking protocol’s addressing format, and it operates in a fashion that is largely transparent to the network-layer protocol. From the point of view of the routers and end systems, the switch or bridge is essentially invisible.

A router, by definition, has two or more network interfaces (because it connects two or more networks). Any system with multiple interfaces is called multihomed. A host can also be multihomed, but unless it specifically forwards packets from one interface to another, it is not called a router. Also, routers need not be special hardware boxes that only move packets around an internet. Most TCP/IP implementations, for example, allow a multihomed host to act as a router also, if properly configured to do so. In this case we can call the system either a host (when an application such as File Transfer Protocol (FTP) [RFC0959] or the Web is used) or a router (when it is forwarding packets from one network to another). We will use whichever term makes sense given the context.

One of the goals of an internet is to hide all of the details of the physical layout (the topology) and lower-layer protocol heterogeneity from the applications. Although this is not obvious from our two-network internet in Figure 1-4, the application layers should not care (and do not care) that even though each host is attached to a network using link-layer protocol D (e.g., Ethernet), the hosts are separated by a router and switch that use link-layer G. There could be 20 routers between the hosts, with additional types of physical interconnections, and the applications would run without modification (although the performance might be somewhat different). Abstracting the details in this way is what makes the concept of an internet so powerful and useful.

## 1.3. THE ARCHITECTURE AND PROTOCOLS OF THE TCP/IP SUITE
So far we have discussed architecture, protocols, protocol suites, and implementation techniques in the abstract. In this section, we discuss the architecture and particular protocols that constitute the TCP/IP suite. Although this has become the established term for the protocols used on the Internet, there are many protocols beyond TCP and IP in the collection or family of protocols used with the Internet. We begin by noting how the ARPANET reference model of layering, which ultimately formed the basis for the Internet’s protocol layering, differs somewhat from the OSI layering discussed earlier.

### 1.3.1. The ARPANET Reference Model
Figure 1-5 depicts the layering inspired by the ARPANET reference model, which was ultimately adopted by the TCP/IP suite. The structure is simpler than the OSI model, but real implementations include a few specialized protocols that do not fit cleanly into the conventional layers.

Figure 1-5. Protocol layering based on the ARM or TCP/IP suite used in the Internet. There are no official session or presentation layers. In addition, there are several “adjunct” or helper protocols that do not fit well into the standard layers yet perform critical functions for the operation of the other protocols. Some of these protocols are not used with IPv6 (e.g., IGMP and ARP).

Image
Starting from the bottom of Figure 1-5 and working our way up the stack, the first layer we see is 2.5, an “unofficial” layer. There are several protocols that operate here, but one of the oldest and most important is called the Address Resolution Protocol (ARP). It is a specialized protocol used with IPv4 and only with multi-access link-layer protocols (such as Ethernet and Wi-Fi) to convert between the addresses used by the IP layer and the addresses used by the link layer. We examine this protocol in Chapter 4. In IPv6 the address-mapping function is part of ICMPv6, which we discuss in Chapter 8.

At layer number 3 in Figure 1-5 we find IP, the main network-layer protocol for the TCP/IP suite. We discuss it in detail in Chapter 5. The PDU that IP sends to link-layer protocols is called an IP datagram and may be as large as 64KB (and up to 4GB for IPv6). In many cases we shall use the simpler term packet to mean an IP datagram when the usage context is clear. Fitting large packets into link-layer PDUs (called frames) that may be smaller is handled by a function called fragmentation that may be performed by IP hosts and some routers when necessary. In fragmentation, portions of a larger datagram are sent in multiple smaller datagrams called fragments and put back together (called reassembly) when reaching the destination. We discuss fragmentation in Chapters 5 and 10.

Throughout the text we shall use the term IP to refer to both IP versions 4 and 6. We use the term IPv6 to refer to IP version 6, and IPv4 to refer to IP version 4, currently the most popular version. When discussing architecture, the details of IPv4 versus IPv6 matter little. When we delve into the way particular addressing and configuration functions work (Chapter 2 and Chapter 6), for example, these details will become more important.

Because IP packets are datagrams, each one contains the address of the layer 3 sender and recipient. These addresses are called IP addresses and are 32 bits long for IPv4 and 128 bits long for IPv6; we discuss them in detail in Chapter 2. This difference in IP address size is the characteristic that most differentiates IPv4 from IPv6. The destination address of each datagram is used to determine where each datagram should be sent, and the process of making this determination and sending the datagram to its next hop is called forwarding. Both routers and hosts perform forwarding, although routers tend to do it much more often. There are three types of IP addresses, and the type affects how forwarding is performed: unicast (destined for a single host), broadcast (destined for all hosts on a given network), and multicast (destined for a set of hosts that belong to a multicast group). Chapter 2 looks at the types of addresses used with IP in more detail.

The Internet Control Message Protocol (ICMP) is an adjunct to IP, and we label it as a layer 3.5 protocol. It is used by the IP layer to exchange error messages and other vital information with the IP layer in another host or router. There are two versions of ICMP: ICMPv4, used with IPv4, and ICMPv6, used with IPv6. ICMPv6 is considerably more complex and includes functions such as address autoconfiguration and Neighbor Discovery that are handled by other protocols (e.g., ARP) on IPv4 networks. Although ICMP is used primarily by IP, it is also possible for applications to use it. Indeed, we will see that two popular diagnostic tools, ping and traceroute, use ICMP. ICMP messages are encapsulated within IP datagrams in the same way transport layer PDUs are.

The Internet Group Management Protocol (IGMP) is another protocol adjunct to IPv4. It is used with multicast addressing and delivery to manage which hosts are members of a multicast group (a group of receivers interested in receiving traffic for a particular multicast destination address). We describe the general properties of broadcasting and multicasting, along with IGMP and the Multicast Listener Discovery protocol (MLD, used with IPv6), in Chapter 9.

At layer 4, the two most common Internet transport protocols are vastly different. The most widely used, the Transmission Control Protocol (TCP), deals with problems such as packet loss, duplication, and reordering that are not repaired by the IP layer. It operates in a connection-oriented (VC) fashion and does not preserve message boundaries. Conversely, the User Datagram Protocol (UDP) provides little more than the features provided by IP. UDP allows applications to send datagrams that preserve message boundaries but imposes no rate control or error control.

TCP provides a reliable flow of data between two hosts. It is concerned with things such as dividing the data passed to it from the application into appropriately sized chunks for the network layer below, acknowledging received packets, and setting timeouts to make certain the other end acknowledges packets that are sent, and because this reliable flow of data is provided by the transport layer, the application layer can ignore all these details. The PDU that TCP sends to IP is called a TCP segment.

UDP, on the other hand, provides a much simpler service to the application layer. It allows datagrams to be sent from one host to another, but there is no guarantee that the datagrams reach the other end. Any desired reliability must be added by the application layer. Indeed, about all that UDP provides is a set of port numbers for multiplexing and demultiplexing data, plus a data integrity checksum. As we can see, UDP and TCP differ radically even though they are at the same layer. There is a use for each type of transport protocol, which we will see when we look at the different applications that use TCP and UDP.

There are two additional transport-layer protocols that are relatively new and available on some systems. As they are not yet very widespread, we do not devote much discussion to them, but they are worth being aware of. The first is the Datagram Congestion Control Protocol (DCCP), specified in [RFC4340]. It provides a type of service midway between TCP and UDP: connection-oriented exchange of unreliable datagrams but with congestion control. Congestion control comprises a number of techniques whereby a sender is limited to a sending rate in order to avoid overwhelming the network. We discuss it in detail with respect to TCP in Chapter 16.

The other transport protocol available on some systems is called the Stream Control Transmission Protocol (SCTP), specified in [RFC4960]. SCTP provides reliable delivery like TCP but does not require the sequencing of data to be strictly maintained. It also allows for multiple streams to logically be carried on the same connection and provides a message abstraction, which differs from TCP. SCTP was designed for carrying signaling messages on IP networks that resemble those used in the telephone network.

Above the transport layer, the application layer handles the details of the particular application. There are many common applications that almost every implementation of TCP/IP provides. The application layer is concerned with the details of the application and not with the movement of data across the network. The lower three layers are the opposite: they know nothing about the application but handle all the communication details.

### 1.3.2. Multiplexing, Demultiplexing, and Encapsulation in TCP/IP
We have already discussed the basics of protocol multiplexing, demultiplexing, and encapsulation. At each layer there is an identifier that allows a receiving system to determine which protocol or data stream belongs together. Usually there is also addressing information at each layer. This information is used to ensure that a PDU has been delivered to the right place. Figure 1-6 shows how demultiplexing works in a hypothetical Internet host.

Figure 1-6. The TCP/IP stack uses a combination of addressing information and protocol demultiplexing identifiers to determine if a datagram has been received correctly and, if so, what entity should process it. Several layers also check numeric values (e.g., checksums) to ensure that the contents have not been damaged in transit.

Image
Although it is not really part of the TCP/IP suite, we shall begin bottom-up and mention how demultiplexing from the link layer is performed, using Ethernet as an example. We discuss several link-layer protocols in Chapter 3. An arriving Ethernet frame contains a 48-bit destination address (also called a link-layer or MAC—Media Access Control—address) and a 16-bit field called the Ethernet Type. A value of 0x0800 (hexadecimal) indicates that the frame contains an IPv4 datagram. Values of 0x0806 and 0x86DD indicate ARP and IPv6, respectively. Assuming that the destination address matches one of the receiving system’s addresses, the frame is received and checked for errors, and the Ethernet Type field value is used to select which network-layer protocol should process it.

Assuming that the received frame contains an IP datagram, the Ethernet header and trailer information is removed, and the remaining bytes (which constitute the frame’s payload) are given to IP for processing. IP checks a number of items, including the destination IP address in the datagram. If the destination address matches one of its own and the datagram contains no errors in its header (IP does not check its payload), the 8-bit IPv4 Protocol field (called Next Header in IPv6) is checked to determine which protocol to invoke next. Common values include 1 (ICMP), 2 (IGMP), 4 (IPv4), 6 (TCP), and 17 (UDP). The value of 4 (and 41, which indicates IPv6) is interesting because it indicates the possibility that an IP datagram may appear inside the payload area of an IP datagram. This violates the original concepts of layering and encapsulation but is the basis for a powerful technique known as tunneling, which we discuss more in Chapter 3.

Once the network layer (IPv4 or IPv6) determines that the incoming datagram is valid and the correct transport protocol has been determined, the resulting datagram (reassembled from fragments if necessary) is passed to the transport layer for processing. At the transport layer, most protocols (including TCP and UDP) use port numbers for demultiplexing to the appropriate receiving application.

### 1.3.3. Port Numbers
Port numbers are 16-bit nonnegative integers (i.e., range 0–65535). These numbers are abstract and do not refer to anything physical. Instead, each IP address has 65,536 associated port numbers for each transport protocol that uses port numbers (most do), and they are used for determining the correct receiving application. For client/server applications (see Section 1.5.1), a server first “binds” to a port number, and subsequently one or more clients establish connections to the port number using a particular transport protocol on a particular machine. In this sense, port numbers act more like telephone number extensions, except they are usually assigned by standards.

Standard port numbers are assigned by the Internet Assigned Numbers Authority (IANA). The set of numbers is divided into special ranges, including the well-known port numbers (0–1023), the registered port numbers (1024–49151), and the dynamic/private port numbers (49152–65535). Traditionally, servers wishing to bind to (i.e., offer service on) a well-known port require special privileges such as administrator or “root” access.

The range of well-known ports is used for identifying many well-known services such as the Secure Shell Protocol (SSH, port 22), FTP (ports 20 and 21), Telnet remote terminal protocol (port 23), e-mail/Simple Mail Transfer Protocol (SMTP, port 25), Domain Name System (DNS, port 53), the Hypertext Transfer Protocol or Web (HTTP and HTTPS, ports 80 and 443), Interactive Mail Access Protocol (IMAP and IMAPS, ports 143 and 993), Simple Network Management Protocol (SNMP, ports 161 and 162), Lightweight Directory Access Protocol (LDAP, port 389), and several others. Protocols with multiple ports (e.g., HTTP and HTTPS) often have different port numbers depending on whether Transport Layer Security (TLS) is being used with the base application-layer protocol (see Chapter 18).

Note

If we examine the port numbers for these standard services and other standard TCP/IP services (Telnet, FTP, SMTP, etc.), we see that most are odd numbers. This is historical, as these port numbers are derived from the NCP port numbers. (NCP, the Network Control Protocol, preceded TCP as a transport-layer protocol for the ARPANET.) NCP was simplex, not full duplex, so each application required two connections, and an even-odd pair of port numbers was reserved for each application. When TCP and UDP became the standard transport layers, only a single port number was needed per application, yet the odd port numbers from NCP were used.

The registered port numbers are available to clients or servers with special privileges, but IANA keeps a reserved registry for particular uses, so these port numbers should generally be avoided when developing new applications unless an IANA allocation has been procured. The dynamic/private port numbers are essentially unregulated. As we will see, in some circumstances (e.g., on clients) the value of the port number matters little because the port number being used is transient. Such port numbers are also called ephemeral port numbers. They are considered to be temporary because a client typically needs one only as long as the user running the client needs service, and the client does not need to be found by the server in order to establish a connection. Servers, conversely, generally require names and port numbers that do not change often in order to be found by clients.

### 1.3.4. Names, Addresses, and the DNS
With TCP/IP, each link-layer interface on each computer (including routers) has at least one IP address. IP addresses are enough to identify a host, but they are not very convenient for humans to remember or manipulate (especially the long addresses used with IPv6). In the TCP/IP world, the DNS is a distributed database that provides the mapping between host names and IP addresses (and vice versa). Names are set up in a hierarchy, ending in domains such as .com, .org, .gov, .in, .uk, and .edu. Perhaps surprisingly, DNS is an application-layer protocol and thus depends on the other protocols in order to operate. Although most of the TCP/IP suite does not use or care about names, typical users (e.g., those using Web browsers) use names frequently, so if the DNS fails to function properly, normal Internet access is effectively disabled. Chapter 11 looks into the DNS in detail.

Applications that manipulate names can call a standard API function (see Section 1.5.3) to look up the IP address (or addresses) corresponding to a given host’s name. Similarly, a function is provided to do the reverse lookup—given an IP address, look up the corresponding host name. Most applications that take a host name as input also take an IP address. Web browsers support this capability. For example, the Uniform Resource Locators (URLs) http://131.243.2.201/index.html and http://[2001:400:610:102::c9]/index.html can be typed into a Web browser and are both effectively equivalent to http://ee.lbl.gov/index.html (at the time of writing; the second example requires IPv6 connectivity to be successful).

## 1.4. INTERNETS, INTRANETS, AND EXTRANETS
As suggested previously, the Internet has developed as the aggregate network resulting from the interconnection of constituent networks over time. The lowercase internet means multiple networks connected together, using a common protocol suite. The uppercase Internet refers to the collection of hosts around the world that can communicate with each other using TCP/IP. The Internet is an internet, but the reverse is not true.

One of the reasons for the phenomenal growth in networking during the 1980s was the realization that isolated groups of stand-alone computers made little sense. A few stand-alone systems were connected together into a network. Although this was a step forward, during the 1990s we realized that separate networks that could not interoperate were not as valuable as a bigger network that could. This notion is the basis for the so-called Metcalfe’s Law, which states roughly that the value of a computer network is proportional to the square of the number of connected endpoints (e.g., users or devices). The Internet idea, and its supporting protocols, would make possible the interconnection of different networks. This deceptively simple concept turns out to be remarkably powerful.

The easiest way to build an internet is to connect two or more networks with a router. A router is often a special-purpose device for connecting networks. The nice thing about routers is that they provide connections to many different types of physical networks: Ethernet, Wi-Fi, point-to-point links, DSL, cable Internet service, and so on.

Note

These devices are also called IP routers, but we will use the term router. Historically these devices were called gateways, and this term is used throughout much of the older TCP/IP literature. Today the term gateway is used for an application-layer gateway (ALG), a process that connects two different protocol suites (say, TCP/IP and IBM’s SNA) for one particular application (often electronic mail or file transfer).

In recent years, other terms have been adopted for different configurations of internets using the TCP/IP protocol suite. An intranet is the term used to describe a private internetwork, usually run by a business or other enterprise. Most often, the intranet provides access to resources available only to members of the particular enterprise. Users may connect to their (e.g., corporate) intranet using a virtual private network (VPN). VPNs help to ensure that access to potentially sensitive resources in an intranet is made available only to authorized users, usually using the tunneling concept we mentioned previously. We discuss VPNs in more detail in Chapter 7.

In many cases an enterprise or business wishes to set up a network containing servers accessible to certain partners or other associates using the Internet. Such networks, which also often involve the use of a VPN, are known as extranets and consist of computers attached outside the serving enterprise’s firewall (see Chapter 7). Technically, there is little difference between an intranet, an extranet, and the Internet, but the usage cases and administrative policies are usually different, and therefore a number of these more specific terms have evolved.

## 1.5. DESIGNING APPLICATIONS
The network concepts we have touched upon so far provide a fairly simple service model [RFC6250]: moving bytes between programs running on different (or, occasionally, the same) computers. To do anything useful with this capability, we need networked applications that use the network for providing services or performing computations. Networked applications are typically structured according to a small number of design patterns. The most common of these are client/server and peer-to-peer.

### 1.5.1. Client/Server
Most network applications are designed so that one side is the client and the other side is the server. The server provides some type of service to clients, such as access to files on the server host. We can categorize servers into two classes: iterative and concurrent. An iterative server iterates through the following steps:

I1. Wait for a client request to arrive.

I2. Process the client request.

I3. Send the response back to the client that sent the request.

I4. Go back to step I1.

The problem with an iterative server occurs when step I2 takes a long time. During this time no other clients are serviced. A concurrent server, on the other hand, performs the following steps:

C1. Wait for a client request to arrive.

C2. Start a new server instance to handle this client’s request. This may involve creating a new process, task, or thread, depending on what the underlying operating system supports. This new server handles one client’s entire request. When the requested task is complete, the new server instance terminates. Meanwhile, the original server instance continues to C3.

C3. Go back to step C1.

The advantage of a concurrent server is that the server just spawns other server instances to handle the client requests. Each client has, in essence, its own server. Assuming that the operating system allows multiprogramming (essentially all do today), multiple clients are serviced concurrently. The reason we categorize servers, and not clients, is that a client normally cannot tell whether it is talking to an iterative server or a concurrent server. As a general rule, most servers are concurrent.

Note that we use the terms client and server to refer to applications and not to the particular computer systems on which they run. The very same terms are sometimes used to refer to the pieces of hardware that are most often used to execute either client or server applications. Although the terminology is thus somewhat imprecise, it works well enough in practice. As a result, it is common to find a server (in the hardware sense) running more than one server (in the application sense).

### 1.5.2. Peer-to-Peer
Some applications are designed in a more distributed fashion where there is no single server. Instead, each application acts both as a client and as a server, sometimes as both at once, and is capable of forwarding requests. Some very popular applications (e.g., Skype [SKYPE], BitTorrent [BT]) are of this form. These applications are called peer-to-peer or p2p applications. A concurrent p2p application may receive an incoming request, determine if it is able to respond to the request, and if not forward the request on to some other peer. Thus, the set of p2p applications together form a network among applications, also called an overlay network. Such overlays are now commonplace and can be extremely powerful. Skype, for example, has grown to be the largest carrier of international telephone calls. According to some estimates, BitTorrent was responsible for more than half of all Internet traffic in 2009 [IPIS].

One of the primary problems in p2p networks is called the discovery problem. That is, how does one peer find which other peer(s) can provide the data or service it wants in a network where peers may come and go? This is usually handled by a bootstrapping procedure whereby each client is initially configured with the addresses and port numbers of some peers that are likely to be operating. Once connected, the new participant learns of other active peers and, depending on the protocol, what services or files they provide.

### 1.5.3. Application Programming Interfaces (APIs)
Applications, whether p2p or client/server, need to express their desired network operations (e.g., make a connection, write or read data). This is usually supported by a host operating system using a networking application programming interface (API). The most popular networking API is called sockets or Berkeley sockets, indicating where it was originally developed [LJFK93].

This text is not a programming text, but occasionally we refer to a feature of TCP/IP and whether that feature is provided by the sockets API or not. All of the programming details with examples for sockets can be found in [SFR04]. Modifications to sockets intended for use with IPv6 are also described in a number of freely available online documents [RFC3493][RFC3542][RFC3678][RFC4584][RFC5014].

## 1.6. STANDARDIZATION PROCESS
Newcomers to the TCP/IP suite often wonder just who is responsible for specifying and standardizing the various protocols and how they operate. A number of organizations represent the answer to this question. The group with which we will most often be concerned is the Internet Engineering Task Force (IETF) [RFC4677]. This group meets three times each year in various locations around the world to develop, discuss, and agree on standards for the Internet’s “core” protocols. Exactly what constitutes “core” is subject to some debate, but common protocols such as IPv4, IPv6, TCP, UDP, and DNS are clearly in the purview of IETF. Attendance at IETF meetings is open to anyone, but it is not free.

IETF is a forum that elects leadership groups called the Internet Architecture Board (IAB) and the Internet Engineering Steering Group (IESG). The IAB is chartered to provide architectural guidance to activities in IETF and to perform a number of other tasks such as appointing liaisons to other standards-defining organizations (SDOs). The IESG has decision-making authority regarding the creation and approval of new standards, along with modifications to existing standards. The “heavy lifting” or detailed work is generally performed by IETF working groups that are coordinated by working group chairs who volunteer for this task.

In addition to the IETF, there are two other important groups that interact closely with the IETF. The Internet Research Task Force (IRTF) explores protocols, architectures, and procedures that are not deemed mature enough for standardization. The chair of the IRTF is a nonvoting member of IAB. The IAB, in turn, works with the Internet Society (ISOC) to help influence and promote worldwide policies and education regarding Internet technologies and usage.

### 1.6.1. Request for Comments (RFC)
Every official standard in the Internet community is published as a Request for Comments, or RFC. RFCs can be created in a number of ways, and the publisher of RFCs (called the RFC editor) recognizes multiple document streams corresponding to the way an RFC has been developed. The current streams (as of 2011) include the IETF, IAB, IRTF, and independent submission streams. Prior to being accepted and published (permanently) as an RFC, documents exist as temporary Internet drafts while they receive comments and progress through the editing and review process.

All RFCs are not standards. Only so-called standards-track category RFCs are considered to be official standards. Other categories include best current practice (BCP), informational, experimental, and historic. It is important to realize that just because a document is an RFC does not mean that the IETF has endorsed it as any form of standard. Indeed, there exist RFCs on which there is significant disagreement.

The RFCs range in size from a few pages to several hundred. Each is identified by a number, such as RFC 1122, with higher numbers for newer RFCs. They are all available for free from a number of Web sites, including http://www.rfc-editor.org. For historical reasons, RFCs are generally delivered as basic text files, although some RFCs have been reformatted or authored using more advanced file formats.

A number of RFCs have special significance because they summarize, clarify, or interpret particular sets of other standards. For example, [RFC5000] defines the set of all other RFCs that are considered official standards as of mid-2008 (the most recent such RFC at the time of writing). An updated list is available at the current standards Web site [OIPSW]. The Host Requirements RFCs ([RFC1122] and [RFC1123]) define requirements for protocol implementations in Internet IPv4 hosts, and the Router Requirements RFC [RFC1812] does the same for routers. The Node Requirements RFC [RFC6434] does both for IPv6 systems.

### 1.6.2. Other Standards
Although the IETF is responsible for standardizing most of the protocols we discuss in this text, other SDOs are responsible for defining protocols that merit our attention. The most important of these groups include the Institute of Electrical and Electronics Engineers (IEEE), the World Wide Web Consortium (W3C), and the International Telecommunication Union (ITU). In their activities relevant to this text, IEEE is concerned with standards below layer 3 (e.g., Wi-Fi and Ethernet), and W3C is concerned with application-layer protocols, specifically those related to Web technologies (e.g., HTML-based syntax). ITU, and more specifically ITU-T (formerly CCITT), standardizes protocols used within the telephone and cellular networks, which is becoming an ever more important component of the Internet.

## 1.7. IMPLEMENTATIONS AND SOFTWARE DISTRIBUTIONS
The historical de facto standard TCP/IP implementations were from the Computer Systems Research Group (CSRG) at the University of California, Berkeley. They were distributed with the 4.x BSD (Berkeley Software Distribution) system and with the BSD Networking Releases until the mid-1990s. This source code has been the starting point for many other implementations. Today, each popular operating system has its own implementation. In this text, we tend to draw examples from the TCP/IP implementations in Linux, Windows, and sometimes FreeBSD and Mac OS (both of which are derived from historical BSD releases). In most cases, the particular implementation matters little.

Figure 1-7 shows a chronology of the various BSD releases, indicating the important TCP/IP features we cover in later chapters. It also shows the years when Linux and Windows began supporting TCP/IP. The BSD Networking Releases shown in the third column were freely available public source code releases containing all of the networking code, both the protocols themselves and many of the applications and utilities (e.g., the Telnet remote terminal program and FTP file transfer program).

Figure 1-7. The history of software releases supporting TCP/IP up to 1995. The various BSD releases pioneered the availability of TCP/IP. In part because of legal uncertainties regarding the BSD releases in the early 1990s, Linux was developed as an alternative that was initially tailored for PC users. Microsoft began supporting TCP/IP in Windows a couple of years later.

Image
By the mid-1990s, the Internet and TCP/IP were well established. All subsequent popular operating systems support TCP/IP natively. Research and development of new TCP/IP features, previously found first in BSD releases, are now typically found first in Linux releases. Windows has recently implemented a new TCP/IP stack (starting with Windows Vista) with many new features and native IPv6 capability. Linux, FreeBSD, and Mac OS X also support IPv6 without setting any special configuration options.

## 1.8. ATTACKS INVOLVING THE INTERNET ARCHITECTURE
Throughout the text we shall briefly describe attacks and vulnerabilities that have been discovered in the design or implementation of the topic we are discussing. Few attacks target the Internet architecture as a whole. However, it is worth observing that the Internet architecture delivers IP datagrams based on destination IP addresses. As a result, malicious users are able to insert whatever IP address they choose into the source IP address field of each IP datagram they send, an activity called spoofing. The resulting datagrams are delivered to their destinations, but it is difficult to perform attribution. That is, it may be difficult or impossible to determine the origin of a datagram received from the Internet.

Spoofing can be combined with a variety of other attacks seen periodically on the Internet. Denial-of-service (DoS) attacks usually involve using so much of some important resource that legitimate users are denied service. For example, sending so many IP datagrams to a server that it spends all of its time just processing the incoming packets and performing no other useful work is a type of DoS attack. Other DoS attacks may involve clogging the network with so much traffic that no other packets can be sent. This is often accomplished by using many sending computers, forming a distributed DoS (DDoS) attack.

Unauthorized access attacks involve accessing information or resources in an unauthorized fashion. This can be accomplished with a variety of techniques such as exploiting protocol implementation bugs to take control of a system (called 0wning the system and turning it into a zombie or bot). It can also involve various forms of masquerading such as an attacker’s agent impersonating a legitimate user (e.g., by running with the user’s credentials). Some of the more pernicious attacks involve taking control of many remote systems using malicious software (malware) and using them in a coordinated, distributed fashion (called botnets). Programmers who intentionally develop malware and exploit systems for (illegal) profit or other malicious purposes are generally called black hats. So-called white hats do the same sorts of technical things but notify vulnerable parties instead of exploit them.

One other concern with the Internet architecture is that the original Internet protocols did not perform any encryption in support of authentication, integrity, or confidentiality. Consequently, malicious users could usually ascertain private information by merely observing packets in the network. Those with the ability to modify packets in transit could also impersonate users or alter the contents of messages. Although these problems have been reduced significantly thanks to encryption protocols (see Chapter 18), old or poorly designed protocols are still sometimes used that are vulnerable to simple eavesdropping attacks. Given the prevalence of wireless networks, where it is relatively easy to “sniff” the packets sent by others, such older or insecure protocols should be avoided. Note that while encryption may be enabled at one layer (e.g., on a link-layer Wi-Fi network), only host-to-host encryption (IP layer or above) protects information across the multiple network segments an IP datagram is likely to traverse on its way to its final destination.

## 1.9. SUMMARY
This chapter has been a whirlwind tour of concepts in network architecture and design in general, plus the TCP/IP protocol suite in particular that we discuss in detail in later chapters. The Internet architecture was designed to interconnect different existing networks and provide for a wide range of services and protocols operating simultaneously. Packet switching using datagrams was chosen for its robustness and efficiency. Security and predictable delivery of data (e.g., bounded latency) were secondary concerns.

Based on their understanding of layered and modular software design in operating systems, the early implementers of the Internet protocols adopted a layered design that employs encapsulation. The three main layers in the TCP/IP protocol suite are the network layer, transport layer, and application layer, and we mentioned the different responsibilities of each. We also mentioned the link layer because it relates so closely with the TCP/IP suite. We shall discuss each in more detail in subsequent chapters.

In TCP/IP, the distinction between the network layer and the transport layer is critical: the network layer (IP) provides an unreliable datagram service and must be implemented by all systems addressable on the Internet, whereas the transport layers (TCP and UDP) provide an end-to-end service to applications running on end hosts. The primary transport layers differ radically. TCP provides in-ordered reliable stream delivery with flow control and congestion control. UDP provides essentially no capabilities beyond IP except port numbers for demultiplexing and an error detection mechanism. Unlike TCP, however, it supports multicast delivery.

Addresses and demultiplexing identifiers are used by each layer to avoid confusing protocols or different associations/connections of the same protocol. Link-layer multi-access networks often use 48-bit addresses; IPv4 uses 32-bit addresses and IPv6 uses 128-bit addresses. The TCP and UDP transport protocols use distinct sets of port numbers. Some port numbers are assigned by standards, and others are used temporarily, usually by client applications when communicating with servers. Port numbers do not represent anything physical; they are merely used as a way for applications that want to communicate to rendezvous.

Although port numbers and IP addresses are usually enough to identify the location of a service on the Internet, they are not very convenient for humans to remember or use (especially IPv6 addresses). Consequently, the Internet uses a hierarchical system of host names that can be converted to IP addresses (and back) using DNS, a distributed database application running on the Internet. DNS has become an essential component of the Internet infrastructure, and efforts are under way to make it more secure (see Chapter 18).

An internet is a collection of networks. The common building block for an internet is a router that connects the networks at the IP layer. The “capital-I” Internet is an internet that spans the globe and interconnects over two billion users (as of 2011). Private internets are called intranets and are usually connected to the Internet using special devices (firewalls, discussed in Chapter 10) that attempt to prevent unauthorized access. Extranets usually consist of a subset of an institution’s intranet that is designed to be accessed by partners or affiliates in a limited way.

Networked applications are usually designed using a client/server or peer-to-peer design pattern. Client/server is more popular and traditional, but peer-to-peer designs have also seen tremendous success. Whatever the design pattern, applications invoke APIs to perform networking tasks. The most common API for TCP/IP networks is called sockets. It was provided with BSD UNIX distributions, software releases that pioneered the use of TCP/IP. By the late 1990s the TCP/IP protocol suite and sockets API were available on every popular operating system.

Security was not a major design goal for the Internet architecture. Determining where packets originate can be difficult for a receiver, as end hosts can easily spoof source IP addresses in unsecured IP datagrams. Distributed DoS attacks also remain an ongoing challenge because victim end hosts can be collected together to form botnets that can carry out DDoS and other attacks, sometimes without the system owners’ knowledge. Finally, early Internet protocols did little to ensure privacy of sensitive information, but most of those protocols are now deprecated, and modern replacements use encryption to provide confidential and authenticated communications between hosts.

## 1.10. REFERENCES
[B64] P. Baran, “On Distributed Communications: 1. Introduction to Distributed Communications Networks,” RAND Memorandum RM-3420-PR, Aug. 1964.

[BT] http://www.bittorrent.com

[C88] D. Clark, “The Design Philosophy of the DARPA Internet Protocols,” Proc. ACM SIGCOMM, Aug. 1988.

[CK74] V. Cerf and R. Kahn, “A Protocol for Packet Network Intercommunication,” IEEE Transactions on Communications, COM-22(5), May 1974.

[D08] J. Day, Patterns in Network Architecture: A Return to Fundamentals (Prentice Hall, 2008).

[D68] E. Dijkstra, “The Structure of the ‘THE’-Multiprogramming System,” Communications of the ACM, 11(5), May 1968.

[DBSW66] D. Davies, K. Bartlett, R. Scantlebury, and P. Wilkinson, “A Digital Communications Network for Computers Giving Rapid Response at Remote Terminals,” Proc. ACM Symposium on Operating System Principles, Oct. 1967.

[I96] IBM Corporation, Systems Network Architecture—APPN Architecture Reference, Document SC30-3422-04, 1996.

[IPIS] Ipoque, Internet Study 2008/2009, http://www.ipoque.com/resources/internet-studies/internet-study-2008_2009

[K64] L. Kleinrock, Communication Nets: Stochastic Message Flow and Delay (McGraw-Hill, 1964).

[LC04] S. Lin and D. Costello Jr., Error Control Coding, Second Edition (Prentice Hall, 2004).

[LJFK93] S. Leffler, W. Joy, R. Fabry, and M. Karels, “Networking Implementation Notes—4.4BSD Edition,” June 1993.

[LT68] J. C. R. Licklider and R. Taylor, “The Computer as a Communication Device,” Science and Technology, Apr. 1968.

[OIPSW] http://www.rfc-editor.org/rfcxx00.html

[P07] J. Pelkey, Entrepreneurial Capitalism and Innovation: A History of Computer Communications 1968–1988, available at http://historyofcomputercommunications.info

[P73] L. Pouzin, “Presentation and Major Design Aspects of the CYCLADES Computer Network,” NATO Advanced Study Institute on Computer Communication Networks, 1973.

[RFC0871] M. Padlipsky, “A Perspective on the ARPANET Reference Model,” Internet RFC 0871, Sept. 1982.

[RFC0959] J. Postel and J. Reynolds, “File Transfer Protocol,” Internet RFC 0959/STD 0009, Oct. 1985.

[RFC1122] R. Braden, ed., “Requirements for Internet Hosts—Communication Layers,” Internet RFC 1122/STD 0003, Oct. 1989.

[RFC1123] R. Braden, ed., “Requirements for Internet Hosts—Application and Support,” Internet RFC 1123/STD 0003, Oct. 1989.

[RFC1812] F. Baker, ed., “Requirements for IP Version 4 Routers,” Internet RFC 1812, June 1995.

[RFC3493] R. Gilligan, S. Thomson, J. Bound, J. McCann, and W. Stevens, “Basic Socket Interface Extensions for IPv6,” Internet RFC 3493 (informational), Feb. 2003.

[RFC3542] W. Stevens, M. Thomas, E. Nordmark, and T. Jinmei, “Advanced Sockets Application Program Interface (API) for IPv6,” Internet RFC 3542 (informational), May 2003.

[RFC3678] D. Thaler, B. Fenner, and B. Quinn, “Socket Interface Extensions for Multicast Source Filters,” Internet RFC 3678 (informational), Jan. 2004.

[RFC3787] J. Parker, ed., “Recommendations for Interoperable IP Networks Using Intermediate System to Intermediate System (IS-IS),” Internet RFC 3787 (informational), May 2004.

[RFC6434] J. Loughney, E. Jankiewicz, and T. Narten, “IPv6 Node Requirements,” Internet RFC 6434 (informational), Dec. 2011.

[RFC4340] E. Kohler, M. Handley, and S. Floyd, “Datagram Congestion Control Protocol (DCCP),” Internet RFC 4340, Mar. 2006.

[RFC4584] S. Chakrabarti and E. Nordmark, “Extension to Sockets API for Mobile IPv6,” Internet RFC 4584 (informational), July 2006.

[RFC4677] P. Hoffman and S. Harris, “The Tao of IETF—A Novice’s Guide to the Internet Engineering Task Force,” Internet RFC 4677 (informational), Sept. 2006.

[RFC4960] R. Stewart, ed., “Stream Control Transmission Protocol,” Internet RFC 4960, Sept. 2007.

[RFC5000] RFC Editor, “Internet Official Protocol Standards,” Internet RFC 5000/STD 0001 (informational), May 2008.

[RFC5014] E. Nordmark, S. Chakrabarti, and J. Laganier, “IPv6 Socket API for Source Address Selection,” Internet RFC 5014 (informational), Sept. 2007.

[RFC6250] D. Thaler, “Evolution of the IP Model,” Internet RFC 6250 (informational), May 2011.

[RFC6434] J. Loughney, E. Jankiewicz, and T. Narten, “IPv6 Node Requirements,” Internet RFC 6434 (informational), Dec. 2011.

[SFR04] W. R. Stevens, B. Fenner, and A. Rudoff, UNIX Network Programming, Volume 1, Third Edition (Prentice Hall, 2004).

[SKYPE] http://www.skype.com

[SRC84] J. Saltzer, D. Reed, and D. Clark, “End-to-End Arguments in System Design,” ACM Transactions on Computer Systems, 2(4), Nov. 1984.

[W02] M. Waldrop, The Dream Machine: J. C. R. Licklider and the Revolution That Made Computing Personal (Penguin Books, 1992).

[X85] Xerox Corporation, Xerox Network Systems Architecture—General Information Manual, XNSG 068504, 1985.

[Z80] H. Zimmermann, “OSI Reference Model—The ISO Model of Architecture for Open Systems Interconnection,” IEEE Transactions on Communications, COM-28(4), Apr. 1980.