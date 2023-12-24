import pygame
from pygame.locals import *

pygame.init()

screen = pygame.display.set_mode((640, 480))

clock = pygame.time.Clock()

animal_dict = {'cow': pygame.image.load('cow.png'),
                'chicken': pygame.image.load('chicken.png'),
                'pig': pygame.image.load('pig.png')}

class Animal:
    def __init__(self, animal_type, x, y):
        self.animal_type = animal_type
        self.x = x
        self.y = y
        self.image = animal_dict[animal_type]
        self.speed = 5

    def draw(self, screen):
        screen.blit(self.image, (self.x, self.y))

    def move(self):
        if self.animal_type == 'cow':
            self.x -= self.speed
        elif self.animal_type == 'chicken':
            self.y += self.speed
        elif self.animal_type == 'pig':
            self.x += self.speed

def create_animals():
    animals = []
    animals.append(Animal('cow', 320, 100))
    animals.append(Animal('chicken', 200, 100))
    animals.append(Animal('pig', 440, 100))
    return animals

def draw_animals(animals, screen):
    for animal in animals:
        animal.draw(screen)

def move_animals(animals):
    for animal in animals:
        animal.move()

animals = create_animals()

while True:
    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()
            sys.exit()

    screen.fill((0, 0, 0))

    move_animals(animals)
    draw_animals(animals, screen)

    pygame.display.flip()
    clock.tick(60)
