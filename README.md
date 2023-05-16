# codepath-prework
import pygame
import time
import random

# Initialize Pygame
pygame.init()

# Define colors
black = pygame.Color(0, 0, 0)
white = pygame.Color(255, 255, 255)
red = pygame.Color(255, 0, 0)
green = pygame.Color(0, 255, 0)
blue = pygame.Color(0, 0, 255)

# Set the width and height of the game window
width = 800
height = 600
game_window = pygame.display.set_mode((width, height))

# Set the title of the game window
pygame.display.set_caption('Snake Game')

# Set the speed of the snake
snake_speed = 15

# Define the font style and size
font_style = pygame.font.SysFont(None, 50)

# Define the score font style and size
score_font = pygame.font.SysFont(None, 35)


def your_score(score):
    value = score_font.render("Your Score: " + str(score), True, white)
    game_window.blit(value, [10, 10])


def our_snake(snake_block, snake_list):
    for x in snake_list:
        pygame.draw.rect(game_window, green, [x[0], x[1], snake_block, snake_block])


# Define the game loop
def game_loop():
    game_over = False
    game_close = False

    # Initial position of the snake
    x1 = width / 2
    y1 = height / 2

    # Change in position of the snake
    x1_change = 0
    y1_change = 0

    # Define the size of the snake's body
    snake_block = 10

    # Create an empty list for the snake's body
    snake_list = []
    length_of_snake = 1

    # Generate random coordinates for the food
    food_x = round(random.randrange(0, width - snake_block) / 10.0) * 10.0
    food_y = round(random.randrange(0, height - snake_block) / 10.0) * 10.0

    # Game loop
    while not game_over:

        while game_close:
            game_window.fill(black)
            game_over_message = font_style.render("Game Over! Press Q-Quit or C-Play Again", True, red)
            game_window.blit(game_over_message, [width / 6, height / 3])
            your_score(length_of_snake - 1)
            pygame.display.update()

            # Check for key presses in the game over screen
            for event in pygame.event.get():
                if event.type == pygame.KEYDOWN:
                    if event.key == pygame.K_q:
                        game_over = True
                        game_close = False
                    if event.key == pygame.K_c:
                        game_loop()

        # Check for key presses during the game
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                game_over = True
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_LEFT:
                    x1_change = -snake_block
                    y1_change = 0
                elif event.key == pygame.K_RIGHT:
                    x1_change = snake_block
                    y1_change = 0
                elif event.key == pygame.K_UP:
                    y1_change = -snake_block
                    x1_change = 0
                elif event.key == pygame.K_DOWN:
                    y1_change = snake_block
                    x1_change = 0

        # Check if
