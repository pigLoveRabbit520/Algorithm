# 八皇后问题

问题本身是这样：在8×8格的国际象棋上摆放八个皇后，使其不能互相攻击，问有几种解。问题等价于8×8格的棋盘上，放8个棋子，任意两个棋子都不能处于同一行、同一列或同一斜线上，求有几种解。这个问题是**回溯算法**经典应用。

javascript实现

    const NUM_QUEENS = 8;
    let solutionNum = 0;

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



