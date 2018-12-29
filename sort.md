## 排序算法

### 测试数据
```javascript
    var playload = [5,4,7,12,4,9,2,1,13,2];
```

### 冒泡排序
```javascript
var playload = [5,4,7,12,4,9,2,1,13,2];
function bubbleSort(arr){
    //从右到左冒泡，一次冒泡将最大的排在左边
    for(let i=0;i<arr.length;i++){
        for(let j=0;j<arr.length-i-1;j++){
            if( arr[j] > arr[j+1]){
                let temp = arr[j+1];
                arr[j+1] = arr[j];
                arr[j] = temp;
            }
        }
    }
    return arr;
}
bubbleSort(playload);
```

### 选择排序

```javascript
var playload = [5,4,7,12,4,9,2,1,13,2];
function selectSort(arr){
    //左边是已排好序，从右边选择最小的放到左边
    for(let i = 0; i < arr.length-1; i++){
        let min = i;
        for(let j=i+1; j < arr.length; j++ ){
            if( arr[min] > arr[j]){
               min = j;
            }
        }
        let temp = arr[i];
        arr[i] = arr[min];
        arr[min] = temp;
    }
    return arr;
}
selectSort(playload);
```

### 插入排序

```javascript
var playload = [5,4,7,12,4,9,2,1,13,2];
function insertionSort(arr){
    //左边是已排好序，将右1插入左边合适位置
    for(let i=1; i<arr.length;i++){
        let key  = arr[i];
        let j = i-1;
        while(j>=0 && arr[j]>key){
            arr[j+1] = arr[j]
            j--;
        }
        arr[j+1] = key;
    }
    return arr;
}
insertionSort(playload);
```

### 快速排序
```javascript
var playload = [5,4,7,12,4,9,2,1,13,2];
function quickSort(arr,low,high){
    //关键是找到中间点，中间点左边的数都比它小，中间点右边的数都比它大
    if(low < high){
        let pivot = partition(arr, low, high);
        quickSort(arr, low, pivot-1);
        quickSort(arr, pivot+1, high);
    }
    return arr;
}
function partition(arr,low,high){
    let pivot = arr[low];
    while(low<high){
        while(low<high && arr[high]>pivot){
            high--;
        }
        arr[low] = arr[high];
        while(low<high && arr[low]<=pivot){
            low++;
        }
        arr[high] = arr[low]
    }
    arr[low] = pivot;
    return low;
}
quickSort(playload,0,playload.length-1);
```