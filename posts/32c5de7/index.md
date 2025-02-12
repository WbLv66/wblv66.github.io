# 基于搜索的路径规划


&lt;!--more--&gt;

{{&lt; figure src=&#34;https://cdn.pixabay.com/photo/2024/05/09/08/07/ai-generated-8750163_1280.jpg&#34;&gt;}}

# 基于搜索的路径规划

算法流程：

- 维护一个容器用来存储待访问的节点；维护一个数组用来标记已访问的节点；维护一个数组用来标记父节点
- 进行初始化
- 循环遍历容器：
  - 按照预设规则弹出容器中的节点，将这个节点标记为已访问
  - 如果弹出的节点是终点，则证明找出路径，结束
  - 扩展邻居节点
  - 将未访问过且非障碍物的节点按着某种顺序放入容器中，记录父节点
- 结束
## 1. 广度优先与深度优先

### 1.1 广度优先(BFS)

广度优先算法使用的容器为**队列(queue)**，遵循的规则是**先进先出**。

{{&lt; figure src=&#34;基于搜索的路径规划/queue.png&#34; caption=&#34;queue&#34;height=&#34;400&#34; width=&#34;auto&#34; &gt;}}

算法：



```python
def bfs(grid, start, end):
  visited = np.zeros_like(grid) # 存储已访问过的节点,访问过为1 
  parent = np.full_like(grid, None, dtype=object)  # 存储父节点，以便重建路径
  queue = deque([start]) # 创建一个队列，并将起始节点添加到队列中
```
          

---

> 作者: lvwinbor  
> URL: https://lvwinbor.github.io/posts/32c5de7/  

