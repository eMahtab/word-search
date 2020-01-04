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
Ok lets ask this question before we talk about code implementation, how do we solve this problem in our head :grey_question:

We first search for first matching letter in the grid which matches with the first letter of the given word.
Then we try to find the match for remaining letters of the word in the grid.
Searching for matching letters in 4 directions  :
1. one column forward  (row, column + 1)
2. one column backward (row, column - 1)
3. one row above (row - 1, column)
4. one row down  (row + 1, column)

**Note that the order in which we look for matching letters doesn't matter, we can search in different order (2, 1, 3, 4) or (3, 4, 1, 2) etc.**


So we will iterate over grid row by row, scanning from first column to last column. We will first check if 
`board[row][column] == word.charAt(0)` is true, if it is, it means now we can start our search.

#### Base cases :

We will define a recursive method which will help us find the matches at index 1, index 2, index 3 and so on. We will increment the index by one, once we find a match for the character in the grid. If the value of index becomes equal to length of the given word, it means we found the entire match and we will return true (this will be one of our base case in the recursive method).

Also we need to check whether the value of row and column are within the bounds of the board and 
if `board[row][column] != word.charAt(index)`, if not we will return false (this will be our second base case in the recursive method)

Otherwise it means, we haven't found the entire word match and the character at `index` matches with `board[row][column]`
So now we search for next characters match in 4 cells `(row, column + 1)  (row, column - 1)  (row - 1, column)  (row + 1, column)` 


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

## References :
https://www.youtube.com/watch?v=vYYNp0Jrdv0

