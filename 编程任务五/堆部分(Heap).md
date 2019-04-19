# 堆部分(Heap)

## 使用vector构建堆
```
// 构建堆heap

template<class T>
class Heap
{
	//建堆
	Heap(const T* a, int sz)
	{
		_a.resize(sz);
		for(int i = 0; i<sz; i++)
		{
			_a[i] = a[i];

		}
		for(int i =(_a.size() - 2)/2;i>=0;i--)
			/*外层循环，每次传入根结点下标。
		（_a.size()-2）/2即为最后一个非叶子结点下标。*/
		{
			AdjustDown(i);
		}

	}
protected:
	//向下调整
	void AdjustDown(int root)
	{
		int parent = root;
		size_t child = parent*2+1;
		while(child<_a.size())
		{
			if(child+1<_a.size() && _a[child+1]>_a.[child])
				child++;
			if(_a[child]>_a[parent])
			{
				swap(_a[child],_a[parent]);
				parent = child;
				child = parent*2 + 1;

			}
			else
				break;
		}
	}

	void AdjustUp(int root)
	{
		int child = root;
		int parent = (root-1)/2 ;
		
		while(child>0)
		{
			if(!(_a[child]<_a[parent]))
			{
				swap(_a[child],_a[parent]);
				child = parent;
				parent = (child-1)/2;

			}
			else
			{
				break;
			}
		}
	}

	void Push(const T& x)//插入，插入到数组最后，然后针对该节点进行一次向上处理

	{
		_a.push_back(x);
		AdjustUp(_a.size() - 1);


	}

	void Pop() //删除根节点
	{
		assert(!_a.empty());
		swap(_a[0],_a[_a.size() - 1]);
		_a.pop_back();
		AdjustDown(0);


	}


protected:
	vector<T> _a;;// 用vector代替一个数组
}
```
## 堆排序
```
/* heap sort 主函数
 */
void heap_sort(int heap[], int heap_size)
{
  	if (heap == NULL || heap_size < 2)
  	{
    	return;
  	}
  //构建最大堆
 	 build_max_heap(heap, heap_size);
  
  	int i;
  	for (i = heap_size - 1; i > 0; i--)
  	{
    /* 把当前树的根节点交换到末尾
     * 相当于取出最大值，树的规模变小。
     * 交换后的树不是最大堆，但是根的两颗子树依然是最大堆
     * 满足调用max_heapify的条件。之所以这样交换，
     * 是因为用max_heapify处理时间复杂度较低，
     * 如果不交换而直接"取出"heap[0], 此处可能要使用
     * build_max_heap重新建立最大堆，时间复杂度较大
     */
   	 	swap_val(heap[0], heap + i);
  	
    	heap_size--;
    	//维护最大堆
    	max_heapify(heap, heap_size, 0);
  	}
}
```
## 优先队列python
```
# PriorityQueue

class PriorityQueue:
    _arr=[]
    _index=-1
    def __init__(self,arr=[]):
        self._arr=arr
        self._index=len(self._arr)-1#指向最后一个元素
        self.firstBuildHeap()
                        #index代表要进行向下调整的结点
    def buildHeap(self,index,_arr):
        if self._index==-1:    #如果堆里没有原始 则返回
            return
        temp=_arr[index]#temp代表index下标的值
        k=(index*2)+1  #k代表index的左子树
        lenth=len(_arr)-1
        while k<=lenth:
            if  k<lenth and _arr[k]<_arr[k+1] :#如果k的左子树小于length（也就是k还有右子树）并且它的右子树大于它
                k+=1    #k++    k指向了右子树
            if _arr[k]<temp:    #如果temp大于当前子树的最大值（无论左子树还是右子树都大于，因为上个判断已经判断了左右子树大小)
                break           #直接返回
            _arr[index]=_arr[k]    #如果temp不大于左子树或者右子树的值  将K结点（index子树）的值赋给inedx结点值
            index=k                #要调整的结点变为K 因为index结点已经判断完了
            k=(k*2)+1              #K变成index的左子树

        _arr[index]=temp        #如果循环结束，说明调整完毕，最后index的值是将是它的子树的值，需要修改为value也就是temp的值
    def firstBuildHeap(self):
        index=(len(self._arr)//2)-1
        while index>=0:
            self.buildHeap(index,self._arr)
            index-=1
    def get_arr(self):
        return self._arr

    def getMax(self):
        if self._index == -1:   #如果_index为-1  则堆为空
            return
        self.__swap(0,self._index,self._arr)#不然交换堆顶元素和最后的元素
        maxValue=self._arr[self._index]  #交换后取得最后一个元素
        self.__remove()     #删除最后一个元素
        return maxValue     #返回最大值

    def __remove(self):
        if self._index==-1: #如果_index为-1  则堆为空
            return
        self._arr.pop() #删除最后一个元素
        self._index-=1
        self.buildHeap(0,self._arr)#因为目前堆顶元素是未知的，所以要进行一次调整
        return

    def insert(self,value):
        self._arr.append(value) #将新值插入到堆尾
        self._index += 1        #index++ index代表了value的下标
        index=self._index
        if index % 2 == 0:
            parent = index // 2 - 1
        else:
            parent = index // 2 #获取index的父节点
        temp=self._arr[index]   #获取value的值

        #上滤
        while parent>=0:           #如果没超过根节点  也就是index的父节点最大只能为0号下标
            if   temp<self._arr[parent]:    #如果下标index的值也就是value小于它的父节点，没破坏堆序性
                break
            #print(index,parent)
            self._arr[index] = self._arr[parent]#不然的话将它的父节点的值赋给index
            index=parent        #index的父节点成为新的待调整结点
            if index%2==0:
                parent = index // 2-1
            else:
                parent=index//2#取得新index的父节点
        self._arr[index]=temp#循环结束后将temp也就是value的值给最后停下来的index
        return
    def __swap(self,i,j,arr):
        k=arr[i]
        arr[i]=arr[j]
        arr[j]=k

```