面试题，出队的判断搞了半天没搞出来，主要还是没刷 leetcode。下面这个加了模板和一些判断，昨天写得太low了。

```c++
template <typename T>
class Queue
{
public:
    void enqueue(const T& _elem)
    {
        s_1.push(_elem);
    }
    void dequeue()
    {
        if(s_1.empty() && s_2.empty())
        {
            cerr << "queue is empty" << endl;
        }
        if(!s_2.empty())
        {
            s_2.pop();
        }
        while(!s_1.empty())
        {
            int _s_1_top = s_1.top();
            s_1.pop();
            s_2.push(_s_1_top);
        }
        s_2.pop();
    }
    int top()
    {
        if(s_1.empty() && s_2.empty())
        {
            cerr << "queue is empty" << endl;
            s_1.top();
        }
        int ret;
        if(!s_2.empty())
        {
            ret = s_2.top();
            return ret;
        }
        while(!s_1.empty())
        {
            int _s_1_top = s_1.top();
            s_1.pop();
            s_2.push(_s_1_top);
        }
        ret = s_2.top();
        return ret;
    }
private:
    stack<T> s_1;
    stack<T> s_2;
};
```

​																																			2022-4-13