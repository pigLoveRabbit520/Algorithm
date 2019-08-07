# 八皇后问题

问题本身是这样：在8×8格的国际象棋上摆放八个皇后，使其不能互相攻击，问有几种解。问题等价于8×8格的棋盘上，放8个棋子，任意两个棋子都不能处于同一行、同一列或同一斜线上，求有几种解。

javascript实现

```text
const NUM_QUEENS = 8
let solutionNum = 0

let queens = (new Array(NUM_QUEENS)).fill(-1);
function eightQueensPuzzle(queens) {
    placeQueen(queens, 0);
    console.log(`解个数为${solutionNum}`);
}

function placeQueen(queens, row) {
    for(let i = 0; i < NUM_QUEENS; i++) {
        queens[row] = i;
        if(row == 0) {
            placeQueen(queens, row + 1);
        } else {
            if(isLegal(queens, row)) {
                if(row == NUM_QUEENS - 1) {
                    solutionNum++;
                    console.log(queens);
                } else {
                    placeQueen(queens, row + 1);
                }
            }
        }
    }
}

function isLegal(queens, row) {
    for(let i = 0; i < row; i++) {
        if(queens[row] == queens[i] || ( Math.abs(queens[row] - queens[i]) == Math.abs(row - i) )) {
            return false;
        }
    }
    return true;
}

eightQueensPuzzle(queens);
```

用堆栈方式解决
```
class Stack {
    constructor() {
        this.top = -1
        this.arr = [0] // 记录列值，从1开始
    }

    setItem(item) {
        this.top++
        if (this.arr.length > this.top) {
            this.arr[this.top] = item
        } else {
            this.arr.push(item)
        }
    }

    getTopItem() {
        return this.arr[this.top]
    }

    display() {
        let res = []
        for (let row = 1; row <= this.top; row++) {
            res.push(`(${row}, ${this.arr[row]})`)
        }
        console.log(res.join(' '))
    }
}

function placeQueen(arr, top, col) {
    if (top <= 1) {
        return true 
    } else {
        for (let row = 1; row < top; row++) {
            if (arr[row] === col || (Math.abs((arr[row] - col)) === Math.abs(row - top))) {
                return false
            }
        }
        return true
    }
}

function queenProblem(num) {
    const stack = new Stack()
    stack.top = 0 // 不从0开始
    stack.setItem(0) // 放入(1,0)
    while (stack.top > 0) {
        let find = false
        for (let col = stack.getTopItem() + 1; col <= num; col++) {
            if (placeQueen(stack.arr, stack.top, col)) {
                stack.arr[stack.top] = col
                find = true
                break
            }
        }
        if (find) {
            if (stack.top === num) {
                stack.display() // 打印结果
            } else {
                stack.setItem(0) // 进入下一行从0开始
            }
        } else {
            stack.top--
        }
    }
}
```
