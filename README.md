# data-analysis
data in python
	MT	maketime1	ability1	cost1	maketime2	ability2	cost2	maketime3	ability3	cost3	maketime4	ability4	cost4
1	6	60	5000	12	24	20000	9	36	8000	11	6	15000	10
2	24	66.5	10000	9	24	10000	10	48	13000	10	6	10000	10
3	12	58	3000	11	24	3000	12	56	9000	12	6	8000	11
4	24	49.5	6000	10	24	6000	11	30	10000	11	6	7000	11
5	12	60	2000	11	24	0	0	0	0	0	0	0	0
6	24	60	9000	11	24	0	0	0	0	0	0	0	0
Command Mode (press Esc to enable)
F
: find and replace
Ctrl-Shift-F
: open the command palette
Ctrl-Shift-P
: open the command palette
Enter
: enter edit mode
P
: open the command palette
Shift-Enter
: run cell, select below
Ctrl-Enter
: run selected cells
Alt-Enter
: run cell and insert below
Y
: change cell to code
M
: change cell to markdown
R
: change cell to raw
1
: change cell to heading 1
2
: change cell to heading 2
3
: change cell to heading 3
4
: change cell to heading 4
5
: change cell to heading 5
6
: change cell to heading 6
K
: select cell above
Up
: select cell above
Down
: select cell below
J
: select cell below
Shift-K
: extend selected cells above
Shift-Up
: extend selected cells above
Shift-Down
: extend selected cells below
Shift-J
: extend selected cells below
A
: insert cell above
B
: insert cell below
X
: cut selected cells
C
: copy selected cells
Shift-V
: paste cells above
V
: paste cells below
Z
: undo cell deletion
D,D
: delete selected cells
Shift-M
: merge selected cells, or current cell with cell below if only one cell is selected
Ctrl-S
: Save and Checkpoint
S
: Save and Checkpoint
L
: toggle line numbers
O
: toggle output of selected cells
Shift-O
: toggle output scrolling of selected cells
H
: show keyboard shortcuts
I,I
: interrupt the kernel
0,0
: restart the kernel (with dialog)
Esc
: close the pager
Q
: close the pager
Shift-L
: toggles line numbers in all cells, and persist the setting
Shift-Space
: scroll notebook up
Space
: scroll notebook down
Edit Mode (press Enter to enable)
Tab
: code completion or indent
Shift-Tab
: tooltip
Ctrl-]
: indent
Ctrl-[
: dedent
Ctrl-A
: select all
Ctrl-Z
: undo
Ctrl-/
: comment
Ctrl-D
: delete whole line
Ctrl-U
: undo selection
Insert
: toggle overwrite flag
Ctrl-Home
: go to cell start
Ctrl-Up
: go to cell start
Ctrl-End
: go to cell end
Ctrl-Down
: go to cell end
Ctrl-Left
: go one word left
Ctrl-Right
: go one word right
Ctrl-Backspace
: delete word before
Ctrl-Delete
: delete word after
Ctrl-Y
: redo
Alt-U
: redo selection
Ctrl-M
: enter command mode
Ctrl-Shift-F
: open the command palette
Ctrl-Shift-P
: open the command palette
Esc
: enter command mode
Shift-Enter
: run cell, select below
Ctrl-Enter
: run selected cells
Alt-Enter
: run cell and insert below
Ctrl-Shift-Minus
: split cell at cursor
Ctrl-S
: Save and Checkpoint
Down
: move cursor down
Up
: move cursor up
#####
# SciPy Linear Algebra Library
S1=[]
S2=[]
S3=[]
listcolumn=data1.columns
for name1 in listcolumn:
    length=len(data1.columns)
#A = data1.corr()
#L = scipy.linalg.cholesky(A, lower=True)
#U = scipy.linalg.cholesky(A, lower=False)
    s=[]
    s1=[]
    s2=[]
    for i in range(1000):
        b=0
        matrixfinal=np.random.normal(loc=100, scale=1, size=250).reshape(250,1)
        for name in data1.columns:
            #a=np.random.normal(loc=data1[name].mean(), scale=data1[name].std(), size=250)
            a=stock_monte_carlo(data1.loc['2017-09-01'][name],250,data1[name].pct_change(1).mean(),data1[name].pct_change(1).std())
            b=b+a[0]*C[name]/100
            matrixfinal=np.hstack((matrixfinal,a.reshape(250,1)))
        matrixfinal=np.delete(matrixfinal,0,axis=1)
        data3=pd.DataFrame(matrixfinal)
#data3=pd.DataFrame(matrixfinal.dot(U/np.abs(U.sum(0))))
#data3.drop([0],axis=1,inplace=True)
        data3.columns=data1.columns#获取模拟数据
        data3['combineindex']=data3.sum(axis=1)
        yearincomerate=((data3.loc[249]['combineindex']+b)/data3.loc[0]['combineindex'])**(250/data3['combineindex'].count())-1
        varofincomerate=data3['combineindex'].pct_change(1).std()*np.sqrt(250)#收益波动率
        sharpratio=(yearincomerate-0.015)/varofincomerate#
        sharpratio1=(yearincomerate-0.015)/(data3['combineindex'].pct_change(1).cumsum().std()*np.sqrt(250))
        sharpratio2=(yearincomerate-0.015)/(data3['combineindex'].std()*np.sqrt(250))
        s.append(sharpratio)
        s1.append(sharpratio1)
        s2.append(sharpratio2)
    S1.append(np.mean(s))
    S2.append(np.mean(s1))
    S3.append(np.mean(s2))
    data1.drop(name1,axis=1,inplace=True)
#####获取票息数据
C={}
for num in c.columns:
    datalilv1=w.wsd( num, "couponrate2", "2017-09-01","2018-09-01","credibility=1")
    C[num]=np.mean(datalilv1.Data[0])
######
datalilv=w.wsd("011801582.IB", "net_cnbd", "2017-09-01", "2018-09-01", "credibility=1")
c=pd.DataFrame([datalilv.Times,datalilv.Data[0]]).T
c.columns=['date','101351029.IB']
c.index=pd.to_datetime(c.date)
c.drop(['date'],axis=1,inplace=True)
####
import random
list1=set(data[data['债券等级']=='AAA']['债券代码'])
#[random.randrange(1000) for i in range(100)]
list2=random.sample(list1, 120)
