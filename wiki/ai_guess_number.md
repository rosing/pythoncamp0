#猜数字AI

###作业要求  

    + 猜数游戏AI版
- 期待:
    + 抽象你的自然思维
    + 在尽可能短的代码行数中完成:无人介入的猜数游戏
    + 最好能动画式演示游戏过程
- 要求:
    + 基础: 用程序模拟出自己猜数的策略, 并进行检验
    + 可用: 用自制的猜数AI, 和自己的游戏对战
    + 合格: 猜数AI的游戏过程,可记录,可回放
    + 天才: 猜数AI的游戏过程,可记录,可回放,可分享,加载...进一步的:
        * 通过大量的游戏对战,统计自个儿AI 的能力?! 
        * 发布他人的AI 也可以接入的服务?
        * 并行多组游戏?
        * 怎么证明自个儿的 AI 策略是最优的?能用最少次数猜中?
- 教程期待:
    + 向 6个月 前看过以往自己教程的自己认真描述
    + 怎么设计代码来减少行数完成这个任务?
    + 有哪些理解上的坑,如何能理解之?


###思考步骤

- 实现功能 
  + 用户输入0~1000的数，用于检测AI
  + 提供两种不同AI算法
  + 输出对象化
  + 全部于画布上输出  
   	 + 输出每一步运算
   	 + 输出两种算法的过程
   	 + 统计不同算法所需的步骤数，并由此判断算法策略的优劣
 
- 小模块功能
  + DrawText类：用于绘制相关list指定的文本，每一个元素占一行。
    可外部修改list。调用draw方法绘制，并返回当前最后一个元素坐标值，用于下一个对象输出。
  + is_int函数：用于验证输入是否为正整数
  + review_handler用于回顾，回顾的时间间隔由timer设定
  + 设置一个按钮，其功能等同于input后回车输出。此按钮的重要意义在于可让用户不用回车而是点击按钮确定，优化用户体验。  
   
- 关键语法：
  + all _is_int = all(c in "0123456789" for c in txt)
  + list的切片 list[n,m]
   
- **尚未实现的功能**   
   并行多组游戏猜不同的数（本版本尚未实现） 
  
- 步骤
- 填坑  
  + 坑一：frame.add_button("回放"，handler)   
     * 提示：syntax error:invalid string(possibly contains a unicode character)
     * 原因是不支持中文
     * 解决方法：frame.add_button(u"回放"，handler) 
     * 不能直接对变量赋非unicode的值，s = u'数值'
     * 此方法在list.append,print 等处有效
     * 本地可以在文件头加上-\*- coding:utf-8 -*- 但codeskulptor无用
  + 坑二：出现猜重复的数字
  	 * 原因：使用random.randint得到的数字是包括两边的。
  	 * 解决办法：左边边界加1，右边界减1
  + 坑三：第一次回顾后，重新玩新游戏，还自个儿回顾。
     * 原因：没有停止timer
     * 解决办法：在猜数字开始的时候停止timer
   + 坑四（此坑未填）：canvas.draw_text(u'绘制中文'，[50,112], 48, "Red")
     - 报错：ValueError:text may not contain non-printing characters
     - 尝试：# -\*- coding:utf-8 -*- 没用。# coding=gbk也木有用。
     
      
   
###求解
  + 发布他人AI，可以接入的服务（完全不知道怎么理解）
  + 如何在canvas.draw_text内画出中文？ 
  + 为什么在其他的教程中会出现# coding=gbk，#号不是注释用的吗？为什么系统能读取后面的内容？还有什么是可以读的？