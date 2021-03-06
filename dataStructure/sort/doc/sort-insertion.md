## 插入排序

思路：将数据分为两个区域：有序区，无序区。每一次,帮无序区的一个元素，在有序区中找到合适的位置并插入进去，直到将有序区的放满。

### 简单插入排序

元素插入有序区的时候，可以从前向后比较，也可以从后向前比较。这里推荐使用从后向前。

#### 实现算法：
1. 取出无序区的一个元素。
2. 从有序区的从后向前比较，如果准备插入元素比当前指针指向的前一位小，则将有序区的当前元素后移一位。直到找到合适的插入位置。
3. 将这个元素插入到有序区中。

```JavaScript
function insertion(array) {
    if (!Array.isArray(array)) {
        return null;
    }

    for (let i = 1; i < array.length; i++) {
        let temp = array[i];
        let j = i;
        for (; j > 0 && array[j-1] > temp ; j--) {
            array[j] = array[j-1];
        }
        array[j] = temp;
    }

    return array;
}

```

### 希尔排序

#### 前提知识：
1. 希尔排序通过将比较的全部元素分为几个区域来提升插入排序的性能。
2. 如果需排序的数据几乎是已排好的了，那么此时插入排序较快。
3. 步长序列：即步长的选择，最后都会为1。常见的有互质的步长（2<sup>k</sup>-1)，我们这里使用最简单的二分法。

```javascript
function shell(array) {
    if (!Array.isArray(array)) {
        return null;
    }

    const length = array.length;
    let gap = Math.floor(length / 2);

    while (gap > 0) {
        for (let i = gap; i < array.length; i++) {
            let temp = array[i];
            let j = i;
            for (; j > 0 && array[j - gap] > temp; j -= gap) {
                array[j] = array[j - gap];
            }
            array[j] = temp;
        }

        gap = Math.floor(gap / 2);
    }

    return array;
}
```
## 源代码
[sort-insertion](../src/insertion.js)


