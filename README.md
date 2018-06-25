# BragonDollJ
#My first game on programing class

import pygame
pygame.init()

win = pygame.display.set_mode((640,480))

pygame.display.set_caption("Bragon Doll J")

walkRight = [pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R1.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R2.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R3.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R4.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R5.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R6.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R7.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R8.png'),pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R9.png')]
walkLeft = [pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L1.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L2.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L3.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L4.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L5.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L6.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L7.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L8.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L9.png')]
walkRight2 = [pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R1E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R2E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R3E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R4E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R5E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R6E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R7E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R8E.png'),pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/R9E.png')]
walkLeft2 = [pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L1E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L2E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L3E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L4E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L5E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L6E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L7E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L8E.png'), pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/L9E.png')]
bg = pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/mapa.png')
char = pygame.image.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/standing.png')

clock = pygame.time.Clock()

bulletSound = pygame.mixer.Sound('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/atack.ogg')
bulletSound2 = pygame.mixer.Sound('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/atack2.ogg')
hitSound = pygame.mixer.Sound('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/hits.ogg')
bulletSound.set_volume(0.5)
hitSound.set_volume(0.3)

music = pygame.mixer.music.load('C:/Users/bielh/OneDrive/Área de Trabalho/Jogo/Jogo/Game/MHA.ogg')
pygame.mixer.music.set_volume(0.4)
pygame.mixer.music.play(-1)



class player(object):
    def __init__(self,x,y,width,height):
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.vel = 5
        self.health = 10
        self.visible = True
        self.isJump = False
        self.left = False
        self.shooting = False
        self.right = False
        self.walkCount = 0
        self.jumpCount = 10
        self.standing = True
        self.hitbox = (self.x + 17, self.y + 11, 29, 52)

    def draw(self, win):
        if self.visible:
            if self.walkCount + 1 >= 27:
                self.walkCount = 0

            if not(self.standing):
                if self.left:
                    win.blit(walkLeft[self.walkCount//3], (self.x,self.y))
                    self.walkCount += 1
                elif self.right:
                    win.blit(walkRight[self.walkCount//3], (self.x,self.y))
                    self.walkCount +=1
            else:
                if self.right:
                    win.blit(walkRight[0], (self.x, self.y))
                else:
                    win.blit(walkLeft[0], (self.x, self.y))
            self.hitbox = (self.x + 17, self.y + 11, 29, 52)
        #pygame.draw.rect(win, (255,0,0), self.hitbox,2)

    def hit(self):
        if self.health > 1:
            self.health -= 1
        else:
            self.visible = False





class projectile(object):
    def __init__(self,x,y,radius,color,facing):
        self.x = x
        self.y = y
        self.radius = radius
        self.color = color
        self.facing = facing
        self.vel = 8 * facing

    def draw(self,win):
        pygame.draw.circle(win, self.color, (self.x,self.y), self.radius)
class projectile2(object):
    def __init__(self,x,y,radius,color,facing):
        self.x = x
        self.y = y
        self.radius = radius
        self.color = color
        self.facing = facing
        self.vel = 8 * facing

    def draw(self,win):
        pygame.draw.circle(win, self.color, (self.x,self.y), self.radius)


class player2(object):
    def __init__(self,x,y,width,height):
        self.x = x
        self.y = y
        self.width = width
        self.height = height
        self.vel = 5
        self.health = 10
        self.visible = True
        self.isJump = False
        self.shooting = False
        self.left = False
        self.right = False
        self.walkCount = 0
        self.jumpCount = 10
        self.standing = True
        self.hitbox = (self.x + 17, self.y + 11, 29, 52)

    def draw(self, win):
        if self.visible:
            if self.walkCount + 1 >= 27:
                self.walkCount = 0

            if not(self.standing):
                if self.left:
                    win.blit(walkLeft2[self.walkCount//3], (self.x,self.y))
                    self.walkCount += 1
                elif self.right:
                    win.blit(walkRight2[self.walkCount//3], (self.x,self.y))
                    self.walkCount +=1
            else:
                if self.right:
                    win.blit(walkRight2[0], (self.x, self.y))
                else:
                    win.blit(walkLeft2[0], (self.x, self.y))
            self.hitbox = (self.x + 17, self.y + 11, 29, 52)
        #pygame.draw.rect(win, (255,0,0), self.hitbox,2)

    def hit(self):
        if self.health > 1:
            self.health -= 1
        else:
            self.visible = False




def redrawGameWindow():
    win.blit(bg, (0,0))
    text = font.render('Vida: ' + str(score), 1, (0,0,0))
    text2 = font.render('Vida: ' + str(score2), 2, (0,0,0))
    text3 = font2.render("Player 2 Venceu",2,(50,205,50))
    text4 = font2.render("Player 1 Venceu",2,(50,205,50))
    if score < 1:
        win.blit(text4,(200,210))
    if score2 < 1:
        win.blit(text3,(200,210))
    win.blit(text, (540, 10))
    win.blit(text2,(0,10))

    man.draw(win)
    man2.draw(win)
    for bullet in bullets:
        bullet.draw(win)
    for tiro in tiros:
        tiro.draw(win)

    pygame.display.update()


#mainloop
font = pygame.font.SysFont('comicsans', 30, True)
font2 = pygame.font.SysFont('arial',38,True)
man = player(100, 377, 64, 64)
man2 = player2(500, 381, 64, 64)
score = 10
score2 = 10
shootLoop = 0
shootLoop2 = 0
bullets = []
tiros = []
run = True
estado = 'jogando'
while run:
    clock.tick(27)



    if shootLoop > 0:
        shootLoop += 1
    if shootLoop > 3:
        shootLoop = 0

    if shootLoop2 > 0:
        shootLoop2 += 1
    if shootLoop2 > 3:
        shootLoop2 = 0

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            run = False

    if man2.visible == True:

        for bullet in bullets:
            if bullet.x < 640 and bullet.x > 0:
                bullet.x += bullet.vel
            else:
                bullets.remove(bullet)
            if bullet.y - bullet.radius < man.hitbox[1] + man.hitbox[3] and bullet.y + bullet.radius > man.hitbox[1]:
                if bullet.x + bullet.radius > man.hitbox[0] and bullet.x - bullet.radius < man.hitbox[0] + man.hitbox[2]:
                    hitSound.play()
                    man.hit()
                    bullets.pop(bullets.index(bullet))
                    score2 -= 1



    if man.visible == True:

        for tiro in tiros:
            if tiro.x < 640 and tiro.x > 0:
                tiro.x += tiro.vel
            else:
                tiros.remove(tiro)
            if tiro.y - tiro.radius < man2.hitbox[1] + man2.hitbox[3] and tiro.y + tiro.radius > man2.hitbox[1]:
                if tiro.x + tiro.radius > man2.hitbox[0] and tiro.x - tiro.radius < man2.hitbox[0] + man2.hitbox[2]:
                    hitSound.play()
                    man2.hit()
                    tiros.pop(tiros.index(tiro))
                    score -= 1




    keys = pygame.key.get_pressed()
    if score < 1:
        estado = 'end'
    if score2 < 1:
        estado = 'end'


    if keys[pygame.K_KP4] and shootLoop2 == 0:
        if man2.left:
            facing = -1
        else:
            facing = 1
        if len(bullets) < 4:
            bulletSound2.play()
            bullets.append(projectile(round(man2.x + man2.width //2), round(man2.y + man2.height//2), 6, (0,191,255), facing))
        shootLoop2 = 1

    if keys[pygame.K_LEFT] and man2.x > man2.vel:
        man2.x -= man2.vel
        man2.left = True
        man2.right = False
        man2.standing = False
    elif keys[pygame.K_RIGHT] and man2.x < 640 - man2.width - man2.vel:
        man2.x += man.vel
        man2.right = True
        man2.left = False
        man2.standing = False
    else:
        man2.standing = True
        man2.walkCount = 0

    if not(man2.isJump):
        if keys[pygame.K_UP]:
            man2.isJump = True
            man2.right = False
            man2.left = False
            man2.walkCount = 0
    else:
        if man2.jumpCount >= -10:
            neg = 1
            if man2.jumpCount < 0:
                neg = -1
            man2.y -= (man2.jumpCount ** 2) * 0.5 * neg
            man2.jumpCount -= 1
        else:
            man2.isJump = False
            man2.jumpCount = 10
    if keys[pygame.K_a] and man.x > man.vel:
        man.x -= man2.vel
        man.left = True
        man.right = False
        man.standing = False
    elif keys[pygame.K_d] and man.x < 640 - man.width - man.vel:
        man.x += man.vel
        man.right = True
        man.left = False
        man.standing = False
    else:
        man.standing = True
        man.walkCount = 0

    if not(man.isJump):
        if keys[pygame.K_w]:
            man.isJump = True
            man.right = False
            man.left = False
            man.walkCount = 0
    else:
        if man.jumpCount >= -10:
            neg = 1
            if man.jumpCount < 0:
                neg = -1
            man.y -= (man.jumpCount ** 2) * 0.5 * neg
            man.jumpCount -= 1
        else:
            man.isJump = False
            man.jumpCount = 10
    if keys[pygame.K_SPACE] and shootLoop == 0:
        if man.left:
            facing2 = -1
        else:
            facing2 = 1
        if len(tiros) < 4:
            bulletSound.play()
            tiros.append(projectile(round(man.x + man.width //2), round(man.y + man.height//2), 6, (236,20,25), facing2))
        shootLoop = 1

    if (estado == 'end'):
        if(keys[pygame.K_r]):
            estado == 'jogando'
            score = 10
            score2 = 10
            man.health = 10
            man2.health = 10
            man.x = 100
            man2.x = 500
            man.visible = True
            man2.visible = True
            bullets = []
            tiros = []
        if(keys[pygame.K_q]):
            pygame.quit()



    redrawGameWindow()

pygame.quit()
