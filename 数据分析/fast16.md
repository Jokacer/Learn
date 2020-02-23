1. 闪存驱动器所经历的不同类型的错误及其在该领域的频率(第3节)
2. 原始误码率（RBER）受到的影响以及与其他错误的关系（section 4）
3. 不可纠正错误，频率以及受到的影响（section 5）
4. 不同类型硬件故障特征（section 6）
5. 不同闪存技术的可靠性比较(MLC eMLC SLC)(section 7)
6. 闪存驱动器和硬盘驱动器的比较（section8）

同代驱动模式之间主要区别是芯片类型不同，使用的驱动程序和固件相同，使用相同的ECC来进行检测纠错。
收集的数据为每个驱动器在字段中的每天在该领域中的数据，除了统计不同类型的错误还包括每天的工作负载统计：读写和擦除数量，还有一个日志用于记录何时芯片声明failed何时被用于交换修复

从不同错误类型频率的baseline统计数据开始，区分透明类型错误和非透明类型错误，透明错误类型如下：
1. 可纠正错误(Correctable error):在读操作期间由ECC检测并纠正错误
2. 读错误(read error):在读操作期间经历一个非ecc错误但在重试后成功
3. 写错误(write error):写操作经历一个错误但在重试后成功
4. 擦除错误(erase error):在一个块上擦除失败

不透明错误如下：
1. 不可纠正错误(Uncorrectable error):读操作的损坏位比ecc可纠正的要多
2. Final read error:读操作发生的错误在重试后依然错误
3. Final write error:写操作发生的错误在重试后依然错误
4. Meta Error:驱动器元数据错误
5. Timeout error:操作超时3秒

最常见的non-transparent error是final read errors，由模型可看出20%-63%的驱动会出现至少一次该错误，每1000天会有2-6天受到该错误影响，相对而言final write errors是发生频率都会小得多，大约1.5%-2.5%的驱动、10000天内有1-4天发生这种错误，这种差别的原因可能因为写失败后悔尝试在其他位置再写，因此相比于final read errors是由于一小部分相关存储区域的损坏而言，final write errors表明有更大规模的硬件问题

raw bit error rate(RBER):作为闪存可靠性的标准，定义为每次读取比特数量中损坏的比特数量(包括可纠正的损坏和不可纠正的损坏)，第二代驱动器可产生精确的数量。第一代只会给出损坏数最多的chunk中的损坏数。

workload里其主要作用的是保留错误，而读打扰错误却微乎其微

UBER(Uncorrectable bit errors rate):衡量uncorrectable errors的标准，定义为不可纠正的比特错误占总的读取比特数，然而这不是一个有意义的度量标准，毕竟UEs与读计数无关