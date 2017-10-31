# Python Application focusing Data Structures and Algorithms

## "Guess That Number" game

### Version A

The following program shows the use of conditionals and the import of 
the `random` module to generate random numbers for the user to guess. 
Also, it is presented how to get an input from the user. Let's see:

```python
#!/usr/bin/env python3
import random

def main():
    print('---------------------------------')
    print('   GUESS THAT NUMBER GAME')
    print('---------------------------------')
    print()
    the_number = random.randint(0, 100)
    guess = -1

    name = input('Player what is your name? ')

    while guess != the_number:
        guess_text = input('Guess a number between 0 and 100: ')
        guess = int(guess_text)
        if guess < the_number:
            print(f"Sorry {name}, your guess of {guess} was too LOW.")
        elif guess > the_number:
            print(f"Sorry {name}, your guess of {guess} was too HIGH.")
        else:
            print(f"Excellent work {name}, you won, it was {guess}!")

    print("We're done here.\n")

if __name__ == '__main__':
    main()
```
