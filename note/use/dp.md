改leetcode 1659



有一个矩形区域放满气球，小右有两把枪，一把狙击枪，一把手枪，小右如果使用狙击枪命中一个气球可以得到100分，使用手枪命中气球可以得到50分，假设小右是个神枪手，可以做到百发百中，因此商家给小右做了这么几个限定条件

1. 如果狙击枪命中的气球旁边每有一个气球被打爆的话，则这个气球减20分，
2. 如果手枪命中的气球旁边每有一个气球被打爆的话，则这个气球加15分

旁边指相邻，即上下左右相邻得格子

给定矩形区域的大小及狙击枪和手枪各自的子弹数量，问小右如何打才能使自己获取最大的分数（注意：子弹不一定必须打完）



示例1:

<img src="https://img-blog.csdnimg.cn/20210707144010970.jpg" alt="得分情况" width="30%" style="float:left;" />

```
输入：m=2    n=3    superBullet=1   bullet=2
输出：230
解释：狙击枪打（1, 1），手枪打（1, 3）和（2, 3）

		（1，1）得分：100   - （0*20）= 100
		（1，3）得分：50 + （1*15）= 65
		（2，3）得分：50 + （1*15）= 65
		
	最终得分：100+65+65 = 230
```

示例2:

```
输入：m=3   n=1		superBullet=2   bullet=1
输出：240
解释：狙击枪打（1, 1）和（3, 1），手枪打（2, 1）

		（1，1）得分：100 - （1*20）= 80
		（2，1）得分：50 + （2*15）= 80
		（3，1）得分：100 - （1*20）= 80
		
	最终得分：80+80+80 = 240
```

示例3:

```
输入：m=2   n=2		superBullet=4   bullet=0
输出：240
```

```go
var (
	MAXN = 5
	pow  []int
	cnts [][]int
	s1   = []int{0, 100, 50}
	s2   = [][]int{
		{0, 0, 0},
		{0, -40, -5},
		{0, -5, 30},
	}

	ss1 []int
	ss2 [][]int
)

func ls(x, y int) int {
	return x * pow[y]
}

func rs(x, y int) int {
	return x / pow[y]
}

func tl(x int) int {
	return x % 3
}

func cr(x, n int) int {
	sum := 0
	p, t := -1, 0
	for i := 0; i < n; i++ {
		t = tl(x)
		sum += s1[t]
		if p != -1 {
			sum += s2[p][t]
		}
		p = t
		x = rs(x, 1)
	}
	return sum
}

func cc(x, y, n int) int {
	sum := 0
	for i := 0; i < n; i++ {
		sum += s2[tl(x)][tl(y)]
		x, y = rs(x, 1), rs(y, 1)
	}
	return sum
}

func valid(x, a, b int) bool {
	return cnts[x][0] <= a && cnts[x][1] <= b
}

func Init() {
	if len(pow) > 0 {
		return
	}
	pow = make([]int, MAXN+1)
	pow[0] = 1
	for i := 1; i <= MAXN; i++ {
		pow[i] = pow[i-1] * 3
	}

	mS := ls(1, MAXN)
	cnts = make([][]int, mS)
	for s := 0; s < mS; s++ {
		x := s
		cnt := []int{0, 0}
		for ; x > 0; x = rs(x, 1) {
			t := tl(x)
			if t > 0 {
				cnt[t-1]++
			}
		}
		cnts[s] = cnt
	}

	ss1 = make([]int, mS)
	ss2 = make([][]int, mS)
	for s := 0; s < mS; s++ {
		ss2[s] = make([]int, mS)
		ss1[s] = cr(s, MAXN)
	}

	for s1 := 0; s1 < mS; s1++ {
		for s2 := s1; s2 < mS; s2++ {
			ss2[s1][s2] = cc(s1, s2, MAXN)
			ss2[s2][s1] = ss2[s1][s2]
		}
	}
}

func getMaxScore(m int, n int, superBullet int, bullet int) int {
	Init()
	f := make([][][][]int, 2)
	l1, l2 := superBullet, bullet
	mS := ls(1, m)

	clearF := func(p int) {
		for i := 0; i < l1; i++ {
			for j := 0; j < l2; j++ {
				for s := 0; s < mS; s++ {
					f[p][i][j][s] = -1
				}
			}
		}
	}

	for p := 0; p < 2; p++ {
		f[p] = make([][][]int, l1+1)
		for i := 0; i <= l1; i++ {
			f[p][i] = make([][]int, l2+1)
			for j := 0; j <= l2; j++ {
				f[p][i][j] = make([]int, mS)
			}
		}
	}
	clearF(0)
	clearF(1)

	for i := 0; i <= l1; i++ {
		for j := 0; j <= l2; j++ {
			for s := 0; s < mS; s++ {
				if valid(s, i, j) {
					f[0][i][j][s] = cr(s, m)
				}
			}
		}
	}

	for p := 1; p < n; p++ {
		now, pre := p&1, (p&1)^1
		for i := 0; i <= l1; i++ {
			for j := 0; j <= l2; j++ {
				for s := 0; s < mS; s++ {
					if !valid(s, i, j) {
						continue
					}
					pi, pj := i-cnts[s][0], j-cnts[s][1]
					for ps := 0; ps < mS; ps++ {
						if f[pre][pi][pj][ps] == -1 {
							continue
						}
						tsum := f[pre][pi][pj][ps] + ss1[s] + ss2[s][ps]

						if f[now][i][j][s] < tsum {
							f[now][i][j][s] = tsum
						}
					}
				}
			}
		}
		clearF(pre)
	}

	now := (n - 1) & 1
	res := 0
	for i := 0; i <= l1; i++ {
		for j := 0; j <= l2; j++ {
			for s := 0; s < mS; s++ {
				if res < f[now][i][j][s] {
					res = f[now][i][j][s]
				}
			}
		}
	}

	return res
}
```

