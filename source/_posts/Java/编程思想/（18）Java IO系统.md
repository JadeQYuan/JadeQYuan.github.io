title: Java I/O系统
description: Java I/O系统
categories: 
  - Java
  - 编程思想
author: Jade
date: 2021-12-27 10:00:00
---

{% markmap %}

## 18.0 序
- 对程序语言设计者来说，创建一个好的输入/输出（I/O）系统是一项艰难的任务。
- 不仅存在各种I/O源端和想要与之通信的接收端，而且还需要以多种不同的方式与它们进行通信。
- Java类库的设计者通过创建大量的类来解决这个难题。

## 18.1 File类
- File类既能代表一个特定文件的名称，又能代表一个目录下的一组文件的名称。
- FilenameFilter接口。策略模式。
- 程序设计中一项常见的任务就是在文件集上执行操作。这些文件要么在本地目录中，要么遍布整个目录树中。 -- 工具。
- 也可以用File对象来创建新的目录或尚不存在的整个目录路径。
- File类其它方法： canRead、canWrite、getName、getParent、getPath、renameTo、mkdirs。

## 18.2 输入和输出
- 编程语言的I/O类库中常使用流整个抽象概念，代表任何有能力产出数据的数据源对象或者是有能力接收数据的接收端对象。
- 流屏蔽了实际的I/O设备中处理数据的细节。
- Java类库中的I/O中分成输入和输出两部分。
- 任何自InputStream或Reader派生而来的类都含有read方法，用于读取单个字节或字节数组。
- 任何自OutputStream或Writer派生而来的类都含有write方法，用于写单个字节或字节数组。
- 很少使用单一的类来创建流对象，而是通过叠合多个对象来提供所期望的功能。 -- 装饰器设计模式。
- Java中流类库让人迷惑的主要原因就在于：创建但一个的结果流，却需要创建多个对象。

- Java 1.0中，限定与输入有关的类都应该从InputStream继承，与输出有关的类都应该从OutputStream继承。

- InputStream的作用是用来表示那些从不同数据源产生输入的类。
- 数据源包括 1. 字节数组（ByteArrayInputSteam）； 2. String对象（StringBufferInputSteam）； 3. 文件（FileInputSteam）； 4. 管道（PipedInputSteam）； 5. 流序列（SequenceInputStream）； 6. 其它数据源。
- FilterInputStream也属于一种InputStream，为装饰器类提供基类。把属性或有用的接口与输入流连接在一起。

- OutputStream类别的类巨顶了输出所要去往的目标。
- 目标包括 1. 字节数组（ByteArrayOutputSteam）； 2. 文件（FileOutputSteam）； 3. 管道（PipedOutputStream）。
- FilterOutputStream为装饰器类提供了一个基类，把属性或者有用的接口与输出流链接了起来。

## 18.3 添加属性和有用的接口
- Java I/O类库需要多种不同功能的组合。增加了代码的复杂性。

- FilterInputStream类能够完成两件完全不同的事情。DataInputStream允许读取不同的基本类型数据即String对象，其它类在内部修改InputSteam的行为方式。
- FilterInputStream类型：DataInputStream、BufferedInputStream、LineNumberInputStream、PushbackInputStream。
- FilterOutputStream类型：DataOutputStream、PrintStream、BufferedOutputStream。

## 18.4 Reader和Writer
- Java 1.1对基本的I/O流类库进行了重大的修改。
- Reader和Writer提供兼容Unicode与面向字符的I/O功能。
- Java 1.1 向InputStream和OutputStream继承层次结构中添加了一些新类。
- 适配器类：InputStreamReader可以把InputStream转换为Reader，OutputStreamWriter可以把OutStream转换为Writer。
- 设计Reader和Writer继承层次结构主要是为了国际化。

- Java 1.1类：Reader、Writer、FileReader、FileWriter、StringReader、StringWriter、CharArrayReader、CharArrayWriter、PipedReader、PipedWriter。
- StringBufferInputStream已弃用。

- Java 1.1类：FilterReader、FilterWriter、BufferedReader、BufferWriter、PrintWriter、LineNumberReader、StreamTokenizer、PushbackReader。
- LineNumberInputStream已弃用。

## 18.5 自我独立的类：RandomAccessFile
- RandomAccessFile适用于由大小已知的记录组成的文件。
- RandomAccessFile不是InputStream或者OutputStream继承层次结构中的一部分。
- RandomAccessFile与拥有和别的I/O类型本质不同的行为，可以在一个文件内向前或向后移动。
- 只有RandomAccessFile支持搜寻方法，并且只适用于文件。
- 在JDK 1.4中，RandomAccessFile的大多数功能由nio存储映射文件所取代。

## 18.6 I/O流的典型使用方式
- 缓冲输入文件： new BufferedReader(new FileReader(filename));。
- 从内存输入： new StringReader(BufferedInputFile.read(string));。
- 格式化的内存输入： new DataInputStream(new ByteArrayInputStream(BufferedInputFile.read(string).getBytes()));。
- 基本的文件输出： new PrintWriter(new BufferedWriter(new FileWriter(filename)));。PrintWriter。
- 存储和恢复数据： DataInputStream、DataOutStream。要么为文件中的数据采用固定的格式，要么将额外的信息保存到文件中。
- 读写随机访问文件： RandomAccessFile。
- 管道流： 用于任务之间的通信。

## 18.7 文件读写的实用工具
- 一个很常见的程序化任务就是读取文件到内存，修改，然后再写出。

## 18.8 标准I/O
- 标准I/O这个术语参考的Unix中“程序所使用的单一信息流”这个概念。标准输入、标准输出、标准错误。
- 标准I/O的意义在于：可以很容易把程序串联起来，一个程序的标准输出可以成为另一程序的标准输入。

- 按照标准I/O模型，Java提供了System.in、System.out、System.err。
- System.out、System.err已经事先被包装成了PrintWriter对象。System.in是一个未经包装的InputStream，读取之前必须包装。

- Java的System类提供了一些简单的静态方法调用，以允许对标准输入、输出和错误I/O流进行重定向。setIn、setOut、setErr。
- I/O重定向操纵的是字节流，而不是字符流。

## 18.9 进程控制
- Java类库提供了在Java内部执行其他操作系统的程序，并且控制这些程序的输入和输出的类。ProcessBuilder、Process。

## 18.10 新I/O
- JDK 1.4的java.nio.\*包中引入了新的Java I/O类库，其目的在于提高速度。
- 实际上，旧的I/O包已经使用nio重新实现过，以便充分利用这种速度提高。
- 速度的提高来自于所使用的结构更接近于操作系统执行的I/O的方式：通道和缓冲器。
- 并没有直接和通道交互，只是和缓冲器交互，并把缓冲器派送到通道。通道要么从缓冲器获得数据，要么向缓冲器发送数据。
- 唯一直接与通道交互的缓冲器是ByteBuffer。可以存储未加工字节的缓冲器。
- 使用wrap方法将已存在的字节数组包装到ByteBuffer中。 -- 数组支持的ByteBuffer。
- 对于只读访问，必须显式使用allocate方法来分配ByteBuffer。allocateDirect产生一个与操作系统有更高耦合的直接缓冲器。
- 一旦调用read存储字节，就必须调用缓冲器上的flip，做好读取字节的准备。
- 如果打算使用缓冲器执行进一步的read操作，必须得调用clear来为read做好准备。
- transferTo、transferFrom允许一个通道和另一个通道直接相连。

- ByteBuffer可以看作是具有asCharBuffer方法的CharBuffer。
- 缓冲器容纳的是普通字节，为了转换成字符，要么在输入时进行编码，要么在输出时进行解码。
- java.nio.charset.Charset类提供了把数据编码成多种不同类型的字符集的工具。

- ByteBuffer只能保存字节类型的数据，但是具有从其所容纳的字节中产生出各种不同基本类型值的方法。

- 视图缓冲器通过某个特定的基本数据类型的视窗查看其底层的ByteBuffer。
- ByteBuffer依然是实际存储数据的地方，对视图的修改都会映射成对ByteBuffer中数据的修改。
- ByteBuffer是以高位优先的形式存储数据的。

- ByteBuffer是将数据移进移出通道的唯一方式，并且只能创建一个独立的基本类型缓冲器，或者使用as方法从ByteBuffer中获得。

- Buffer由数据和可以高效地访问即操作这些数据的四个索引组成。索引是：mark、position、limit、capacity。

- 内存映射文件允许创建和修改因为太大而不能放入内存的文件。
- MappedByteBuffer是一种特殊类型的直接缓冲器。
- MappedByteBuffer由ByteBuffer继承而来。

- JDK 1.4 引入了文件枷锁机制，允许同步访问某个作为共享资源的文件。
- 文件锁对其他的操作系统进程是可见的，因为Java的文件加锁直接映射到了本地操作系统的加锁工具。
- 如果由Java虚拟机，它会自动释放锁，或者关闭加锁的通道。也可以显式释放锁。

## 18.11 压缩
- Java I/O类库中的类支持读写压缩格式的数据流。
- 压缩类库是按字节方式而不是字符方式处理的。
- 压缩类：CheckedInputStream、CheckedOutputStream、DeflaterOutputStream、ZipOutputStream、GZIPOutputSteam、InflaterInputStream、ZipInputStream、GZIPInputStream。
- 支持Zip格式的Java库更加全面。
- Zip格式也被应用于JAR文件格式中。
- 一个JAR文件由一组压缩文件构成，同时还有一张描述了所有这些文件的文件清单。
- Sun的JDK自带的jar程序可根据选择自动压缩文件。
- jar工具的功能没有zip工具那么强大。

## 18.12 对象序列化
- Java的对象序列化将那些实现了Serializable接口的对象转换成一个字节序列，并能够在以后将这个字节序列完全恢复为原来的对象。
- 利用序列化可以实现轻量级持久化。
- 对象序列化的概念加入到语言是为了支持两种主要特性。 1. 远程方法调用RMI； 2. 对JavaBeans来说，对象的序列化是必需的。

- 反序列化，必须保证Java虚拟机能找到相关的.class文件。

- 通过实现Externalizable接口，代替实现Serializable接口，来对序列化过程进行控制。
- Externalizable接口继承了Serializable接口，同时增添了两个方法：writeExternal、readExternal。
- 用transient关键字关闭序列化。
- 可以实现Serializable接口，并添加（而非覆盖或实现）writeObject和readObject的方法。
- Java的版本控制机制过于简单，因而不能在任何场合都可靠运转，尤其是对JavaBeans更是如此。

## 18.13 XML
- 对象序列化的一个重要限制是它只是Java的解决方案：只有Java程序才能反序列化这种对象。
- 一种更具互操作性的解决方案是将数据转换为XML格式，这可以是其被各种各样的平台和语言使用。
- 用XML编程时的各种选择不胜枚举，包括随JDK发布的javax.xml.*类库。

## 18.14 Preferences
- Preferences API与对象序列化相比，前者与对象持久化更密切，因为它可以自动存储和读取信息。
- Preferences API用于存储和读取用户的偏好以及程序配置项的设置。
- Preferences是一个键值集合，存储在一个节点层级结构中。

## 18.15 总结
- 一旦理解了装饰器模式，并开始在某些情况下使用该类库以利用其提供的灵活性，那就开始从这个设计中受益了。

{% endmarkmap %}