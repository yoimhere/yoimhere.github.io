---
layout: post
title: static函数的小技巧
description:  在iOS开发中,如果我们使用比较底层的Api框架时经常需要传入static函数作为回调来处理结果,但是这个static函数有个小技巧,相信很多人都没注意到.
categories: iOS，小技巧
tags: 小技巧

---
### 前言

在iOS开发中,如果我们使用比较底层的Api框架时经常需要传入static函数作为回调来处理结果,但是这个static函数有个小技巧,相信很多人都没注意到.

### 举个栗子

```
static void kHandleInputBuffer (
                                void *client,              
                                AudioQueueRefinAQ,               
                                AudioQueueBufferRef    inBuffer,            
                                const AudioTimeStamp    *inStartTime,       
                                UInt32 inNumPackets,        
                                const AudioStreamPacketDescription *desc){
    ZJAudioManager *audioManager = (__bridge ZJAudioManager *) client;
    [audioManager handlerSomeThing]; //报错
}

@implementation ZJAudioManager

    - (void)start
     {
	       AudioQueueNewInput(&.mDataFormat,
	                      kHandleInputBuffer,
	                      (__bridge void *)(self),   
	                      NULL, 
	                      NULL, 
	                      0, 
	                     &mQueue);
	   }
	   
	//未暴露给外部
    - (void)handlerSomeThing
     {
        //code
     }
@end
```

### 解决办法

1.使用performSelector

```
1if ([self    respondsToSelector:@selector(handlerSomeThing)]) {
         [self performSelector:@selector(handlerSomeThing)]
    }
``` 

2.把handlerSomeThing方法暴露出去

>以上的方法在针对少数的类似情况还是可以的，但是还是有缺点的:
>1.@selector(handlerSomeThing) 如果handlerSomeThing方法名改动容易出错.
>2.暴露的情况的话，会造成不必要的过多方法在外,下面的是一种比较有效的小技巧,未暴露Method,Property都可以访问到.

#### 正确小技巧

```
@implementation ZJAudioManager
    static void kHandleInputBuffer (
                                void *client,              
                                AudioQueueRefinAQ,               
                                AudioQueueBufferRef        inBuffer,            
                                const AudioTimeStamp        *inStartTime,       
                                UInt32 inNumPackets,        
                                const AudioStreamPacketDescription *desc){
        ZJAudioManager *audioManager = (__bridge ZJAudioManager *) client;
        [audioManager handlerSomeThing]; //搞定收工
    }
    
    - (void)start
     {
           AudioQueueNewInput(&.mDataFormat,
                          kHandleInputBuffer,
                          (__bridge void *)(self),
                          NULL,
                          NULL,
                          0,
                         &mQueue);
      }
	   
	//未暴露给外部
    - (void)handlerSomeThing
     {
        //code
     }
@end
```

