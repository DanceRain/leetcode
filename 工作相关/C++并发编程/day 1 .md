## 创建线程

```c++
void proc(int& a)
{
    cout << "我是子线程，传入参数为" << a << endl;
    cout << "子线程种显示子线程id为" << this_thread::get_id << endl;
}

int main()
{
    int a = 9;
    thread th2(proc, ref(a));
    cout << "我是主线程" << endl;
    cout << "主线中显示子线程的id为" << th2.get_id() << endl;
    th2.join();
    return 0;
}
```

将join（）理解为“等待”，在程序中主线程将等待子线程运行结束才继续执行。