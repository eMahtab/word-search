# Word Search
## https://leetcode.com/problems/word-search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

```
Example:

board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```
## Approach :



## Implementation :

```java
public  boolean exist(char[][] board, String word) {
		if(board == null || board.length == 0)
			return false;
		
		for(int row = 0; row < board.length; row++) {
			for(int column = 0; column < board[0].length; column++) {
				if(board[row][column] == word.charAt(0) && searchWord(board, row, column, word, 0)) {
					return true;
				}
			}
		}
		return false;
	}

	private  boolean searchWord(char[][] board, int row, int column, String word, int index) {
		if(index == word.length()) {
			return true;
		}
		if(row < 0 || row >= board.length || column < 0 || column >= board[0].length || 
				 board[row][column] != word.charAt(index)) {
			return false;
		}
		
		char temp = board[row][column];
		board[row][column] = '#';
		
		boolean res = searchWord(board, row, column + 1, word, index + 1) ||
				      searchWord(board, row, column - 1, word, index + 1) ||
				      searchWord(board, row - 1, column, word, index + 1) ||
				      searchWord(board, row + 1, column, word, index + 1);
		
		board[row][column] = temp;
		return res;		      
	}

```
