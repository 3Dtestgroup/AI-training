# **Reorganize the in-class lesson notes from live video_20190615**



然后，我们为什么要搞一个这个样子的东西出来，用这个东西来求邻居数的和，就是，你现在可以想象，比方说，这是一张纸，一个方形的纸这些纸它有很多格子，然后这些格子里面有的是1，有的是0，我们里面有一些随机数，然后我们把这个中间的部分做一个交互，然后我们把这个交互拿起来，然后我们开始移动这个交互，我们可以把这个交互向这个方向移动，我们把这个放到这里来，把它堆到最左上角，他就可以把它所有的1和0都粘起来，粘起来以后我们把它贴到中间来，然后，再做同样的操作，在这个方向，把这条边贴到最顶上，再粘一下。。。。。。。他就好像一个装置一样，你的一个操作就把周围8个方向贴8个边，一共做了8次操作以后，就把所有的单个量周围8个点上的1加过来了，只要你粘过以后，你相当于把所有的数字都加到这个点上，所以说，我们在这个最初的矩阵表示上面，直接做出来一个neiboor的array，你做完这个操作以后，得到一个矩阵，我们得到一个矩阵以后，我们剩下的事情就好办了因为我只需要在这个邻居矩阵上去做判断，就是apply我的那些规则，那些规则其实就那些，这个矩阵就一开始的z这个矩阵里面它就是很多01，n这个矩阵上同样的，它最大的是8，然后最小的是0，就这些数，我 对n里面的每一个点都做一个，我要符合规则，apply了这些rule以后，那我就得出一个结论来，或者生，或者死，所以这个循环就完成了。大家可以看一下这个东西的document，他是啥意思呢。下面是rule，输入是一个表达式，输入大于1的，最后它会回来一些位置，我们就用这个东西来拼一个结果出来。这就是我们这个idao的基本的想法，就是你想用这个之前，把这个，这块大家看得懂吗，这是最关键的一段，就是我们没有用for循环，我们在每一个这个东西比方说这个z1它其实是在这一个大块，这样的一个矩形，差不多是100万的矩形，累加一遍，把它叠加起来，加了一遍以后，我们就得到了n中间的几个数，然后，为什么我们只的n中间的数？因为周围的数我们不理，应该都是0，就是大家可以看他，他在这个，你可以把代码写成2维的模式，在视觉上看到的和我们思维想的是一样的，你也可以加一些空格把他们都对齐，大家能明白吗这是在干什么吗？所以你只要把这些index的值都对应了，你的加法就一定是对的，做完这个加法以后，我们就在这个n上面开始选，然后我们搞出来4个规则，其实是故意搞得复杂一点的因为规则是可以化简的。然后根据这些规则，我们就这些就是一些index，我们把这些index置0，置0的意思就是说这2个是死的规则，这2个是生的规则，我们把边上的东西都清一遍，把周围的都清理一遍，这样就完成了，这是一个初始的解，然后，大家可以看一下这个，打印一下中间的结果。大概就是像这样的。然后我们算一下它的时间，它应该是200多毫秒跑了3遍，应该每一轮是70多毫秒，70多毫秒其实已经比我们昨天见得要快了，这是我们用numpy的一个一开始给的完全是用python写的，这是用numpy写的，这里引用了非常多的概念，就是我们如何去做邻居，算这个邻居的矩阵，就是以cell为单位思考这个问题，而不是以整个矩阵为单位思考这个问题，我们思考的抽象方式其实更高，就是像这个操作它其实是一个很大的操作，但是，你不要觉得很大就很难，速度还可以，这一部分是我们后面要保留的，就是这一步，我们没有要改进的余地了但是这一笔有点啰嗦，我们看看可不可以搞得再快一点，我们刚才有几个一看就知道它肯定会浪费时间的就是我们要把copy去掉，我们就直接用view，直接操作。这样的话占用的内存是同一个会减少点时间，其实，最关键的点是这里，其实一开始我们就把memory的size降下来了，就是，原来可能4兆，现在只有1兆，大家可以试一下，我们现在这种解法其实是有上限的，因为假设我们100亿这种量级，会导致内存被吃爆，因为我们需要2块大数据，一块点，一块邻居，这是他是有一定限度的，这次我们再做一下改进，这个改进的点。是不是快了？变成30多毫秒，大概提速了2倍，第一次最快，2秒变成70毫秒，继续往下减，我们也可以这样做，底下这个置0的操作可以和下面并起来，它其实也在置0，考虑到昨天看到的所有的图像，我感觉他总是稀疏的，如果不是太密的话，它也会立即变得稀疏，他在第一个循环里大部分都挤死了，所以他总是稀疏的话意味着置0的点一定大大多于置1的点，我们就可以做一次统一置0，然后，在置1，也就是说，这个地21,22,26可以合并，合并完以后再试图合并22,24行。再往下减，只有一次置0操作，置0操作前，我们干了一件事，就是你在这之前你必须记住某一些值，有一些现在存活，周围邻居是2的点，它应该仍然存活，但是如果你现在把它置0了，这个信息就丢到了，你没法通知到这种情况是不是曾经发生过，就是说你会丢到一些存活的点，你的规则就搞错了，所以你要存一下，存一下以后你再置回来。如果原来是1，邻居3，它还是1，如果他原来是0，邻居是3，现在1，所以我就把条件简化了，规则化简，这个大家搞懂了吧。已经20毫秒了，再简化，这是我写的最初的一个，这很好，这只有4行，这2行没什么信息量，就是在置0，但这个是有问题的，看上去很简洁，其实漏掉了我刚才说的那种情况，原来是2的情况，被我搞没了。然后这就是我昨天的那个东西，这个解其实跟我们的解一模一样他在数学上是一模一样的，你可以看这一部分，等号右边的部分就是再算邻居解的部分，我们这个表达式这么啰嗦的原因就是我们没法更简化它。



但是它是一种更简洁的表达方式。就他只写它必须的字符，他一共只有不到10个字符，就表达了很多，这就是他要干的事情。它读代码的方式完全不一样。然后我们来讨论一下这个问题，就是我们刚才的解法，你看懂了就是看懂了，而且这个code跟边界没有关系，它只跟内存限制有关系，一旦他写好后，你好像一个编码一样，你已经incode在你的function里面，已经完美了，就是，这是我们的这个代码，大家可以看一下。我一会给你们讲讲这个代码。



开始，下午我们学概论统计，概率统计这个大纲是这样它是先讲的统计，就是先讲数据统计分析这部分，然后，它讲概率的问题，它讲分布很少，我个人感觉你要学数学，我们学了4个数学，一个初等代数，微积分，线性代数，和概率，我个人感觉最难的是概率，为什么这样说呢，因为其他这几个数学，就是你的思路是很明确的，我要微分，我要积分，我要分解多项式，我算矩阵，求逆，你肯定是有一个非常明确的目标的，但是概率这个问题，它很大问题它的思维是没有起点的，就是你不知道从哪开始想这个问题，这是它难的地方，另一个就是，它特别注重概念，它不是一个推理或者是一步一步推算的问题，它特别注重概念，你要理解它，就是概念的东西你要么理解，要么不理解，不存在一个中间步骤，所以，它的很多题目也有类似的特点。就是，我找了一些题。大家看一下。然后，我们有一大堆证明，看见了吧，先给大家一些印象，因为我觉得你学这个数理统计这一部分，其实你看他的作业你看看pandas，你基本都能明白了，它主要是一个应用工具的过程，但是，我觉得我们学的目的不是我们学会用这个工具，这个没有太大意思，我们要学会一种思维方式，就是，怎么样来考虑问题，一直到条件概率这里，有这么一堆问题大家可以想一想，可以做一做。这些问题在数学上有一个分类，涂点概率模型，其实，所谓古典离散的，不是连续的，然后，跟这个基数有很大的关系，你看我们这些题基本都是基数的。而且我们这6个证明题一道都不要用公式的推导去证明，就是你们可以试一试，你用数学方法可以证明其中的一些定理但是会很麻烦，你可能整个下午就在做这些题，但是他们都有简单的方法，而且他们的办法都一样，就是，我其实在重复同一个idea，就是形式不一样但是它的基本的想法是一模一样的，然后，看这个问题，就是计数的问题，我们给它统计一下哪种拿法，很多种题，我们从头开始，讲到中间的时候我们再来做这些题，先来点轻松的，反正笔记都在这。从分析数据样本开始，用了很多pandas的东西，因为很方便，有现成的库可以调用，其实你不用也一样，这个球均值大家都知道，首先求出和来然后再一除就是均值，在这个调用里面，然后中值，中值这个东西它有2个东西，一个叫media，然后一个叫mode，就是media翻译成中位数，上下差不多，这个是出现最高频率的，出现最高频率的是中数，它肯定这个5w最高的，我们很容易找到一个数据集有好几个，这样子。众数就是2个。分布密度，然后我们现在研究分布，分布信息最全的就是那个样本，但是，我们希望在那个样本里面拿到一些数值特征，有各种各样的做法，可以看到分布在什么范围之内，我们把值都算出来，然后5个值，通常来说，数据集，你看这5个指标会获得一种感觉，然后我们给他画下来，画一个立方图。通常，均值都比中值高的多。然后这个不是高斯概率分布，他是一个函数，我们刚才画了一个离散分布的直方图，因为这是一些采样点，我们是希望画出一个连续的分布曲线，就比方说所有人群，我们只有这点数据，我们怎么去猜这个它的分布，我们有一个函数调用，大家可以看一下，看下这文档，其实它画出来的曲线跟下面这个直方图看起来挺吻合的，至少直方图高的地方它也高，直方图偏左它也偏左，然后看这个图，我们给他一个定性的名字，叫偏态峰，这个统计的是学习时间，大部分人很努力的。所以大家从名字能推算出来正态分布从哪里来的，有偏态就有正态，这个放在中间就是正态，正态分布是分数，是乘积，看了这个上学的学习的时间，这个毕业以后赚的钱，这是学习成绩。为什么是一个正态分布，就是它是被事先设定的，所有的大规模正式的考试，它都有测量指标的，它要求最后所有人的分数是这个样子的，如果你最后的成绩不能成这个曲线，那你这个出题就是错误的，事故。高斯分布我们很熟悉，可能最著名的连续的分布就是高斯分布，不连续的最著名的分布式什么？ksi分布，是一个万能的东西，然后高斯分布式大量的连续图像里面的。偏度和峰度，然后我们调用一下。偏度我们刚才知道了，峰度是什么意思，这个这个是瘦还是胖，瘦就代表分布非常集中，胖的话就代表分布不是那么的紧，这都是一些测量。就这么简单。这是range，但其实如果我只告诉你range，你是没有感觉的，因为就是你能说这三个哪个大码，它要跟他的range做一个百分比，要归一化，现在只是算一个数，你看不出，所以要用这个百分比，然后我们选择的是上面分数的这一行，你可以，这里面有一个57，大概注意一下这个数据不是排好的，他没有顺序就是，他的意思是什么，假设你的分数是57，你在班里面是怎么排名，排名就是你是百分之多少，百分之多少的人被你打败了。你注意一下他的调用。然后，跟刚才我们算的众数，众数有好几个数都是一样的。然后，四分位数，意思是我们刚才单独拿了一个样本，来看你在班里的水平是怎么样的，我们现在想看全班同学的情况，就是我们要看你是在20%的区间，就是这个意思，最后画出来这样的图。



然后我们看一下例外，我们怎么处理这种，这个呢就是把这个算上这个，算出来后画出来的是这种情况，这就是高的点，挣的很多的同学，有例外以后大家就需要解释这个，，其实你正常的话你不需要解释，例外得解释，有了例外以后有2种情况就是这个，你觉得这个例外是有问题的还是没有，重新做数据分析，第二就是你承认也可以，然后，这就是排除掉这个例外，这是不排除，然后，假设我们搞得人多一点，就是，不是几个人，我们全年级全市，全国，意外就很难出现了。方差，标准差，刚才我们讲了测量分布，百分比，4分位啊，是一些方法但是有一个更常用的方法就是我们用一个值，方差来表示分布期望之外的参数，定义的公式。然后我们做一下平方根，平方根的好处就是可以把负值去掉，再开一下方，是一样的。调用的这个。这个我们大家都很熟悉的我们在前面的课里面讲这个numpy的时候也都提到了这个概念，甚至做了跟多的题，这个很有意思，大家可以看看这个东西，画一个图出来。你知道这个定理的名字？这个特点，百分之98，百分之68百分之99.7定理，听起来很啰嗦但是其实就是怪名字做的特性，就是它为什么选这3个数，就是标准差参数，1倍 ，2倍，3倍，你看，3倍的时候基本上所有的东西都被包括进来了。给大家做个题，这个归一化，归一化这个概念知道吗？你们往后学，这个东西挺威望的，动不动就出归一化，不归一化其实你搞得这些数据你在瞎弄，就全都污染了，就没有意义了，我们刚才学的几个都打印出来了。然后我给你一组数据，你就算一下discribe，完了呢就画一个图，然后一个直方图，分析完毕。然后我们看多变量数据，我们分析不是那么简单，只是考个分数分析一下，我们要把很多维度的测量关联起来，还是刚才那个，然后多变量数据分析你要把他们归到0和1之间，然后，怎么变呢，就搞一个函数，本来这个不在numpy里面，就自己弄一个，不是很复杂，然后你做了这个0到1之间的数据以后，你发现你就可以比较了，这是这三个东西。你就只看这个你绝得有相似性吗，看不出来，但是能看出来是高是低，大概的平均量的分布。分数值最好的，看起来是一个均匀的分布，然后这个时间跟收入这些值钱的东西分布不怎么均匀，这其实是可以解释的，下面来解释一下，这个散点图画的是分数和工资，是不是正相关，是你学习成绩越好，你挣的越多，画一条线。这个是相关系数的数学定义，它也有个函数可以调它，然后这个值0.81，我们看一下定义，0就是正相关，符合我们刚才的感觉，负的是负相关。这其实带来一个问题，就是我们现在在数轴上，这叫正相关，不相关还有一种叫法，独立，所以负相关不是独立，所以有的人逻辑上就乱了，这个正相关肯定不独立，一样的，互斥事件一定是不独立事件，只要有我就没你，他们互斥，所以不独立，独立就是有没有你跟我都没关系。大家猜一下学习成绩和时间的相关性，和学习成绩和收入的相关性，哪一个会更大，肯定是相关的。
你其实心里有一个判断，不管你画出来是什么，然后最小二乘拟合，这个其实是机器学习最经典的起点，画一条线出来，然后，这段代码就是刚才公式的实现，最关键的就是算这个斜率。基本上你所有的可以处理数据序列的软件都有这个东西，excel都有，最基本的，这个是吧这个异常点去掉的，数据清理的概念，然后，我们把这个分开来讲，我们前面就相当于做了一个模型出来，把那个斜率跟截距的线给画出来，就是我们的预测模型，然后，我们用这个预测模型归类，其实一大堆的AI的工程的剧本结构就是这样的，通过数据搞一个模型出来，然后你再归类，所以你从刚才计算的角度来看，我们从散点里面画出一条线来，然后一大堆算，但是，那个叫training，这个叫预测模型已经搞好了，你会发现这个简单这个口算都能算出来，所以通常就是mode一旦training好了，它需要的计算资源就不是那么多，你只要跑这个model就很快，8万多。
好，我们讲这个概率，这一段比较简单，做这个数学的统计分析，这个概率我记得我们当时学这个的时候，不是第一就明白概率的概念，我们还要高一些其他的东西，集合的概念，计数，组合数，一会我们会有这种题目的，这里面最有用的概念应该就是概率之和等于1，这根据定义，所以就是一个事件它的集合和他的补集的和加起来是1，就是这个定义。条件概率和独立，刚才我们已经讲过独立了，独立事件，比方说抛硬币，这是最简单的，你这次拋完和下次抛完没有关系。



我们先讲一个案例，这是一个比较好玩的案子，检察官案例，新生儿突然死亡症的概率是1/8000，有个医学教授认为这是一种非常罕见的病，那连续两个得病的概率就是要7000多万分之一了，法庭上当做证据来证明是不可能的，法官把母亲判了。这是一个真实的案例，从道理上来说这个合理吗？如果不合理怎么来打败他，它的概念错在哪了？两个时间不独立，如果一个孩子死了，那第二个孩子死的概率特别高，是有关联的。 

独立事件乘法原则，投硬币，计数，基本就一半一半，所以说数学一定要知道他的条件，定义域。这是我刚才说的互斥事件，条件概率很有用，A和B同时发生的概率除以A发生的概率。也可以把条件概率连起来，连起来就是贝叶斯。



这是组合数的算法，就是n个东西里面拿K个，然后不能再放回去，不管顺序，一共有多少种拿法，然后大家在公式上想出来什么问题，怎么做到的。其实就是出一下，把order除掉。把它分成两个部分。我们画一个象限，两种交易的方法，就是换不换，允不允许拿出来再放回去，这个把他叫做replace。然后我们偏一下这个象限，可以replace也有order，如果是N个里面拿K个，n的k次方。大家想想不准放回去也不记order，有多少种可能？我们把它写在这里。排列数是k。你画一个全的象限，然后各种各样的情况你都考虑到了，所以你可以计数。

丢硬币如果有两次正面的概率，这种离散的概率你写的时候你都写event=2然后连续的概率你可以写大于，底下为什么要除以8，这是三次所有的情况，然后有两次正面概率分布是怎么搞得？只要挑出来是嘛两个正面，算一个概率分布，显然有两次正面的概率肯定比一次负面的概率大。把他画出来，大家看了有没有眼熟，像正态分布。泊松分布，伯努利，他们都是有联系的，，假设概率发生是有偏的，不是一半一半，怎么来算这个东西，就是把概率乘进去，一共扔了n次，，有多少个k，哪些位置发生了K。这个事件发生概率是p，n-k次是他的补集。这就是二项式分布，为什么是二项式，因为这个跟二项式的系数是一样的。大家回忆起来就是skewness，这个东西不是1/2,。Numpy里面没有分布的函数，Scipy里面有。然后PMF叫possibility mass function,这是离散的概率分布，我们以前证明过一个概率密度，扔硬币这种事情扔多了，最后就是正态分布。

既然是分布的话就会讲期望，方差，这是这个公式，你能够证明这个公式。做100此实验，或者是0或者是1，最后加起来应该是25.。我们来证明这个公式，你可以往二项式定理那里证（a+b）^n，把它展开以后应该是什么样的，如果n=2的话，a^2+2ab+b^2, 这就是二项式定理。如果二项式定理成立的话，a等于1，b等于几。

因为你写出来是个很规整的证明，但我们想用另外的思路来考虑这个问题，给大家一点时间做一做，有没有想出更好的证明。这就是概率思维方式，我是想说明我们要证明这个东西，这是一个结果，好比这是一个要加密的东西，你要解开，办法是要编造出一个事件来，正好运算结果是它，反向思维是非常难的。二进制数是一个非常好的比喻，后面这些证明题都是类似的，要反推，这很难，如果想出来，这个证明会很短。



想一想这是一个小的班，其实选举制度也是这个样的，比方说这不是27人，是3亿人，选总统只要是符合条件的都能选。总统来指定内阁成员。这个等式有问题，没有考虑重复。
这个大家也想一个故事，比方说m是来自仪电的人，n是仪电之外的人，选出22个同学出来一共有多少种做法，可以有很多种组合加起来。 这个式子怎么证，大家可以试一下。比方说我们有21个同学，肯定能把大家组成一对一对的，然后你有多少种组法，右边的等式就是说挑一部分同学出来，也就是说一个同学被挑出来了，他的pair有(2n-1)种选法。这个pair就不能算在整个队伍里面的，所以选下一个pair，这就是挑出所有的pair的做法。上面这个等式你可以这样想，把所有的人都排好，算order，这是最大的一个数，假设你已经分好组了，应该有n个pair，这n个pair怎么排是无所谓的，在组里面那两个人的位置也是无所谓的，每一个都在除以2，才可以证明这个东西一样。

大家想一想这个问题，任务是要把所有糖分完这个问题是有order的。不是只分成三组，给谁是重要的。如果分拆的话很复杂。13个糖有14个位置，分两种情况，一种是中间的人没糖，第二种情况是中间的人有糖。14C2 + 14C1，算出来是105. 我来说另一种解法，这就变成把这个问题二进制编码了，一共有15位，里面有两个一，你要找两个一,就是15C2，一共105，一样的，你在15个位置里面找1的位置。要是拆开求和就太复杂了。这就是把图填满了。

相同生日概率，我们刚刚开始上课的时候，房间里有两个人生日相同的概率超过50%，有多少人以上肯定会有相同生日，365以上，这个问题我们简化一下，不去考虑闰年，另外就是认为所有人的生日是均匀分布的，你出生在任何一天都是有可能的，其实不是这样的，节日之后出生的概率很高，然后大概多少人可以到90%以上，其实就像一个泊松分布一样，大家可以算一算，回来我们讨论一下。



 每个小孩都有糖，就是不能有小孩没有糖有多少种分法，我们想三个小孩分6个糖，我们标记一下位置，有8个位置，我把分隔符画点，就能把他们分开，就代表第一个小孩拿两个，第二个小孩拿一个，然后第三个小孩拿三个。不管我怎么折腾，一共8个东西，我要在8个空间里面选两个位置来点点，剩下的填上圈，这个可以理解把。

相同生日概率，我们是27个人，当你有27个人的时候，你会有多大的概率，60%，我们这个班里面有60%的概率两个同学的生日在同一天，这个概率其实挺高的。怎么算，我们现在已经有一个解了，然后看code,把公式写出来。这个是连乘，我们来解释一下这个operation，大家想一想。这个公式写出来是这样的，底下是365的k次方，上面是一个连乘，365的连乘，怎么解释他，假设这里面没有兄弟姐妹，双胞胎。假设没有这种关系，也没有2月29号这样的生日，每个人都有365个可能,如果你不想让他重复，第一个人随便选一个人，第二个人就不能是这个数，以此类推。我们就把这个题给解了，我们再往下算一下，看看到99应该是多少，我们把参数调一下，你们猜一下会有多少人。



58位， 条件概率，我刚才写的A并B也能简写成AB，大家做一个贝叶斯的题，s代表垃圾，F就是转发，这个文章里面出现转发他是垃圾的概率是多少，然后根据条件概率，分母是，分母是两种情况，转发的两种情况，要么是垃圾20%，不是垃圾出现转发是1%，把这个换一下发现是一样的。这个是垃圾的概率是0.8，算一下这个值，应该是个很大的数，98%。

下面讲讲采样和分布，中心极限定理，这个特别有用，这个定律极大地简化了工作，为什么要选正态分布，因为选了选了各种各样的参数，各种event，假设你选的feature有足够好的独立性的话，不管分布是什么，最后加起来结果趋近于这个分布，选的越多越正确。这是一个非常好的定理，加大简化了我们基于统计，机器学习算法。我们试一下，numpy也有分布，他是放的随机数生成器，另外个办法是Scipy的库，跟我们观察的印象里很像。

回到刚才1,2,3sigma，置信区间的概念，中间红色的线是期望，旁边这两个紫色的线应该是2sigma,对应的是95，中间画的这一条，95%的样本都是落在这个范围，N是试验次数。
这个我直接把0.95画出来，刚才是根据规律找出来的2sigma，我们选随机数。均值的意思就是说总体评价是好，大于0，总体评价是差，小于0.我们看如果是差的话是不是在置信区间里面。过程就是你先做一个假设，差，然后搞一个置信度，画的红线是90%，然后画一个线不在范围之内，假设失败。这个你只做了一边的假设，你还能做两边的假设。就好像现在有一些数值，你要得到一个定性的结论，通常是个布尔，好或者坏，有个sentiment还是一个表达情绪的人，你需要对你的结论有个可信的范围，误差是多少，先设好假设，然后根据分布，得到结论。




