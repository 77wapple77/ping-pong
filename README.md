# ping-pong
from pygame import *
'from pygame import movie'
#Создание классов
class GameSprite(sprite.Sprite):
    def __init__(self, player_speed, player_image, move_up, move_down, player_x, player_y):
        super().__init__()
        self.player_speed = player_speed
        self.image = transform.scale(image.load(player_image), (w_weight, w_height))
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y
    def reset(self):
        window.blit(self.image(self.rect.x, self.rect.y))   

class Player(GameSprite):
    def update_l(self):
        keys = key.get_pressed()
        if keys[K_w] and self.rect.y > 5:
            self.rect.y -= self.player_speed
        if keys[K_s] and self.rect.y < self.w_height - 80:
            self.rect.y += self.player_speed
    def update_r(self):
        keys = key.get_pressed()
        if keys[K_UP] and self.rect.y > 5:
            self.rect.y -= self.player_speed
        if keys[K_DOWN] and self.rect.y < self.w_height - 80:
            self.rect.y += self.player_speed
#размеры картинок
w_height = 500
w_weight = 700
'back = (25, 134, 67)'
#Создание окна
window = display.set_mode((w_weight, w_height))
'window.fill(back)'
#Названия картинок
img_rackets = 'ping-pong_racket.png'
img_ball = 'ball.png'
img_back = 'background.jpg'

bg = transform.scale(image.load(img_back), (w_weight, w_height))
#создание флажков
finish = False
game = True
clock = time.Clock()
FPS = 60
#Описание класса игроков
racket_1 = Player(img_rackets, 30, 200, 4, 50, 150)
racket_2 = Player(img_rackets, 520, 200, 4, 50, 150)
ball = GameSprite(img_ball, 200, 200, 4, 50, 50)
#Создание игрового цикла
while game:
    for e in event.get():
        if e.type == QUIT:
            game = False
    if sprite.collide(ball, racket_1) and sprite.collide(ball, racket_2):
        ball.player_speed = -1
    if ball.collide(w_height - 490) and ball.collide(w_height - 10):
        ball.player_speed = -1

    if finish != True:
        window.blit(bg, (0, 0))

        racket.update_l()
        racket.update_r()

        racket_1.reset()
        racket_1.draw()

        racket_2.draw()
        racket_2.reset()

        ball.reset()
        ball.draw()

    display.update()
    clock.tick(FPS)
