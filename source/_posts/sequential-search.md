title: 顺序表查找算法及其优化
date: 2014-09-01 17:27:21
tags: 算法, 优化
---
顺序查找算法实现如下:

    var arr = [5, 2, 4, 3, 1]
        , sequentialSearch = function(arr, val) {
            var i = 0
                , len = arr.length;
            for ( ; i < len; i++) {             // 比较一次
                if (arr[i] === val) {           // 比较二次
                    return i;
                }
            }
            return i;                           // 返回len,则说明查找失败
        }

这里并不是足够完美, 因为每次循环时都需要对i是否越界, 即是否小于len做判断。事实上，还可以有更好的办法，设置一个哨兵, 就可以解决不需要每次让i与len做比较了。
## 顺序表查找优化
    var arr = [5, 2, 4, 3, 1]
        // 有哨兵的顺序表查找
        , sequentialSearchOpt = function(arr, val) {
            var i = 0
                , arr = arr.slice(0)            // 保证函数内操作不影响外部的arr数组 
                , len = arr.length;
            arr[len] = val;                     // 设置arr[len]为关键字值作为哨兵
            // arr.push(val);
            while (arr[i] !== val) {            // 比较一次
                i++;
            }
            return i;                           // 返回len,则说明查找失败
        }

如果arr[i]中有值等于val则返回i，否则一定会在循环结束处等于val, 此时返回len值。说明数组中没有关键字等于val,查找失败。

> 在测试过程中, 发现因为由于对象是按地址传递的，在函数中改变数组`arr[len] = val`会影响到外部的数组，因此需要在函数内clone一份数组出来

这种在查找方向的尽头设置‘哨兵’免去了在查找过程中每一次比较后都要判断查找位置是否越界的小技巧，看似与原先差别不大，但在总数较多时，效率提高很大，是非常好的编程技巧。

**参考：** 大话数据结构 

