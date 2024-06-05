import pygame
import random
import sys

# Initialize Pygame
pygame.init()

# Set up some constants
WIDTH, HEIGHT = 1080, 720
BACKGROUND_COLOR = (0, 0, 0)

# Create a screen
screen = pygame.display.set_mode((WIDTH, HEIGHT))

class Square:
    def __init__(self):
        self.x = WIDTH // 2
        self.y = HEIGHT - 50
        self.width = 50
        self.height = 50

    def draw(self, screen):
        pygame.draw.rect(screen, (255, 0, 0), (self.x, self.y, self.width, self.height))

class Target:
    def __init__(self):
        self.x = random.randint(0, WIDTH - 20)
        self.y = random.randint(0, HEIGHT // 2 - 20)
        self.width = 20
        self.height = 20
        self.speed = 10
        self.timer = 60
        

    def move(self):
        self.y += self.speed
        if self.y > HEIGHT - self.height:
            self.y = 0
            self.x = random.randint(0, WIDTH - 20)

    def draw(self, screen):
        pygame.draw.rect(screen, (0, 255, 0), (self.x, self.y, self.width, self.height))

        # Draw the timer
        font = pygame.font.Font(None, 36)
        text = font.render("Time left: " + str(int(self.timer)), True, (255, 255, 255))
        screen.blit(text, (10, 10))

        # Update the timer
        self.timer -= 1 / 60

def check_collision(square, target):
    if (target.x + target.width > square.x and
        target.x < square.x + square.width and
        target.y + target.height > square.y and
        target.y < square.y + square.height):
        return True
    return False

my_list = [30,35,40,45,50,55,0,100]
def main():
    clock = pygame.time.Clock()
    square = Square()
    num_enemies = random.choice(my_list)
    targets = [Target() for _ in range(num_enemies)]
    timer = 0

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        keys = pygame.key.get_pressed()
        if keys[pygame.K_LEFT]:
            square.x -= 25
        if keys[pygame.K_RIGHT]:
            square.x += 25

        screen.fill(BACKGROUND_COLOR)
        square.draw(screen)

        for target in targets:
            target.move()
            target.draw(screen)

            if check_collision(square, target):
                print("Game Over!")
                pygame.quit()
                sys.exit()

            if target.timer <= 0:
                num_enemies = random.choice(my_list)
                targets = [Target() for _ in range(num_enemies)]
                timer = 0

        timer += 1 / 60
        if timer >= 10:
            timer = 0

        pygame.display.flip()
        clock.tick(80)

if __name__ == "__main__":
    main()
