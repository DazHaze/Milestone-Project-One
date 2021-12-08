# Farm People

Farm People is a website created to tell people about a small home farm run by a couple in the Republic of Ireland. It produces fresh vegetables and free-range eggs. The site is solely run CSS and HTML. 

This was created for a project for the Full Stack Development course hosted by [Code Institute](https://codeinstitute.net/ie/5-day-coding-challenge/?utm_term=code%20institute&utm_campaign=CI+-+IRL+-+Search+-+Brand&utm_source=adwords&utm_medium=ppc&hsa_acc=8983321581&hsa_cam=14304747355&hsa_grp=128775288209&hsa_ad=539453915484&hsa_src=g&hsa_tgt=kwd-319867646331&hsa_kw=code%20institute&hsa_mt=e&hsa_net=adwords&hsa_ver=3&gclid=Cj0KCQiAzMGNBhCyARIsANpUkzORRe5o1VJJG9_EwnX2Oxn-ftPjCcE-f8G-M0uOoLartu-8DkXRH5YaAozNEALw_wcB).

[Farm People (Link to external site)](https://dazhaze.github.io/Milestone-Project-One/index.html)

![Am-I-Responsive](https://raw.githubusercontent.com/DazHaze/Milestone-Project-One/main/assets/images/redo-readme/Am-I-Responsive.png)

## The Website

This Website is created as a base for a fully functioning website.

* This goal of the website from the beginning was to create a solid platform to move forward with. The basic layout is solid and clear which will make it easy to be improved and added to.

* The user can find out about the farm and view the about page to find out about the couple that is running it.
## Features

### **Existing Features**

* Landing Page
  * The landing page clearly shows what the website is for and guides the user to social media.

![Instagram-main-page](https://raw.githubusercontent.com/DazHaze/Milestone-Project-One/main/assets/images/redo-readme/instagram-main-page.png)

* Social media links are also clear on the footer

![Mainaining Scores](images/maintaining-scores.png)

* Computer thinking animation to give user the feeling of playing against a real player.

![Computer Thinking Animation](images/computer-thinking-animation.png)

* Piece dropping animation. Without this it is hard for the user to see that they are playing connect four.

![Piece Dropping Animation](images/dropping-animation.png)

### **Future Features**

* Give the computer a more advanced decision making algorithm.
* Create computer predictability so that the user can learn the computer move pattern.
* Display board and pieces in a cleaner way.
* Allow user to have choice of which piece they have.
* Coin toss for who starts (Important because there are patterns where the user that is first always wins).

## Data Model

I decided to use a board class as my model. The game creates an instance of the board when the game starts.

The board class stores the board, size and if the game is currently playing. The board also has moethpds to help play the game. Such as a `print_board` method to print out the current board. A `valid_drop` method to check if there is space in the chosen column and what row that space is. A `dropping_piece` method to create a print animation to drop the piece into the board.

## Testing

I have manually tested this project by doing the following:
* Passed the code through [PEP8](http://pep8online.com/checkresult) linter and confirmed there are no warnings or errors.
* Given invalid inputes: strings when numbers are expected, out of bounds inputs, the same input twice.
* Tested in both local and deployed terminals.

## Bugs

### **Solved Bugs**

#### **Win conditions**
* When creating the 'check_win' function I was getting out of bounds in array errors for some win conditions. I noticed this would be because to check
if the user has won the conditions had row + 1, row + 2 and row + 3 ( with the same for columns). If the board position was `(5, 3)` then row +3 would cause the final value of 
8 to be greater than the actual number of rows available to check. My first idea for a fix was just to add:
```python
    if (row + 3) <= 6:
        # Check for wins
```
* I soon figured out that this does not work as some column win conditions would have a row element that would be out of bounds if 3 is added.
```python
    for c in range(self.col_count-3):
            for r in range(self.row_count):
                if (b[r][c] == piece and
                    b[r][c+1] == piece and
                        b[r][c+2] == piece and
                        b[r][c+3] == piece):
                    return True
```
* I finally settled for this approach after **many** different attempts at this problem. This method has 4 code blocks in the check win function. One for vertical win, one for horixontal win and two for the positive and negative diagonals.

#### **Working backwards**
* At the beginning of this project I found it difficult to work with the board as the first piece would be at say `(0,6)` instead of `(0,0)`. 
This was solved by working with the board in the postion where `(0,0)` is the bottom and then flipping it to display to the user at the end.
```python
    def display_upsidedown_board(self):
            """
            Prints the upside down and flipped board array so pieces at 0,0
            are at the bottom.
            """
            print(f'\n{np.flip(self.board, 0)}\n')
```

### **Remaining Bugs**

* User can send an input when the computer is choosing and placing the piece. This does not break the game as the user choice is still sent and displayed. A fix could be some sort of await function after the user sends one input.

## Validator Testing
* PEP8
  * No errors returned from [PEP8online.com](PEP8online.com)

## Deployment
This project was deployed using Code Institute's mock terminal for Heroku.

* Steps for deployment:
  * Fork or clone this repository
  * Create new Heroku app
  * Set the buildbacks to `Python` and `NodeJS` in that order
  * Link the Heroku app to the repository
  * Click on `Deploy`

## Credits
* [Code Institute](https://codeinstitute.net/all-access-coding-challenge/?utm_term=code%20institute&utm_campaign=CI+-+IRL+-+Search+-+Brand&utm_source=adwords&utm_medium=ppc&hsa_acc=8983321581&hsa_cam=14304747355&hsa_grp=128775288209&hsa_ad=539453915484&hsa_src=g&hsa_tgt=kwd-319867646331&hsa_kw=code%20institute&hsa_mt=e&hsa_net=adwords&hsa_ver=3&gclid=CjwKCAiAv_KMBhAzEiwAs-rX1PXOCAky8yjljHzgvSnccpkyUOvNLVGMuzG11t86weTdFdPiTfNHHhoCFuwQAvD_BwE) for the deployment terminal and the formatting for this MarkDown document.

* [Wikipedia](https://en.wikipedia.org/wiki/Connect_Four) for details on Connect Four game.

* [Geoffrey Mariette](https://medium.com/@geoffrey.mariette/crazy-connect4-with-python-146d384f4cfb) for article on Python Connect Four.