# 6-14 仅有头指针的队列
# 如果用一个循环数组表示队列，且只有一个队列头指针 front，不设队列尾指针 rear，而设置计数器 count 用以记录队列中结点的个数。请编写算法实现队列的三个基本运算：判空、入队、出队。
# 函数接口定义中，QElemSet 是用户定义的数据类型，例如 int、double 或者 char 等。函数 IsEmpty 的功能是判断 queue 是否为空队，若是则返回 true，否则返回 false；函数 EnQueue 将元素 x 插入队尾；函数 DeQueue 将队首元素删除。
# 当调用 EnQueue 但队列已满，或调用 DeQueue 但队列为空时，应该在一行中输出错误信息 ERROR。

bool IsEmpty(Queue queue){
    return queue->count==0;
}
void EnQueue(Queue queue, QElemSet x){
    if(queue->count==queue->capacity){
        printf("ERROR\n");
        return;
    }
    Position rear=(queue->front+queue->count)%queue->capacity;
    queue->data[rear]=x;
    queue->count++;
}
void DeQueue(Queue queue){
    if(queue->count==0){
        printf("ERROR\n");
        return;
    }
    queue->front=(queue->front+1)%queue->capacity;
    queue->count--;
}
