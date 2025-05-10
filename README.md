import pygame

class Bulled:
    def __init__(self, x, y, w, h, speed_y, skin):
        self.hitbox = pygame.Rect(x, y, w, h)
        self.skin = pygame.image.load(skin)
        self.speed_y = speed_y
    def draw(self, window):
        #pygame.draw.rect(window, [255, 0, 0],self.hitbox)
        window.blit(self.skin, self.hitbox)

class Airplane:
    def __init__(self, x, y, w, h, speed_x, speed_y, skin):
        self.hitbox = pygame.Rect(x, y, w, h)
        self.speed_x = speed_x
        self.speed_y = speed_y
        self.skin = pygame.image.load(skin)
        self.bulleds=[]
    def draw(self, window):
        #pygame.draw.rect(window, [255, 0, 0],self.hitbox)
        window.blit(self.skin, self.hitbox)

class Monster:
    def __init__(self, x, y, w, h, skin):
        self.hitbox = pygame.Rect(x, y, w, h)
        self.skin = pygame.image.load(skin)
    def draw(self, window):
        #pygame.draw.rect(window, [255, 0, 0],self.hitbox)
        window.blit(self.skin, self.hitbox)


pygame.init()

window = pygame.display.set_mode([500, 500])
clock = pygame.time.Clock()

monster = Monster( -25, 10, 50, 50,  "jet stisker.png")
monster1 = Monster(25, 10, 50, 50,  "jet stisker.png")
monster2 = Monster(75, 10, 50, 50,  "jet stisker.png")
monster3 = Monster(125, 10, 50, 50,  "jet stisker.png")
monster4 = Monster(175, 10, 50, 50,  "jet stisker.png")
monster5 = Monster(225, 10, 50, 50,  "jet stisker.png")
monster15 = Monster(275, 10, 50, 50,  "jet stisker.png")
monster6 = Monster(325, 10, 50, 50,  "jet stisker.png")
monster7 = Monster(375, 10, 50, 50,  "jet stisker.png")
monster8 = Monster(425, 10, 50, 50,  "jet stisker.png")
monster9 = Monster(0, 60, 50, 50,  "jet stisker.png")
monster10 = Monster(50, 60, 50, 50,  "jet stisker.png")
monster11 = Monster(100, 60, 50, 50,  "jet stisker.png")
monster12 = Monster(150, 60, 50, 50,  "jet stisker.png")
monster13 = Monster(200, 60, 50, 50,  "jet stisker.png")
monster14 = Monster(250, 60, 50, 50,  "jet stisker.png")
monster16 = Monster(300, 60, 50, 50,  "jet stisker.png")
monster17 = Monster(350, 60, 50, 50,  "jet stisker.png")
monster18 = Monster(400, 60, 50, 50,  "jet stisker.png")
monster19 = Monster(20, 110, 50, 50,  "jet stisker.png")
monster20 = Monster(70, 110, 50, 50,  "jet stisker.png")
monster21 = Monster(120, 110, 50, 50,  "jet stisker.png")
monster22 = Monster(170, 110, 50, 50,  "jet stisker.png")
monster23 = Monster(220, 110, 50, 50,  "jet stisker.png")
monster24 = Monster(270, 110, 50, 50,  "jet stisker.png")
monster25 = Monster(320, 110, 50, 50,  "jet stisker.png")
monster26 = Monster(370, 110, 50, 50,  "jet stisker.png")
monsters=[ monster, monster1, monster2, monster3, monster4, monster5, monster6, monster7, monster8, monster9, monster10, monster11,
monster12, monster13, monster14, monster15, monster16, monster17, monster18, monster19, monster20, monster21, monster22, monster23,
monster24, monster25, monster26]


background=pygame.image.load("Space.png")




airplane = Airplane(220, 450, 100, 25, 20, 20, "f15-pixilart.png")
while 1==1:
    keys = pygame.key.get_pressed()
    if keys[pygame.K_d]:
        airplane.hitbox.x += airplane.speed_x
    if keys[pygame.K_a]:
        airplane.hitbox.x -= airplane.speed_x
    
    if keys[pygame.K_m]:
        #bulled.hitbox.y -= bulled.speed_y
        bulled = Bulled(airplane.hitbox.x, airplane.hitbox.y,150, 200, -20,"Bullet.png")
        airplane.bulleds.append(bulled)

   #for jet stisker in monsters:
        #if ball.hitbox.colliderect(enemy.hitbox):
            #monsters.remove(enemy)
            #ball.speed_y *= -1
            #break

    if len(monsters)==0:
        monster.skin = pygame.image.load("space airplane.png")

    
    for monster in monsters:
            for b in airplane.bulleds:
                if monster.hitbox.colliderect(b.hitbox):
                    monsters.remove(monster) 
                    airplane.bulleds.remove(b)
                    break


            
    window.fill([0,0,0])
    window.blit(background, [0, 0])
    airplane.draw(window)
    for Monster in monsters:
        Monster.draw(window)
    for b in airplane.bulleds:
        b.draw(window)
        b.hitbox.y += b.speed_y
    pygame.display.flip()
    
    
    clock.tick(60)
