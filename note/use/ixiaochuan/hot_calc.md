## model

PostSimpItem. 帖子基本信息

PostScoreItem 帖子分数信息

score = up（顶） + 4*reviews（评论） - down（踩）



## task

HotCalc 热门计算   ===》 CalcEveryDuration 计算每个持续时间





## Business

**CalcEveryDuration**

===》 

- 获取热门帖子主题ids
  1. 通过热门主题id获取帖子id及分区分数postScoresPartion
  2. 通过pids获取帖子基本信息result
  3. pids及scores为result中的Id和计算score结果
  4. 哈希获取热门帖子基本信息（通过tid及pids）  oldItems
  5. scores -= oldItems中每个计算出的score结果
  6. 将postScoresPartion中Score更新为scores中score
  7. 将Item其添加到PostScoreAry中，如果score大于0 则 activedCount++
  8. 哈希设置热门帖子基本信息（tid及result）
  9. ===》LRU（tid，activedCount，postScoreAry）



**LRU**

1. 将postScoreAry通过oldScore进行排序
2. activedScoreBegin = len(postScoreAry) - activedCount
3. 对postScoreAry中每个item
   - score > 0 ? score+=activedScoreBegin : score = activedScoreBegin - i
4. ===》 TopicReplaceByReCalcSet（tid）



## dao













