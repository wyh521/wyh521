import pygame  
import sys  
from pygame.locals import *  
  
# 游戏设置  
S_WIDTH, S_HEIGHT = 800, 600  
  
class Block:  
    def __init__(self, x, y, w, h, color):  
        self.x = x  
        self.y = y  
        self.w = w  
        self.h = h  
        self.color = color  
  
    def draw(self, screen):  
        pygame.draw.rect(screen, self.color, (self.x, self.y, self.w, self.h))  
  
class Player:  
    def __init__(self, x, y):  
        self.x = x  
        self.y = y  
        self.speed = 5  
  
    def update(self, keys_pressed):  
        if keys_pressed[K_UP]:  
            self.y -= self.speed  
        if keys_pressed[K_DOWN]:  
            self.y += self.speed  
        if keys_pressed[K_LEFT]:  
            self.x -= self.speed  
        if keys_pressed[K_RIGHT]:  
            self.x += self.speed  
  
    def draw(self, screen):  
        pygame.draw.circle(screen, (255, 0, 0), (self.x, self.y), 20)  
  
def main():  
    pygame.init()  
    screen = pygame.display.set_mode((S_WIDTH, S_HEIGHT))  
    clock = pygame.time.Clock()  
  
    # 游戏角色和方块设置  
    player = Player(S_WIDTH / 2, S_HEIGHT - 30)  
    blocks = [Block(100, 100, 50, 50, (255, 255, 255)), Block(200, 200, 50, 50, (0, 0, 255)), Block(300, 300, 50, 50, (255, 0, 0))]  
  
    running = True  
    while running:  
        for event in pygame.event.get():  
            if event.type == pygame.QUIT:  
                running = False  
            if event.type == pygame.KEYDOWN:  
                if event.key == pygame.K_ESCAPE:  
                    running = False  
  
        keys_pressed = pygame.key.get_pressed()  
        player.update(keys_pressed)  
  
        screen.fill((0, 0, 0))  # 清屏  
        for block in blocks:  
            block.draw(screen)  
        player.draw(screen)  
        pygame.display.flip()  # 更新屏幕显示内容  
        clock.tick(60)  # 设置游戏刷新率为60 FPS  
  
    pygame.quit()  
    sys.exit(1)  # 退出游戏循环  
  
if __name__ == "__main__":  
    main()
