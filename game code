import pygame
import random
import math

# import sys
# import time
pygame.init()

# szerokość i wysokość obszaru roboczego
screen = pygame.display.set_mode((1280, 800),)

# muzyczka
pygame.mixer.music.load(r'C:\Users\Acer Aspire 3\Documents\muzyka.mp3')
pygame.mixer.music.play(-1)


# tło
background = pygame.image.load("Pictures/tlo.jpg")

# nazwa okienka, załadowanie ikonki oraz sprawienie, aby była widocna
pygame.display.set_caption('Kill the mosquitoes!')
icon = pygame.image.load("Pictures/no_for_mosquitoes.png")
pygame.display.set_icon(icon)

# Gracz
player_image = pygame.image.load("Pictures/wąż.png")
player_x = 550          # stała
player_y = 660          # stała
player_x_change = 0     # to zmienna dla różnicy, o jaką będzie poruszał się nasz statek (lewo,prawo)

# Wróg
enemy_image = pygame.image.load("Pictures/mosquito.png")
enemy_x = random.randint(0, (1280-64))   # wróg będzie pojawiał się w losowym miejscu na danym obszarze
enemy_y = random.randint(0, 400)
enemy_x_change = 0.7
enemy_y_change = 0.2

# wróg 2
enemy2_image = pygame.image.load("Pictures/mosquito (1).png")
enemy_x2 = random.randint(0, (1280-64))   # wróg będzie pojawiał się w losowym miejscu na danym obszarze
enemy_y2 = random.randint(0, 400)
enemy_x_change2 = 0.7
enemy_y_change2 = 0.2

# wróg 3
enemy3_image = pygame.image.load("Pictures/mosquito (2).png")
enemy_x3 = random.randint(0, (1280-64))   # wróg będzie pojawiał się w losowym miejscu na danym obszarze
enemy_y3 = random.randint(0, 400)
enemy_x_change3 = 0.7
enemy_y_change3 = 0.2


# Kropla
# ready- nie ma pocisku na ekranie. Player gotowy do ataku
# fire - pocisk jest na ekranie
water_image = pygame.image.load("Pictures/drop (1).png")
water_x = 0    # 0 bo zależeć to będzie od położenia statku
water_y = 585
water_y_change = 2
stan = "ready"

# Wynik
wynik = 0
font = pygame.font.Font('freesansbold.ttf', 32)
textx = 30
texty = 30


# funkcje slużące do pokazywania
def pokazwynik(x, y):
    score = font.render("Wynik: " + str(wynik), True, (9, 69, 87))
    screen.blit(score, (x, y))


def koniec_gry():

    end = font.render("Game Over", True, (9, 69, 87))
    screen.blit(end, (550, 400))


def player(x, y):
    screen.blit(player_image, (x, y))


def enemy(x, y):
    screen.blit(enemy_image, (x, y))


def enemy2(x, y):
    screen.blit(enemy2_image, (x, y))


def enemy3(x, y):
    screen.blit(enemy3_image, (x, y))


def water(x, y):
    screen.blit(water_image, (x, y))


# bez słowa global generuję się ostrzeżenie otym, że w funkcji nadawana jest wartość zmiennej, która globalnie już ją ma
# dzięki 'global' mówimy, że chodzi o zm globalną
# FUNKCJA DO WYWOŁYWANIA JAK TRZEBA
def water_bullet(x, y):
    global stan
    stan = "fire"                       # funkcja zmienia stan na fire, a następnie generuje pocisk
    screen.blit(water_image, (x, y))


# funkcja sprawdza odległość oraz czy nastąpi kolizja
# jeśli odl jest mniejsza niż 32 to zwróci True
def nastapi_kolizja():
    global enemy_y
    global enemy_x
    global water_y
    global water_x
    odl = math.sqrt(pow((enemy_x-water_x), 2) + pow((enemy_y-water_y), 2))
    if odl < 32:
        return True
    else:
        return False


def druga_kolizja():
    global enemy_y2
    global enemy_x2
    global water_y
    global water_x
    odl2 = math.sqrt(pow((enemy_x2 - water_x), 2) + pow((enemy_y2 - water_y), 2))
    if odl2 < 32:
        return True
    else:
        return False


def trzecia_kolizja():
    global enemy_y3
    global enemy_x3
    global water_y
    global water_x
    odl2 = math.sqrt(pow((enemy_x3 - water_x), 2) + pow((enemy_y3 - water_y), 2))
    if odl2 < 32:
        return True
    else:
        return False


# pętla gry
dzialanie = True
while dzialanie:
    # screen.fill((0, 0, 0))
    screen.blit(background, (0, 0))
    for event in pygame.event.get():    # ta funkcja zwraca listę zdarzeń wywyołanych przez gracza(np. przesuwanie okna)
        if event.type == pygame.QUIT:   # jeśli gracz zamknie okno gry, to przestaje ona działać UWAGA! pamiętaj o .type
            dzialanie = False

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                player_x_change = -0.7
            if event.key == pygame.K_RIGHT:
                player_x_change = 0.7
            if event.key == pygame.K_SPACE:
                if stan == "ready":
                    water_x = player_x
                    water_bullet(water_x, water_y)
        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                player_x_change = 0

    # poruszanie statkiem w lewo lub w prawo
    player_x = player_x + player_x_change

    # Granice dla statku
    # dla statku wystarczy podać 0 i szerokość maksymalną bo może on stać w miejscu
    if player_x <= 0:
        player_x = 0
    if player_x >= (1280-128):
        player_x = (1280-128)

    # Nasz wróg będzie poruszał się w dół oraz na boki
    enemy_x = enemy_x + enemy_x_change
    enemy_y = enemy_y + enemy_y_change
    enemy_x2 = enemy_x2 + enemy_x_change2
    enemy_y2 = enemy_y2 + enemy_y_change2
    enemy_x3 = enemy_x3 + enemy_x_change3
    enemy_y3 = enemy_y3 + enemy_y_change3

    # Granice dla wroga
    # u wroga nie można zostawić tylko 0 bo on ma się cały czas ruszać, a nie stać
    if enemy_x <= 0:
        enemy_x_change = 0.3
        enemy_y += enemy_y_change
    if enemy_x >= (1280-64):
        enemy_x_change = -0.3
        enemy_y += enemy_y_change

    if enemy_x2 <= 0:
        enemy_x_change2 = 0.3
        enemy_y2 += enemy_y_change2
    if enemy_x2 >= (1280 - 64):
        enemy_x_change2 = -0.3
        enemy_y2 += enemy_y_change2

    if enemy_x3 <= 0:
        enemy_x_change3 = 0.3
        enemy_y3 += enemy_y_change2
    if enemy_x2 >= (1280 - 64):
        enemy_x_change3 = -0.3
        enemy_y3 += enemy_y_change3

    if enemy_y > 650 or enemy_y2 > 600 or enemy_y3 > 600:
        koniec_gry()


# Ruch kropli
    if water_y < 0:                     # dzięki temu po wystrzeleniu jednego pocisku, można strzelać dalej
        water_y = 585                   # bez tego gracz mógłby strzelić tylko 1 raz
        stan = "ready"

    if stan == "fire":                      # dzięki temu wystrzelony pocisk idzie do góry
        water_bullet(player_x, water_y)
        water_y = water_y - water_y_change

    # Kolizja
    # funkcję  wkładamy do zmiennej
    # jeśli wyjdzie 'true', to stan dla pocisku jest 'ready' , czyli możemy znowu strzelać, mamy +1 punkt
    kolizja = nastapi_kolizja()
    if kolizja:
        stan = "ready"
        wynik = wynik + 1
        enemy_x = random.randint(0, (1280 - 64))
        enemy_y = random.randint(0, 400)

    drugakolizja = druga_kolizja()
    if drugakolizja:
        stan = "ready"
        wynik = wynik + 1
        enemy_x2 = random.randint(0, (1280 - 64))
        enemy_y2 = random.randint(0, 400)

    trzecia = trzecia_kolizja()
    if trzecia:
        stan = "ready"
        wynik = wynik + 1
        enemy_x3 = random.randint(0, (1280 - 64))
        enemy_y3 = random.randint(0, 400)

    player(player_x, player_y)
    enemy(enemy_x, enemy_y)
    enemy2(enemy_x2, enemy_y2)
    enemy3(enemy_x3, enemy_y3)
    pokazwynik(textx, texty)
    pygame.display.update()
