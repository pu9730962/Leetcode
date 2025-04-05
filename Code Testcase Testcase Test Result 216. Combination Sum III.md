# 162. Find Peak Element
## 問題描述
找到所有可以利用k個1-9的數字(不重複)，加總成n的組合。

## Example
![Example](https://github.com/pu9730962/Leetcode/blob/main/Images/Combination%20Sum%20III.png)

## 想法
Backtracking 核心步驟
1.選擇當前步驟：對於每一步驟，嘗試一個選項。  
2.進行遞迴：根據選擇，繼續構建下一步的解答。  
3.回溯：如果當前選擇無法導致最終解答，則回溯並選擇其他選項。  
4.重複：直到嘗試完所有選項，找到所有可能的解答。  

>這題指標稍微複雜，要注意!

## 程式碼
```C
void backtracking(int k, int n, int start, int *path, int pathSize, int ***result, int *returnSize, int **returnColumnSizes){
    if(n < 0) return;
    if(pathSize == k){
        if(n == 0){
            (*returnSize)++;
            *result = realloc(*result, (*returnSize) * sizeof(int*));
            (*result)[*returnSize - 1] = (int*)malloc(k * sizeof(int));
            for(int i = 0; i < k; i++){
                (*result)[*returnSize - 1][i] = path[i];
            }

            *returnColumnSizes = realloc(*returnColumnSizes, (*returnSize) * sizeof(int));
            (*returnColumnSizes)[*returnSize - 1] = k;
        }

        return;
    }

    for(int i = start; i <= 9; i++){
        path[pathSize] = i;
        backtracking(k, n-i, i+1, path, pathSize+1, result, returnSize, returnColumnSizes);
    }
}
int** combinationSum3(int k, int n, int* returnSize, int** returnColumnSizes) {
    *returnSize = 0;
    *returnColumnSizes = NULL;
    int **result = NULL;
    int path[9];

    backtracking(k, n, 1, path, 0, &result, returnSize, returnColumnSizes);

    return result;
}
```
