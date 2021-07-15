# 答题页



### 数据设计

```go
// 题目json数据 45道——45条数据
type Answer struct { //试题
	Id      int
	Type    string   `bson:"type"`
	Topic   string   `bson:"topic"`   //试题题目
	Img     string   `bson:"img"`     //试题图片
	Options []Option `bson:"options"` //试题选项
	Score   int      `bson:"score"`   //试题分数
}

type Option struct {
	context     string `bson:"context"`
	contextType string `bson:"context_type"`
	isRight     bool   `bson:"is_right"`
}


type ExamPaper struct { //试卷
	Id       int        `bson:"id"`
	Type     string     `bson:"type"`
	Question []Question `bson:"answers"` //试题
}

type AnswerPaper struct { //答卷
	Id     int          `bson:"id"`
	Mid    int          `bson:"mid"`
	Did    int          `bson:"did"`
	Eid    int          `bson:"eid"`
	Type   string       `bson:"type"`
	Answer []UserAnswer `bson:"answer"` //答题
	Status int          `bson:"status"` //答题状态  0答题中  1完成答题  2未完成答题
	Score  int          `bson:"score"`  //试卷分数
}

type UserAnswer struct {
	AnswerId    int      `bson:"answer_id"`
	UserAnswers string   `bson:"userAnswers"` //用户答案
	Result      bool     `bson:"result"`       //题目结果  ture/false
}


//request试题  ===》 response试题 20道
db.answer.aggregate( [ { $sample: { size: 20 } } ] ) //从db中随机获取20道

type GetExamParam struct {
	Mid  int    `json:"mid"`
	Did  int    `json:"did"`
	Type string `json:"type"`
}

type SubmitAnswerParam struct {
	Mid           int    `json:"mid"`
	Did           int    `json:"did"`
	Type          string `json:"type"`
	ExamPaperId   int    `json:"exam_paper_id"`   //试卷id
	AnswerPaperId int    `json:"answer_paper_id"` //答卷id
	Num           int    `json:"num"`             //题号
	UserAnswer    string `json:"user_answer"`     //答案
}


//response
type GetExamData struct {
	Type      string    `json:"type"`
	ExamPaper ExamPaper `json:"exam_paper"` //试卷
	PaperId   int       `json:"paper_id"`   //答卷id
	Num       int       `json:"num"`        //第几题
}

type SubmitAnswerData struct {
	Result     bool `json:"result"`      //答题结果
	PaperId    int  `json:"paper_id"`    //试卷id
	NextNum    int  `json:"next_num"`    //下一道题
	Finish     bool `json:"finish"`      //是否完成答题
	TotalScore int  `json:"total_score"` //答题后总分
}



//request（用户id，分数，定位位置） ===》  response结果
type AnswerResult struct { 
	Uid          string `bson:"uid"`
	IntoVillage  bool   `bson:"into_village"`  //是否进村
	Score        int    `bson:"score"`         //成绩
	Achievement  string `bson:"achievement"`   //称号
	IsPosition   bool   `bson:"is_position"`   //是否开启定位
	Remind       string `bson:"remind"`        //提醒
	LicensePlate string `bson:"license_plate"` //车牌
	Guide        string `bson:"guide"`		     //引导文案
}
```

1. 答题页请求，返回ExamPaper数据

2. 答题结束，请求参数uid，分数及定位位置

3. 返回答题结果

   判断是否通过，不通过返回不通过（数据不写入数据库内）

   判断是否开启定位，未开启定位则提示开启定位才能获取车牌

   获取车牌，返回成功入村提示，点击按钮即可入村